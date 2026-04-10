# CS 4700 Web Crawler

### High-Level Approach
This project implements a web crawler in Python that navigates the Fakebook website to locate five hidden secret flags scattered across its pages. 

Before crawling anything, the crawler logs into the website. It first sends a `GET` request to `/accounts/login/` to extract the CSRF token and cookie from the page, then sends a `POST` request with the username, password, and CSRF token. The response sets a `sessionId` cookie, which is attached to all subsequent requests to maintain and authenticated session. 

The crawler then seeds its queue by traversing through the links of the website using BFS. On each iteration it dequeues a link, and then scans the page for secret flags using a regex match as well as parses all links on the page to enqueue any links it has not visited yet. 503 responses are retried automatically. The loop continues until either the queue is exhausted or all five flags are found. 

Once the loop is terminated, the five flags are printed out.

### Challenges I faced
Early on, the login was failing silently (returning a 403), so `sessionId` remained set to `None` and all subsequent page requests were unauthenticated. It took me a while to figure out the issue but I was able to figure it out with debugging statements. Before then, it was hard to tell that there was any issue with my code. 

I also had issues with forgetting to add a trailing slash to the links. Requesting `/accounts/login`, for example, caused the server to return a 301 redirect with an empty body, so there was no CSRF token or cookie to extract. The fix was simply to add a trailing slash, but diagnosing the issue took some time. 

### Overview of how I tested my code
I relied heavily on print statements to track the progress of the crawler and see what it was doing. I also first tested my crawler by hard-coding the `GET` request to other pages as I was working on implementing keeping track of the links visited logic. I tested regex-based secret flag detection by using multiple sample pages to ensure its functionality. I also ran the final code repeatedly to ensure that it was consistently able to find the five flags. 