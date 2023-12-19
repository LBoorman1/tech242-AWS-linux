# Day6

## Changes to reverse proxy script
I had some issues on friday with configuring the reverse proxy, I think it had something to do with the order I was executing the commands.

I have changed the script so that the apache reverse proxy is configured before starting the maven build. This allows the apache server to be configured before hand and gives it time to
allow the proxy to be set up.

