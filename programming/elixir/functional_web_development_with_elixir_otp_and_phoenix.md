# Functional web development with elixir opt and phoenix

Many early client server systems were stateful. Servers kept working state in memory. They passed messages back and forth with their clients over persis- tent connections. Think of a banking system with a central mainframe and a dedicated terminal for each teller. This worked because the number of clients was small. Having fewer clients limited the system resources necessary to maintain those concurrent connections.

Then Tim Berners-Lee invented a new client server system called the World Wide Web.

The Web is an incredibly successful software platform. It’s available almost everywhere on Earth, on virtually any device. As the Web has grown and spread, so has HTTP. HTTP is a stateless protocol, so we think of Web applications as stateless as well. This is an illusion. State is necessary for applications to do anything interesting, but instead of keeping it in memory on the server, we push it off into a database where it awaits the next request.

Offloading state to a database provides some real advantages. HTTP based applications need only maintain temporary connections with clients until they send a response, so they require far fewer resources to serve the same number of requests. Most languages can’t muster the concurrency necessary to maintain enough persistent connections to be meaningful for a modern Web application.

Going “stateless” has let us scale.
But statelessness comes at a cost. It introduces significant latency as applications need to make one or more trips to the database for the data to prepare a response. It makes the database a scaling bottleneck, and it habituates us to model data for databases rather than for application code.

Elixir offers more than enough concurrency to power stateful servers. Phoenix Channels provide the conduit. A single Phoenix application can maintain persistent Channel connections to hundreds of thousands or even millions of clients simultaneously. Those clients can all broadcast messages to each other, coordinated through the server. While processing those messages, the application remains snappy and responsive. Elixir and Phoenix provide a legitimate alternative to stateless servers capable of handling modern Web traffic.



