# Interfacing with you and me

## Graphical web interface

### vibe.d based java script web gui example

download vibe.d, extract it and change into the example directory:

    wget https://github.com/vibe-d/vibe.d/archive/master.zip
    unzip master.zip
    cd vibe.d-master/examples/rest-js

build and run the example:

    dub run

open `http://127.0.0.1:8080/` in a browser

You can input data for a calculation (addition) and trigger its execution in the
gui. You can input a command in the web gui which is then executed in the
terminal which is running the example.

stop the server by hitting `ctrl+c`

### Addittional information

[vibe.d website example (DConf Talk)](https://www.youtube.com/watch?v=Zs8O7MVmlfw#t=12m56s)
