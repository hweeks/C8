# C8 RGB

## overview

1. concept
1. tech stack
1. architecture
1. ui/ux

## concept

i'd like to have RGB lights on my car, in multiple locations, that:

- are able to be controlled independently
- have a simple queue for using
- are simple to shut down
- are decoupled from LTE or mobile networks

## tech stack

the main idea is that we have:

- a website to interact with the rgb
- local server for controlling rgb

i see three seperate packages:

- frontend (react and bullshit)
- web backend (golang)
- RGB controller

## architecture

the web stack:

 ____________________
|   ____      ____   |
|  |    |    |    |  |
|  | fe |<-->| be |  |
|  |____|    |____|  |
|               ^    |
|               |    |
|             __v_   |
|            |    |  |
|            | lc |  |
|            |____|  |
|____________________|

fe: frontend
be: web golang server
lc: rgb controller

### frontend

this will allow:

- user selects a name
- user is dropped onto layout of corvette
- user can select a location and get
  - current number of folks waiting
  - current animation
  - current animation selectors name
- user can select an animation they'd like to see
- user is alerted when it's their turn
- animation plays

built on:

- react
- redux
- websockets
- some ui framework

### web golang server

this will allow:

- user registration
- websocket connection with browser
- websocket connection with [rgb controller](#rgb-controller)
- queue management

### rgb controller

this will allow:

- an authed connection from the server
- a websocket based message protocol
- a callback system on success or failure

## actual build

the idea here is:

rgb contorller attached to an arduino that auto connects to my wifi from my phone
once connected it alerts the web server it's online
single unit powers entire car, each panel is a seperate panel