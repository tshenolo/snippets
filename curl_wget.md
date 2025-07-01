# Curl & Wget Cheatsheet

*   **curl (Client URL)**:
    *   Purpose: Transfer data from or to a server, using various protocols (HTTP, HTTPS, FTP, etc.). Powerful for API testing.
    *   Basic GET: `curl http://example.com`.
    *   Output to File: `curl -o output.html http://example.com` or `curl -O http://example.com/file.tar.gz` (uses remote filename).
    *   Show Headers: `curl -I http://example.com` (HEAD request) or `curl -i http://example.com` (include response headers in output).
    *   Verbose Output: `curl -v http://example.com`.
    *   POST Request: `curl -X POST -H "Content-Type: application/json" -d '{"key":"value"}' http://example.com/api`.
    *   Other HTTP Methods: `-X PUT`, `-X DELETE`, etc.
    *   Sending Headers: `-H "Authorization: Bearer token"`.
    *   Following Redirects: `-L`.
    *   User Agent: `-A "My User Agent"`.
    *   Cookies: `-b "name=value"` (send), `-c cookie-jar.txt` (store received cookies).
    *   Insecure (ignore SSL errors, for testing): `-k`.
*   **wget (World Wide Web Get)**:
    *   Purpose: Non-interactive download of files from the web. Good for recursive downloads.
    *   Basic Download: `wget http://example.com/file.zip`.
    *   Output to Specific File: `wget -O output_filename.zip http://example.com/file.zip`.
    *   Recursive Download (e.g., mirror a site): `wget -r -np -k http://example.com` (`-r`: recursive, `-np`: no parent, `-k`: convert links). Use with caution.
    *   Limit Download Rate: `--limit-rate=100k`.
    *   Continue Interrupted Download: `-c`.
    *   Background Download: `-b`.
    *   Quiet Mode: `-q`.
    *   Specify User Agent: `--user-agent="My Agent"`.
    *   Ignore SSL errors: `--no-check-certificate`.
