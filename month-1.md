## Background

Over the course of several months we’re gonna put together a super basic site (e.g. Twitter or Reddit clone). However we’re gonna go deep in each stage of the process to better understand the tradeoffs with every decision you make when standing up a service like this. 

The very first things we’re going to do is just stand up a basic Hello World web server. Get it running and accepting requests while running in a docker container.

## The Web Server

We want a web server that responds to the following requests

`GET /hello`

Returns a 200 status code with the response body: “Hello World”

`GET /echo?text=Blah`

Returns a 200 status code with a response body that matches the “text” param exactly

`POST /incr`

Increments an in memory counter and returns a 2xx code with the output of incrementing that counter. The first time the POST request is made, the response body should be “1”. The second time it should return “2”, etc. If the server is restarted, it’s fine that the counter resets (aka just do it in memory)

`GET /boom`

The code should throw an exception / panic. Basically this is the “server code exploded” scenario. The actual response should be a 500 status code and the server shouldn’t totally crash.

## Docker

So that we can easily switch between projects without configuring each of our machines to work across different languages / environments, we’re going to containerize all our projects using Docker. 

If you’re new to Docker, you can install Docker Desktop which gets you everything you need. To make local setup and development easier, we’ll user docker compose to help run stuff in docker. https://docs.docker.com/compose/gettingstarted/ has a pretty good example

From a fresh pull of your repo (and assuming the machine has docker compose installed)

`docker-compose up`

Should be the only command you need to build and run your server.

