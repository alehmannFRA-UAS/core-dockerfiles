# NodeJS for CORE Network Emulator

## Getting Started

First set the Container Image Name to fgftk/nodejs-5g:latest

![node.jpg](https://github.com/alehmannFRA-UAS/core-dockerfiles/blob/main/nodejs-5g/img/node.jpg?raw=true) 

Next open Services and choose UserDefined service. Create a shell script named start.sh as depicted.

![userdefined.jpg](https://github.com/alehmannFRA-UAS/core-dockerfiles/blob/main/nodejs-5g/img/userDefined.jpg?raw=true)


## What is NodeJS

Node.js is a software platform for scalable server-side and networking applications. Node.js applications are written in JavaScript and can be run within the Node.js runtime on Mac OS X, Windows, and Linux without changes.

Node.js applications are designed to maximize throughput and efficiency, using non-blocking I/O and asynchronous events. Node.js applications run single-threaded, although Node.js uses multiple threads for file and network events. Node.js is commonly used for real-time applications due to its asynchronous nature.

Node.js internally uses the Google V8 JavaScript engine to execute code; a large percentage of the basic modules are written in JavaScript. Node.js contains a built-in, asynchronous I/O library for file, socket, and HTTP communication. The HTTP and socket support allows Node.js to act as a web server without additional software such as Apache.

## Dockerfile

* [GitHub](https://github.com/alehmannFRA-UAS/core-dockerfiles)

## License

View [license information](https://github.com/nodejs/node/blob/master/LICENSE) for Node.js or [license information](https://github.com/nodejs/docker-node/blob/master/LICENSE) for the Node.js Docker project.

As with all Docker images, these likely also contain other software which may be under other licenses (such as Bash, etc from the base distribution, along with any direct or indirect dependencies of the primary software being contained).

Some additional license information which was able to be auto-detected might be found in [the repo-info repository's node/ directory](https://github.com/docker-library/repo-info/tree/master/repos/node).

As for any pre-built image usage, it is the image user's responsibility to ensure that any use of this image complies with any relevant licenses for all software contained within.
