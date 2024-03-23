## Commit 1 note
The function boosts content reading efficiency with BufReader for the input stream. It iterates through each line, mapping them into strings. Upon encountering an empty line, it accumulates the HTTP request details into an http_request vector. Finally, this vector is displayed in the terminal. This approach adeptly parses incoming streams, constructing a structured representation of HTTP requests for further processing.

## Commit 2 note
![Commit 2 screen capture](/assets/images/commit2.png)
The program first reads the incoming request using a similar method as described previously. Once the request is obtained, it proceeds to build an HTTP Response. This response is composed of three main parts:

The status line, which contains the HTTP version, status code, and status message.
The Content-length header, indicating the length of the content.
The content itself, which, in this case, is the HTML to be served.
To create the response, the program segregates each of these components into separate string variables. It then combines them into a single string using string formatting techniques. The order is structured as follows: status line, Content-length header, and content.

The status line and Content-length header are separated by a single \r\n, while the header section and content section are separated by two \r\ns. Once the response string is assembled, the program writes it back into the stream as bytes. This process ensures the prompt delivery of the requested HTML content to the client.