# Task 12: Consuming Public APIs Using Python

## 📌 Overview
This task demonstrates how to **consume a public REST API** using Python.  
It covers sending HTTP requests, checking response status, parsing JSON, extracting nested fields, handling errors, formatting output, and saving API data locally.

In this example, we use a free **Quotes API** to fetch a random quote.

---

## 🛠 Tools Used
- Python  
- `requests` library  
- VS Code  

---

## 📂 Project Files
- `api_data_fetch.py` – API integration script  
- `quote.json` – Saved JSON response  

---

## 🔑 Key Concepts Covered
- Sending GET requests  
- Checking HTTP status codes  
- Parsing JSON into Python dictionaries  
- Extracting nested fields  
- Graceful API error handling  
- Formatting console output  
- Saving API data to a file  

---

## ▶ Setup

Install the required library:
```bash
pip install requests
Run the script:

python api_data_fetch.py
🧾 Source Code (api_data_fetch.py)
# TASK 12: Consuming Public APIs Using Python
# This script fetches a random quote from a public API and saves it to a file

import requests
import json

API_URL = "https://api.quotable.io/random"

def fetch_quote():
    """
    Sends a GET request to the API and returns JSON data.
    """
    try:
        response = requests.get(API_URL, timeout=10)

        # Check status code
        if response.status_code == 200:
            return response.json()
        else:
            print(f"API Error: Status Code {response.status_code}")
            return None

    except requests.exceptions.RequestException as e:
        print("Network Error:", e)
        return None


def save_to_file(data, filename="quote.json"):
    """
    Saves JSON data to a local file.
    """
    with open(filename, "w") as file:
        json.dump(data, file, indent=4)
    print(f"Data saved to {filename}")


def main():
    print("\nFetching a random quote...\n")
    data = fetch_quote()

    if data:
        # Extract required fields
        content = data.get("content", "N/A")
        author = data.get("author", "Unknown")

        # Display clean output
        print("--- Quote of the Moment ---")
        print(f"\"{content}\"")
        print(f"- {author}")

        # Save JSON response
        save_to_file(data)
    else:
        print("Failed to fetch quote.")


if __name__ == "__main__":
    main()
🖥 Sample Output
Fetching a random quote...

--- Quote of the Moment ---
"Be yourself; everyone else is already taken."
- Oscar Wilde

Data saved to quote.json
📦 Deliverables
API integration script (api_data_fetch.py)

Saved JSON response file (quote.json)

🎯 Learning Outcome
After completing this task, the intern understands:

How APIs communicate using HTTP

How to parse JSON responses in Python

How to handle network and API errors

How to extract and format data

How to store API responses locally

