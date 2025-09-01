# ClipsWebsite-forNetamiTV

This repository contains the source code for the NetamiTV Clips Website, a platform for managing and displaying clips from NetamiTV's streams.

## Features and Functionality

*   **Website Pages:** Provides various informative pages including an index, about, contact, terms of service, and privacy policy.
*   **Tutorial Section:** Includes detailed tutorials for creating and using clips on different devices (PC and Phone) and Video applications.
*   **Upload and Format Ideas:** Offers resources related to uploading clips and generating format ideas for content creation.
*   **Monetization Information:** Provides information on monetization options for clips.
*   **User Dashboard:** Allows users to manage their connected accounts, verification status, and view recent activity.
*   **Account Verification:** Integrates with Discord for user authentication and social media account verification (YouTube and TikTok).
*   **Admin Panel:** Provides an administrative interface for managing verification data (Excel) and banning IP addresses.
*   **IP-Based Banning:** Implements IP banning functionality to restrict access to the website for malicious users.
*   **Rate Limiting:** Protects the Discord API by limiting the number of requests per hour, preventing abuse and ensuring service availability.
*   **Error Handling:** Includes custom error pages (404 and 500) for a more user-friendly experience.
*   **Maintenance Mode:** Option to put the website into maintenance mode, displaying a maintenance page to users.

## Technology Stack

*   **Python:** The core programming language.
*   **Flask:** A micro web framework for building the web application.
*   **Werkzeug:** A comprehensive WSGI web application library.
*   **dotenv:** For loading environment variables from a `.env` file.
*   **openpyxl:** A Python library for reading and writing Excel files.
*   **requests:** A Python library for making HTTP requests.
*   **JSON:** For handling JSON data.
*   **HTML/CSS/JavaScript:** For the frontend.
*   **Logging:** Used for debugging and error tracking.
*   **Gunicorn:** Used to run the Flask application in production.

## Prerequisites

Before running this project, ensure you have the following installed:

*   Python 3.6 or higher
*   `pip` (Python package installer)

## Installation Instructions

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/n1yshi/ClipsWebsite-forNetamiTV.git
    cd ClipsWebsite-forNetamiTV
    ```

2.  **Create a virtual environment (recommended):**

    ```bash
    python3 -m venv venv
    source venv/bin/activate  # On Linux/macOS
    venv\Scripts\activate  # On Windows
    ```

3.  **Install the dependencies:**

    ```bash
    pip install -r requirements.txt
    ```

4.  **Configure environment variables:**

    *   Create a `.env` file in the project root directory.
    *   Add the following variables to the `.env` file, replacing the example values with your actual values:

        ```
        SECRET_KEY=your-secure-secret-key-here
        DISCORD_CLIENT_ID=your_discord_client_id
        DISCORD_CLIENT_SECRET=your_discord_client_secret
        DISCORD_REDIRECT_URI=your_discord_redirect_uri
        YOUTUBE_API_KEY=your_youtube_api_key
        ```

        **Note:**  `SECRET_KEY` is crucial for session management. `DISCORD_CLIENT_ID`, `DISCORD_CLIENT_SECRET`, and `DISCORD_REDIRECT_URI` are needed for Discord authentication. `YOUTUBE_API_KEY` is required for YouTube video verification.

5. **Set Admin Password Hash:**

    Locate the `ADMIN_PASSWORD_HASH` variable in `main.py` and replace the current hash.  **Important:** Generate a secure password hash using `werkzeug.security.generate_password_hash` and store it safely.

    ```python
    ADMIN_PASSWORD_HASH = generate_password_hash("your_secure_password")
    ```

## Usage Guide

1.  **Initialize banned IPs:**

    The application needs a `banned_ips.json` file. It can be created automatically when you first run it, or you can ensure that the `init_banned_ips()` function in `banned_ips.py` is called upon startup of the main application.

2.  **Run the application:**

    ```bash
    python main.py
    ```

    or, for production:

    ```bash
    gunicorn --bind 0.0.0.0:10938 main:application
    ```

    **Note:** The application will start on `0.0.0.0:10938` by default, make sure that port is available.
    You can change this from the `main.py` file:

    ```python
    app.run(host='0.0.0.0', port=10938, debug=False)
    ```

3.  **Access the website:**

    Open your web browser and navigate to `http://localhost:10938` (or the appropriate address based on your configuration).

4.  **Admin Panel:**

    *   Access the admin panel by navigating to `/admin/excel`.
    *   Log in using the username `admin` and the password set by the hashed password.
    *   The admin panel allows viewing the `verification_data.xlsx` file, downloading it, and managing banned IPs.

5.  **Rate Limit Reset (Development Only):**

    *   The `/reset-rate-limit` route is available in debug mode.  It resets the rate limit data stored in `discord_rate_limit.json`.  This is for development and testing purposes *only*.

## API Documentation

There is no explicit API. The application provides web-based user and admin interfaces.

## Contributing Guidelines

1.  Fork the repository.
2.  Create a new branch for your feature or bug fix.
3.  Implement your changes and write tests.
4.  Ensure all tests pass.
5.  Submit a pull request with a clear description of your changes.

## License Information

No license is specified for this project. All rights are reserved by the repository owner.

## Contact/Support Information

For questions, support, or feature requests, please contact:

*   Elias (NetamiTV): netamitv.site@gmail.com
*   Join Discord for support: [https://dsc.gg/netamitv](https://dsc.gg/netamitv)