---
title: "API (Application Programming Interface)"
date: 2021-05-27
draft: false
layout: default
parent: Government procurement
---

## API (Application Programming Interface)

All interfaces that are implemented should be implemented with either one of the following tech: 

- Restful JSON following the json:api standard [https://jsonapi.org/]. 
- GraphQL following the best practice at [https://graphql.org/learn/best-practices/]. 
- Websockets

A SOAP service is not accepted as a viable API (Application Programming Interface). Neither are a simple XML formatted response. 

## API Coverage

API's delivered as a response to a public procurement of Helsingborg Stad should enable developers to perform all actions avabile for a native user of the application in every avabile role. 

## API Authentication

- Generic Token
- OpenAuth
- JWT token
- Client Side Certificate (for systems with a high security grade)

## API Authorization

An authorization policy should be implemented for the api implementation and that clearly regulates avabile routes. 

## Error resposes & error handling

### Response headers


# API standards document reference

https://github.com/18F/api-standards 

