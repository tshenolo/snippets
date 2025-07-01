# Curl & Wget Cheatsheet

This cheatsheet covers common uses of `curl` and `wget`, two command-line utilities for transferring data using various network protocols.

## `curl` (Client URL)

`curl` is a versatile tool for transferring data from or to a server, supporting protocols like HTTP, HTTPS, FTP, FTPS, SCP, SFTP, LDAP, etc. It's widely used for API testing and interaction.

*   **Basic GET Request** (display content to stdout):
    ```bash
    curl http://example.com
    curl https://api.example.com/data
    ```
*   **Save Output to a File**:
    *   Using redirection (standard shell feature):
        ```bash
        curl http://example.com/page.html > page.html
        ```
    *   Using `-o` (lowercase o, specify filename):
        ```bash
        curl -o output_filename.html http://example.com/page.html
        ```
    *   Using `-O` (uppercase O, use remote filename):
        ```bash
        curl -O http://example.com/archive.tar.gz
        # Saves as archive.tar.gz in the current directory
        ```
*   **Show HTTP Headers Only (HEAD Request)**:
    ```bash
    curl -I http://example.com
    # Or --head
    ```
*   **Include HTTP Response Headers in Output (along with body)**:
    ```bash
    curl -i http://example.com
    # Or --include
    ```
*   **Verbose Output** (shows connection details, headers sent/received):
    ```bash
    curl -v http://example.com
    # For even more details (e.g., SSL handshake):
    # curl -vvv http://example.com
    ```
*   **Follow Redirects (`-L` or `--location`)**:
    ```bash
    curl -L http://example.com # If example.com redirects, curl will follow
    ```
*   **Specify HTTP Method**:
    *   POST Request:
        ```bash
        curl -X POST http://example.com/api/resource
        # With form data (application/x-www-form-urlencoded):
        curl -X POST -d "param1=value1&param2=value2" http://example.com/api/submit
        # With JSON data:
        curl -X POST -H "Content-Type: application/json" -d '{"key":"value", "number":123}' http://example.com/api/json_endpoint
        # POST data from a file:
        curl -X POST -d @data.json -H "Content-Type: application/json" http://example.com/api/post_file
        ```
    *   PUT Request:
        ```bash
        curl -X PUT -H "Content-Type: application/json" -d '{"update_key":"new_value"}' http://example.com/api/resource/123
        ```
    *   DELETE Request:
        ```bash
        curl -X DELETE http://example.com/api/resource/123
        ```
*   **Send Custom HTTP Headers (`-H`)**:
    ```bash
    curl -H "Authorization: Bearer myapitoken" -H "X-Custom-Header: MyValue" https://api.example.com/protected_data
    ```
*   **Set User Agent**:
    ```bash
    curl -A "MyCustomUserAgent/1.0" http://example.com
    # Or --user-agent
    ```
*   **Handle Cookies**:
    *   Send specific cookies:
        ```bash
        curl -b "sessionid=abc123xyz; user_pref=dark_mode" http://example.com
        ```
    *   Read cookies from a file and write received cookies to a file (cookie jar):
        ```bash
        curl -b cookies.txt -c cookies.txt -L http://example.com/login # Read from and write to cookies.txt
        ```
*   **Authentication**:
    *   Basic Authentication (`-u` or `--user`):
        ```bash
        curl -u username:password http://example.com/protected
        # Curl will prompt for password if only username is provided:
        # curl -u username http://example.com/protected
        ```
*   **SSL/TLS Options**:
    *   Insecure mode (ignore SSL certificate errors - **use with caution, security risk!**):
        ```bash
        curl -k https://self-signed.example.com
        # Or --insecure
        ```
    *   Specify custom CA certificate:
        ```bash
        curl --cacert /path/to/ca.crt https://internal.example.com
        ```
    *   Specify client certificate and key:
        ```bash
        curl --cert /path/to/client.pem --key /path/to/client.key https://secure.example.com
        ```
*   **Limit Transfer Rate**:
    ```bash
    curl --limit-rate 100K http://example.com/largefile.zip # Limit to 100 KB/s
    ```
*   **Resume Download (`-C -`)**:
    ```bash
    curl -C - -O http://example.com/largefile.zip # Continue a previously interrupted download
    ```
*   **Silent Mode (`-s` or `--silent`)**: Suppress progress meter and error messages.
    ```bash
    STATUS_CODE=$(curl -s -o /dev/null -w "%{http_code}" http://example.com)
    # This example gets only the HTTP status code.
    ```
*   **Show Error Messages (`-S` or `--show-error`)**: Use with `-s` to show errors but not progress.
    ```bash
    curl -sS http://nonexistent.example.com # Will show error message
    ```
