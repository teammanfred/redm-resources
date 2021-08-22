# Running the RedM server to ‘host a server’

* Installing a FiveM server will take around an hour if you are lucky
* Releases are around 50 megabytes
* Server data is around 170 megabytes
* You will have to create a Cfx.re account ~ 10 minutes

## Canonical documentation

The Cfx.re forums have the canonical documentation on [How to setup a RedM server](https://forum.cfx.re/t/how-to-setup-a-redm-server/918850). Please read those first, the instructions below are notes on those instructions.

## Getting your your Steam Web API Key

**⚠️ YOUR STEAM WEB API KEY GIVES ACCESS TO YOUR STEAM ACCOUNT – DO NOT SHARE THIS KEY**

1. Go to https://steamcommunity.com/dev/apikey
2. It doesn't matter what domain name you use for your key in this particular case, just **don't** use an existing domain you don't control. The safest may be to use `your-name.example.com`.

## Creating a license key

**⚠️ YOUR FIVEM SERVER KEY ALLOW OTHER TO RUN SERVERS UNDER YOUR NAME DO NOT SHARE THESE KEYS**

1. Server name is for your own administration – use anything you want
2. IP address must be an IPv4 address, IPv6 is not supported. You can Google "what is my ip" if you want to know the address of your home connection. 
3. We believe the other fields are used by Cfx.re to get an insight on who is running servers, may as well be nice and let them know.

## Debian or Ubuntu

The instructions take some liberties and assume you know things about things.

### Git

Git is a *distributed version control system*. You will have to install it to get the server data from GitHub.

    apt install git

The output of the command can be a bit noisy, don't worry unless it spews actual errors.

## Using the setup script

Find a nice directory on your machine to keep the server data, for example:

    cd ~
    mkdir -p redm && cd redm
    mv ~/Downloads/setup .
    chmod +x setup
    ./setup

You can run the script multiple times and it will try to be smart about not doing the same thing multiple times.

After this you should be able to run the server:

    ./redm

Or you can run the provided run script directly:

    ./run.sh +set gamename rdr3 +set config server.cfg

## Using the Dockerfile

Change `server.cfg` to fit your needs. You can change `redm` to anything else if you want to create different images.

    docker build -t redm .

Then you can create and start a new container like this:

    docker run -i -t --rm -p 30120:30120 -p 40120:40120 redm ./redm

Please wait until `yarn` finishes compiling all the module assets. Then reboot the server through the web interface on port `40120`

For more control you can start a container and atach it to your console to start the server yourself:

    docker run -a stdin -a stdout -i -t --rm -p 30120:30120 -p 40120:40120 redm
    ./run.sh +set gamename rdr3 +set config server.cfg

Note that this will wipe all server data every time you start it, if you want to persist data it's probably best to learn about Docker volumes.

## Troubleshooting

### Infinite loading screen

Infinite loading screens are likely resource scripts crashing on either the server or client during load. Sometimes they don't show up in logs so they can be hard to debug.

Note that resource loading order may be relevant. Make sure you have the lines with `ensure` in the same order as the examples.

When you run into problems you can reduce the resources to a bare minimum and load them after the server started.

On the client you can open the console with F8. The console may contain hints about what is going wrong.


### qemu: uncaught target signal 6 (Aborted) - core dumped

You are probably attempting to run the server on an M1 mac, that won't work due to an upstream problem in `qemu`.
