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

## Commit 3 note
![Commit 3 screen capture](/assets/images/commit3.png)
Incorporating request validation, the server now distinguishes between valid and invalid requests, responding accordingly with the appropriate content or a 404 Not Found page. This validation process involves parsing the initial request line to determine the requested target path. Based on this path, the server selects the corresponding HTML file to serve. For instance, the root path (GET / HTTP/1.1) triggers the server to serve hello.html, while any other requests prompt the server to serve bad.html. This approach ensures tailored responses based on the nature of the client's request.

## Commit 4 note
Introducing a simulated slow request, the server now includes a conditional delay for a designated route (/sleep), demonstrating its behavior under heavy loads or during slow processing scenarios. Utilizing Rust's thread::sleep function, this feature mimics resource-intensive operations or sluggish network responses by pausing the server's execution for ten seconds upon receiving a request to the /sleep path. This modification underscores the synchronous nature of our server, where handling a slow request can impede the processing of subsequent requests, revealing a significant limitation in scalability and responsiveness.

## Commit 5 note
Initially, a message passing channel facilitates communication between a pool and individual threads for task transmission. The ThreadPool creates worker threads, each with a unique identifier and a receiver obtained from the channel. Workers await tasks, execute them exclusively, and lock their receivers until completion.

The ThreadPool, instantiated with workers and a sender from the channel, dispatches tasks provided via ThreadPool.execute. In the main code, a four-worker thread pool is initialized. Upon receiving a stream from TCPListener, handle_connection(stream) is sent to ThreadPool.execute, assigning HTTP request handling to a worker.






