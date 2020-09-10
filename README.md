# Slow stub

This is the configuration file for a Hoverfly stub that will respond to every http or https request, but only after a delay of 600k milliseconds (10 minutes).

This should be slower than just about any downstream system response, and that makes this stub suitable for testing timeout scenarios.

## Instructions

To start this stub running:

`$ hoverctl start webserver`

`$ hoverctl import unresponsive.json`

Then to test it (note that these example requests shouldn't see a response for 10 minutes, so you probably want to Ctrl-C out of them):

`$ curl http://localhost:8500/anything/you/like`

`$ curl --header "Content-Type: application/json"   --request POST   --data '{"username":"xyz","password":"xyz"}'   http://localhost:8500/api/login`

Then to disable it:

`$ hoverctl stop -t local`

## Docker

To run this using a Docker instance of Hoverfly

`$ docker run -d -p 8888:8888 -p 8500:8500 spectolabs/hoverfly:latest -webserver`

## TODO

There's other stub configs as well:
- one that will send infinite redirects to a client, causing it to keep sending requests
- one that returns service unavailable (http 503)
- one that returns internal service error (http 500)

I'll get around to documenting them soon...
