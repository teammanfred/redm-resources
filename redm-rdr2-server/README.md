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

## Troubleshooting

### Infinite loading screen

1. Try turning adding or revoving `ensure sessionmanager-rdr3` from `server.cfg`.
2. Remove session manage data: `rm -Rf redm/server-data/files/sessionmanager*`
3. Make sure players remove their cache folders after changing this setting.
