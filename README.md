# comment
import os
import json
import time
import logging
from datetime import datetime, timedelta
from typing import List, Dict, Optional

import requests
import numpy as np
import openai
from dotenv import load_dotenv

# Load environment variables
load_dotenv()

# Setup logging
logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(levelname)s - %(message)s')

class CommentBot:
    def __init__(self, data_file="training_data.json"):
        """
        Initialize bot with API clients and load training data.
        """
        self.openai_api_key = os.getenv("OPENAI_API_KEY")
        self.platform_token = os.getenv("PLATFORM_ACCESS_TOKEN")
        self.page_id = os.getenv("PAGE_ID")
        self.data_file = data_file

        if not all([self.openai_api_key, self.platform_token, self.page_id]):
            raise ValueError("Missing required environment variables.")

        openai.api_key = self.openai_api_key
        self.client = openai.OpenAI(api_key=self.openai_api_key)

        # Training data structure: list of dicts with "comment", "reply", and optionally "embedding"
        self.training_data = self.load_training_data()

        # Keep track of last processed comment time to avoid duplicates
        self.last_check_time = datetime.utcnow() - timedelta(minutes=10)  # start 10 min ago

        # Platform API base URL (example: Facebook Graph API)
        self.api_base = "https://graph.facebook.com/v18.0"

    def load_training_data(self) -> List[Dict]:
        """Load training examples from JSON file."""
        if os.path.exists(self.data_file):
            with open(self.data_file, 'r') as f:
                return json.load(f)
        return []

    def save_training_data(self):
        """Save training examples to JSON file."""
        with open(self.data_file, 'w') as f:
            json.dump(self.training_data, f, indent=2)

    def get_embedding(self, text: str) -> List[float]:
        """Get embedding vector for text using OpenAI."""
        response = self.client.embeddings.create(
            input=text,
            model="text-embedding-ada-002"
        )
        return response.data[0].embedding

    def update_embeddings(self):
        """Compute and store embeddings for all training examples (if missing)."""
        for ex in self.training_data:
            if "embedding" not in ex:
                ex["embedding"] = self.get_embedding(ex["comment"])
        self.save_training_data()

    def find_similar_examples(self, comment: str, top_k: int = 3) -> List[Dict]:
        """
        Find top_k most similar training examples to the given comment using cosine similarity.
        """
        if not self.training_data:
            return []

        # Ensure all examples have embeddings
        self.update_embeddings()

        # Get embedding for the new comment
        comment_emb = self.get_embedding(comment)

        # Compute similarities
        similarities = []
        for ex in self.training_data:
            emb = ex["embedding"]
            # Cosine similarity
            sim = np.dot(comment_emb, emb) / (np.linalg.norm(comment_emb) * np.linalg.norm(emb))
            similarities.append((sim, ex))

        # Sort by similarity descending
        similarities.sort(key=lambda x: x[0], reverse=True)
        return [ex for _, ex in similarities[:top_k]]

    def generate_reply(self, comment: str) -> Optional[str]:
        """
        Generate a reply for the comment using GPT with similar examples as context.
        """
        similar = self.find_similar_examples(comment)

        # Build a prompt with examples
        prompt = "You are a helpful assistant that replies to comments on a social media page. Use the following examples of past comments and replies as a guide for style and tone. Then reply to the new comment.\n\n"

        for i, ex in enumerate(similar, 1):
            prompt += f"Example {i}:\nComment: {ex['comment']}\nReply: {ex['reply']}\n\n"

        prompt += f"New comment: {comment}\nReply:"

        try:
            response = self.client.chat.completions.create(
                model="gpt-3.5-turbo",
                messages=[
                    {"role": "system", "content": "You are a social media manager who replies to comments in a friendly and helpful manner."},
                    {"role": "user", "content": prompt}
                ],
                max_tokens=150,
                temperature=0.7
            )
            reply = response.choices[0].message.content.strip()
            return reply
        except Exception as e:
            logging.error(f"OpenAI API error: {e}")
            return None

    def fetch_new_comments(self) -> List[Dict]:
        """
        Fetch comments from the platform that were created after last_check_time.
        Returns list of dicts with 'id', 'text', 'author', 'timestamp'.
        """
        # This is a placeholder. Replace with actual API call to your platform.
        # Example for Facebook: GET /{page-id}/posts?fields=comments{id,message,from,created_time}
        # We'll simulate with a dummy response.
        url = f"{self.api_base}/{self.page_id}/feed"
        params = {
            "access_token": self.platform_token,
            "fields": "comments{id,message,from,created_time}",
            "since": int(self.last_check_time.timestamp())
        }
        try:
            resp = requests.get(url, params=params)
            resp.raise_for_status()
            data = resp.json()
            comments = []
            # Parse the nested structure (simplified)
            for post in data.get("data", []):
                for comment in post.get("comments", {}).get("data", []):
                    comments.append({
                        "id": comment["id"],
                        "text": comment["message"],
                        "author": comment["from"]["name"],
                        "timestamp": comment["created_time"]
                    })
            return comments
        except Exception as e:
            logging.error(f"Error fetching comments: {e}")
            return []

    def post_reply(self, comment_id: str, reply_text: str) -> bool:
        """
        Post a reply to the specified comment.
        Returns True if successful.
        """
        # Placeholder: replace with actual API call
        url = f"{self.api_base}/{comment_id}/comments"
        params = {
            "access_token": self.platform_token,
            "message": reply_text
        }
        try:
            resp = requests.post(url, data=params)
            resp.raise_for_status()
            logging.info(f"Replied to comment {comment_id}")
            return True
        except Exception as e:
            logging.error(f"Error posting reply: {e}")
            return False

    def train_on_manual_reply(self, comment: str, reply: str):
        """
        Add a new example to the training data (e.g., when you manually reply).
        """
        self.training_data.append({
            "comment": comment,
            "reply": reply
            # embedding will be added later when needed
        })
        self.save_training_data()
        logging.info("Added new training example.")

    def run_once(self):
        """Single iteration: fetch new comments, generate & post replies."""
        comments = self.fetch_new_comments()
        for comment in comments:
            # Avoid replying to yourself or already replied (you may want to check)
            # Generate reply
            reply = self.generate_reply(comment["text"])
            if reply:
                success = self.post_reply(comment["id"], reply)
                if success:
                    # Optionally auto-train on successful reply (if you trust it)
                    # self.train_on_manual_reply(comment["text"], reply)
                    pass
            time.sleep(1)  # be gentle with rate limits

        # Update last check time
        self.last_check_time = datetime.utcnow()

    def run(self, interval_seconds=60):
        """
        Main loop: run periodically.
        Set interval_seconds to how often to check for new comments.
        """
        logging.info("Bot started. Press Ctrl+C to stop.")
        try:
            while True:
                self.run_once()
                time.sleep(interval_seconds)
        except KeyboardInterrupt:
            logging.info("Bot stopped.")

# ===== Usage Example =====
if __name__ == "__main__":
    bot = CommentBot()

    # Optional: manually add training examples
    # bot.train_on_manual_reply("Great post!", "Thank you! Glad you liked it.")
    # bot.train_on_manual_reply("When is the next event?", "We'll announce it soon. Stay tuned!")

    # Start the bot
    bot.run(interval_seconds=120)  # check every 2 minutes
