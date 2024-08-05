# developer-resources

### FastCGI
FastCGI is a protocol that defines how your web server (Apache, nginx, lighttpd, etc.) communicates to your CGI program (your server side application in PHP, Ruby, Python, etc.) about the requests it receives. It's an extension of CGI.

In a nutshell, both CGI and FastCGI just describe how to pass a bunch of values — such as HTTP headers, the request body and client input — to the server-side part of your website.

In traditional CGI, when the web server receives an HTTP request it fires up your application as a process, connected by a pipe to send client input though standard input, and then puts all the other values into environment variables. The application then responds through standard output back to the web server which in turn sends it back to the client. FastCGI makes a few changes to this.

Instead of firing up a process with every request, they get started when the web server starts. The process then hangs around to deal with any requests and doesn't get killed when it finishes a request - it just waits for more. This gets rid of any overheads to do with killing and creating processes and allows the processes to do any "set-up" work only once.

FastCGI also stops using operating system pipes and environment variables for communication and instead multiplexes all of this information over a TCP connection. This means that your web server and application are now location independent and can be running on different machines.
Running as fastCGI means that a daemon is running with an open pipe, ready to answer. The Web server sends the request to CGI program's (PHP, Ruby, Python, etc) pipe and PHP replies directly. Caching extensions, notably APC, work way better this way because they are never unloaded from memory.

Using fastCGI doesn’t use more much more memory for a single request but since the process is kept live, it can add up and use more than a module. However, it is still negligible compared to the speed gain.

To make use of FastCGI, most web servers have a module (often installed by default) to handle all of this.
The best way to learn about FastCGI is to read the white paper and at least some of the [specification](https://fastcgi-archives.github.io/).
