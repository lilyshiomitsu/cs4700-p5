# Fakebook Web Crawler

Alan Zhang

## Table of Contents
1. [Initializing Fields](#initializing-fields)
2. [Helpers](#helpers)
3. [Major Difficulties](#major-difficulties)
4. [Testing](#testing)

## Initializing Fields
- From the starter code, the program takes in command-line arguments for the server, port, username, and password.
- The default values for the server and port are `fakebook.khoury.northeastern.edu` and `443`, respectively.
- This crawler maintains a session using CSRF token, session ID, and the csrfmiddleware token.
- BFS is implemented to help with the iteration and actual web crawling in search of the secret flags.
    - A `deque` is used to store discovered links and process them.
    - A `set` is used to track visited links and cycles.

## Helpers
- Core helper functions include:
  - `send_request`: Handles HTTP requests and responses, including headers, cookies, and gzip decoding.
  - `extract_csrf_token`: Extracts the CSRF middleware token from the login page HTML.
  - `get_csrf_token`: Sends an initial request to retrieve authentication tokens from cookies and form data.
  - `login`: Performs the login by sending a POST request with the username, password, and CSRF token.
  - `crawl_link`: Processes each page, searching for secret flags and handling new links.
  - `run`: Manages the overall crawling process, starting from login and running BFS until all five secret flags are found.

## Major Difficulties
- Properly formatting the login POST request and GET was a huge obstacle and took a significant amount of time.
- It took a while to figure out I had to use both the csrfmiddleware token and the one in the Headers under set-cookie.
- Finding an efficient way to crawl took some research before settling on BFS.
- It was difficult to tell if my program was working and just taking a long time or if I was waiting on nothing.

## Testing
- I ran the final code repeatedly and timed it to be usually in the 5-10 minutes range.
- Used print statements to track the progress of the crawler.
- First tested by hard-coding the GET request to other pages and then updating the visited_links and parser.links logic.
- Ensured that the crawler only followed `/fakebook` links while avoiding irrelevant links such as the home page and logout.
- Tested regex-based secret flag detection using multiple sample pages.