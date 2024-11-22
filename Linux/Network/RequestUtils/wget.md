wget stands for "Web GET"

In most cases, use with this options
```bash
wget -qO - http://example.com
```

By default, `wget` downloads the HTTP(S) response body (the content) to a file. The file is typically named based on the URL being accessed, and the behavior depends on the URL and server response. Here's how it works:

### Default Behavior:
1. **File Naming**:
   - If the URL points to a specific file (e.g., `http://example.com/file.txt`), `wget` saves the file with the same name (`file.txt`) in the current directory.
   - If the URL points to a directory or does not specify a file name (e.g., `http://example.com/`), `wget` saves the content to a file named `index.html`.

2. **Overwriting**:
   - If a file with the same name already exists, `wget` appends a numerical suffix to avoid overwriting (e.g., `index.html.1`, `index.html.2`, etc.).

3. **Content Type**:
   - The server determines the content type, but `wget` does not alter the file name based on the `Content-Type` header unless explicitly told to do so.

### Examples:
- **Downloading a specific file**:
  ```bash
  wget http://example.com/file.txt
  ```
  Saves the file as `file.txt`.

- **Downloading from a directory**:
  ```bash
  wget http://example.com/
  ```
  Saves the content to `index.html`.

- **Avoid Overwriting**:
  ```bash
  wget http://example.com/file.txt
  wget http://example.com/file.txt
  ```
  Results in `file.txt` and `file.txt.1`.

---

### Options:
You can customize the default behavior using various options:

- **Custom Output File Name**:
  Use the `-O` option to specify a different name for the downloaded file:
  ```bash
  wget -O custom_name.txt http://example.com/file.txt
  ```
  - The value can be provided immediately after `-O` without a space, or with a space:
    - **With Space**: `-O custom_name.txt`
    - **Without Space**: `-Ocustom_name.txt`

- **Show in Terminal Only**:
  Use the `-O -` or `-O-` to display the response body in the terminal without saving it to a file:
  ```bash
  wget -O - http://example.com/
  ```

- **Do Not Overwrite**:
  Use the `--no-clobber` option to skip downloading if the file already exists:
  ```bash
  wget --no-clobber http://example.com/file.txt
  ```

- **`-q`**:
   - **Quiet mode**: Suppresses most of the output, such as download progress or verbose details.
   - Errors or critical messages (if any) are still displayed.

3. **`-S`**:
   - **Show server response headers**: Displays the HTTP headers received from the server, such as `Content-Type`, `Content-Length`, and status codes like `200 OK` or `404 Not Found`.

4. **`-O -`**:
   - **Output to standard output (stdout)**: Instead of saving the content to a file, the response body (HTML or other data) is written directly to the terminal (stdout).


```bash
wget -qO - http://example.com
```