*   **FTP Upload/Download**:
    *   Upload:
        ```bash
        curl -T localfile.txt ftp://username:password@ftp.example.com/remote/path/
        ```
    *   Download:
        ```bash
        curl -u username:password ftp://ftp.example.com/remote/file.txt -o local_file.txt
        ```
*   **Set Timeout**:
    *   Maximum time for the whole operation:
        ```bash
        curl --max-time 10 http://example.com
        ```
    *   Connection timeout:
        ```bash
        curl --connect-timeout 5 http://example.com
        ```

## `wget` (World Wide Web Get)

`wget` is a non-interactive network downloader. It's excellent for downloading files, mirroring websites, and recursive downloads.

*   **Basic Download** (saves to a file with the remote name):
    ```bash
    wget http://example.com/file.zip
    ```
*   **Specify Output Filename (`-O` - uppercase O)**:
    ```bash
    wget -O my_downloaded_file.zip http://example.com/some_archive.zip
    ```
*   **Continue Interrupted Download (`-c` or `--continue`)**:
    ```bash
    wget -c http://example.com/large_video.mp4
    ```
*   **Background Download (`-b` or `--background`)**:
    ```bash
    wget -b http://example.com/very_large_file.iso
    # Output and errors go to wget-log by default.
    ```
*   **Limit Download Rate (`--limit-rate`)**:
    ```bash
    wget --limit-rate=200k http://example.com/another_large_file.tar.gz # Limit to 200 KB/s
    ```
*   **Recursive Download (Mirroring a site - use responsibly and check `robots.txt`)**:
    ```bash
    wget --mirror -p --convert-links -P ./local_site_copy http://example.com/docs/
    # --mirror: Shortcut for -r -N -l inf --no-remove-listing (recursive, timestamping, infinite depth)
    # -p, --page-requisites: Download all necessary files for displaying the HTML page (images, CSS).
    # --convert-links: Convert links in downloaded HTML to point to local files.
    # -P ./local_site_copy: Save files to the specified directory.
    # -nH, --no-host-directories: Don't create host-prefixed directories.
    # --cut-dirs=number: Ignore number of remote directory components.
    ```
*   **Download Specific File Types Recursively**:
    ```bash
    wget -r -l1 -A.pdf http://example.com/documents/
    # -r: recursive
    # -l1: recursion depth 1 (current directory only)
    # -A.pdf: accept only files ending with .pdf
    ```
*   **Reject Specific File Types**:
    ```bash
    wget -r --reject=gif,jpg http://example.com/
    ```
*   **Quiet Mode (`-q` or `--quiet`)**: Suppress output.
    ```bash
    wget -q -O /dev/null http://example.com/ping # Check if a file is accessible without saving
    ```
*   **No Check Certificate (`--no-check-certificate`)**: Ignore SSL certificate errors (like `curl -k`). **Security risk!**
    ```bash
    wget --no-check-certificate https://self-signed.example.com/file.dat
    ```
*   **Set User Agent (`--user-agent`)**:
    ```bash
    wget --user-agent="MyWgetDownloader/1.1" http://example.com/
    ```
*   **Read URLs from a File (`-i`)**:
    ```bash
    # urls.txt contains one URL per line
    # http://example.com/file1.zip
    # http://another.example.com/doc.pdf
    wget -i urls.txt
    ```
*   **Retry Attempts (`-t` or `--tries`)**:
    ```bash
    wget -t 5 http://example.com/sometimes_unavailable_file.txt # Try 5 times
    # wget -t 0 # Infinite retries
    ```
*   **FTP Download**:
    ```bash
    wget ftp://ftp.example.com/pub/file.tar.gz
    # With username and password:
    # wget --ftp-user=myuser --ftp-password=mypass ftp://ftp.example.com/private/file.zip
    # Or:
    # wget ftp://myuser:mypass@ftp.example.com/private/file.zip (password visible in process list)
    ```
*   **Timestamping (`-N` or `--timestamping`)**: Only download files if the remote version is newer than the local one.
    ```bash
    wget -N http://example.com/data.csv
    ```
*   **Output messages to a log file (`-o`)**:
    ```bash
    wget -o download.log http://example.com/file.zip
    ```
*   **Append output to a log file (`-a`)**:
    ```bash
    wget -a download.log http://example.com/anotherfile.zip
    ```

Both `curl` and `wget` are powerful tools. `curl` is generally favored for complex interactions, API testing, and broader protocol support, while `wget` excels at straightforward downloads and recursive fetching.The `curl_wget.md` cheatsheet has been successfully updated with detailed command examples for various use cases of both `curl` and `wget`, including different HTTP methods, file handling, SSL options, and recursive downloading.

The final command-heavy cheatsheet to enhance in this phase is `tmux.md`. I will add more specific examples for session, window, and pane management.
