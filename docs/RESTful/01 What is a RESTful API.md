# What is a RESTful API

## The Six Guiding Principles of REST

1. Uniform Interface
2. Client-Server
3. Stateless
4. Cacheable
5. Layered System
6. Code on Demand

### Uniform Interface

- **Identification of resources** – The interface must uniquely identify each resource involved in the interaction
  between the client and the server.

- **Manipulation of resources through representations** – The resources should have uniform representations in the
  server response. API consumers should use these representations to modify the resource state in the server.

- **Self-descriptive messages** – Each resource representation should carry enough information to describe how to
  process the message. It should also provide information of the additional actions that the client can perform on the resource.

- **Hypermedia as the engine of application state** – The client should have only the initial URI of the application.
  The client application should dynamically drive all other resources and interactions with the use of hyperlinks.
