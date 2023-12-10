# Inbox Cleaner

This script helps manage a Gmail inbox by filtering out promotional emails using GPT-3 or GPT-4.

## Prerequisites

- Python 3.7 or higher
- Gmail account
- Google Cloud account with Gmail API enabled
- OpenAI API key

## Setup

1. Clone this repository:

   ```
   git clone https://github.com/isafulf/inbox_cleaner.git
   cd inbox_cleaner
   ```

2. Install the required Python packages:

   ```
   pip install -r requirements.txt
   ```

3. Set up your Google API credentials:

    - Follow the instructions [here](https://developers.google.com/workspace/guides/create-credentials) to create a new OAuth 2.0 Client ID.
    - Download the JSON file and rename it to `credentials.json`.
    - Put `credentials.json` in the `inbox_cleaner` directory.

4. Set up your OpenAI API key:

    - Follow the instructions [here](https://platform.openai.com/api-keys) to get your OpenAI API key.
    - Set the key as an environment variable:

      ```
      export OPENAI_API_KEY=<your_openai_api_key>
      ```

## Usage

Run the script:

```
python process_all_unread_emails.py
```

When prompted, enter your first and last name. The script will then start processing your unread emails.

## How the Code Works:

### Check for Existing Credentials:
- The function first checks if the `token.json` file exists. This file contains the user's saved access and refresh tokens. If it exists, the credentials are loaded from this file.

### Credential Validation:
- It checks if the loaded credentials are valid. If they are not valid or do not exist:
   - **Refresh Token**: If the credentials have expired but a refresh token is available, it refreshes the credentials.
   - **User Login**: If no valid credentials are available, it initiates an OAuth flow for the user to log in. This process involves opening a local server on port 9000 for the authentication flow, where the user grants access, and then the credentials are received.

### Save Credentials:
- After the user logs in, or the tokens are refreshed, the new credentials are saved in `token.json` for future use.

### Create Gmail Service:
- Finally, the function uses the credentials to create and return a Gmail service object, which can be used to interact with the Gmail API.
