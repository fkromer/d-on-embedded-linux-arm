# Interfacing with other machines

## RESTful API

One can use the "High-level declarative REST and web application framework"
[vibe.d](http://vibed.org/) to implement a RESTful API server or client on the
BB.

install [libevent](http://libevent.org/) which vibe.d depends on:

    sudo apt-get install libevent-dev

[vibe.d based RESTful API server example (DConf Talk)](DConf Talk)](https://www.youtube.com/watch?v=Zs8O7MVmlfw#t=19m14s)

[vibe.d based RESTful API client example (DConf Talk)](https://www.youtube.com/watch?v=Zs8O7MVmlfw#t=17m40s)

[example of HibernateD based ORM (DConf Talk)](https://www.youtube.com/watch?v=Zs8O7MVmlfw#t=22m32s)

## Sockets

For an example how a client and server may communicate via plain sockets refer
to the source code in
[`/code/clientserver`](https://github.com/fkromer/d-on-embedded-linux-arm/tree/master/code/clientserver).

You can build the scripts `client` and `server` with the build script `build`
in the same directory.
