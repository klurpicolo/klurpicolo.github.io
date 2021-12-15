---
layout: post
title:  "Protocals(Sort of) that backends should know"
date:   2021-12-15 22:00:00 +0700
categories: misc
---

# RESTful APIs (Just a HTTP)
- It's actually "software architectural style" that introduce by Roy Fielding not a protocal
- Simple CRUD API that build on top of HTTP protocal that try to match CRUD operation with HTTP verb
- Since it's build on top of HTTP, so it only supports request-response communication
- Data format usually be JSON, but sometimes XML(rarely)
- OpenAPI is the specifiation defind RESTful APIs, Swagger is a tool for imeplementing OpenAPI
- RESTful APIs isn't defined how to do authentiation and authorization.
- **Pros** : Simeple, Lot of example, Mature
- **Cons** : Let see later...
- **Usecases** :
  - Normal CURD operation
  - Server to server compunication

# Websocket
- It's protocal at OSI layer 7 works over TCP
- It's stateful constrat to HTTP which is stateless
- Full duplex communication
- No Header support. Need sub protocal for real application useage
- STOMP messaging protocal is commonly use on top of Websocket for actual usage
- **Pros** : Can send realtime message initiated from server
- **Cons** : Since it's stateful, It's hard to scale horizontally
- **Usecases** :
  - Realtime chat
  - Server push update notification

# GraphQL
- It's application protoacal built on top of HTTP/2
- Client able to conastruct query to get desired data response
- **Pros** : Client can just ask for what it needs, Reduce network useages
- **Cons** : Sever need to implement additional logic to support GraphQL, Steep learning curve compare to Simple RESTful
- **Usecases** :
  - Realtime chat
  - Server push update notification

# gRPC
- It's application protoacal built on top of HTTP/2
- Protobuf(Protocol Buffers) is used for de/serialization which is binanry format
- Client can call server method with arguments same as native function
- More efficient
- It doesn't work with web broswer
- **Pros** : Very efficient, Don't need to worry about HTTP stuff(eg verb)
- **Cons** : Lack of community, Harder to debug compare to plain HTTP, Steep learning curve compare to plain HTTP
- **Usecases** :
  - Same as RESTful APIs but for server to server only

# Rsocket
- It's protocal at layer 5 and 6
- It supports many type of communication model, Request/response, Request/stream, Fire-and-forget and Channel
- Fully implement Reactive stream
- **Pros** : Very efficient, Built-in flow control(eg back pressure)
- **Cons** : Lack of community, Steep learning curve compare to HTTP
- **Usecases** :
  - Same as RESTful APIs but for server to server only
