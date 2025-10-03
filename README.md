# Pentest Chat CLI

A user-friendly, interactive Command-Line Interface (CLI) for chatting with an AWS Bedrock Knowledge Base. This tool provides a professional chat experience with session management, allowing you to save, resume, and manage multiple conversations.



---

## ✨ Features

* **Interactive Chat Loop**: Engage in a continuous conversation without re-running commands.
* **Full Session Management**:
    * **Save & Resume**: Save chat sessions with custom names and resume them later, preserving the full conversation context.
    * **Session Menu**: An interactive menu on startup to easily select a recent session or start a new one.
    * **List & Delete**: Manage your saved sessions directly from the command line.
* **Rich Terminal Output**: Renders AI responses in Markdown, with beautiful formatting and syntax highlighting for code blocks.
* **Secure & Simple Backend**: Leverages the fully managed AWS Bedrock Knowledge Base service, eliminating the need for a custom backend.
* **Easy Configuration**: Automatically creates a simple `config.yml` file on the first run.

---

## ✅ Prerequisites

Before you begin, ensure you have the following set up:

1.  **AWS Account**: An active AWS account with the necessary permissions.
2.  **AWS CLI Configured**: Your local AWS CLI must be configured with credentials (`aws configure`). The tool uses these credentials via the `boto3` SDK.
3.  **AWS Bedrock Knowledge Base**: You must have a Knowledge Base configured in Amazon Bedrock. You will need two pieces of information:
    * Your **Knowledge Base ID**.
    * The **Model ARN** for the foundation model you want to use (e.g., Llama 3, Claude 3 Sonnet).

---

## 🚀 Installation & Setup

1.  **Clone the Repository**
    Clone this repository to your local machine:
    ```bash
    git clone <your-repository-url>
    cd pentest-chat-cli
    ```

2.  **Install Dependencies**
    It's highly recommended to use a Python virtual environment.
    ```bash
    # Create a virtual environment
    python3 -m venv venv

    # Activate it (on macOS/Linux)
    source venv/bin/activate

    # Install the required libraries
    pip install -r requirements.txt
    ```

3.  **Initial Configuration**
    Run the application for the first time to generate the configuration file:
    ```bash
    python ptchat.py
    ```
    This command will detect that no config file exists and create a default one at `~/.config/ptchat/config.yml`.

4.  **Edit the Configuration File**
    Open the newly created configuration file with your favorite text editor:
    ```bash
    # Example using nano
    nano ~/.config/ptchat/config.yml
    ```
    Replace the placeholder values with your actual **Knowledge Base ID** and **Model ARN**.

    ```yaml
    # ~/.config/ptchat/config.yml
    knowledge_base_id: "ABCDE12345" # <-- Replace this
    model_arn: "arn:aws:bedrock:us-east-1::foundation-model/meta.llama3-70b-instruct-v1:0" # <-- Replace this
    ```

---

## 💻 Usage

All commands are run from the root of the `pentest-chat-cli` directory.

### Starting a Chat

The main command to start or resume a session is `start`.

```bash
python ptchat.py start
```

This will present you with an interactive menu to choose a saved session or start a new one.

### Managing Sessions

You can also list or delete sessions directly.

**List all saved sessions:**
```bash
python ptchat.py session list
```

**Delete a session:**
This command will bring up an interactive menu to select which session to delete.
```bash
python ptchat.py session delete
```

### In-Chat Commands

Once you are in an interactive chat session, you can use the following commands:

* **/save `<name>`**: Saves the current conversation with a given name. If the session is already named, this will simply update it.
* **/quit** or **/exit**: Exits the current chat session.
* **/help**: Displays a list of available in-chat commands.

---

## 📁 Project Structure

```
pentest-chat-cli/
├── ptchat.py           # The main executable script
├── requirements.txt    # Project dependencies
└── ptchat/             # The core Python package
    ├── __init__.py     # Makes 'ptchat' a package
    ├── bedrock_client.py # Handles Boto3 calls to the AWS Bedrock service
    ├── config.py       # Manages loading the config.yml file
    └── session_manager.py # Manages all session file operations
```
