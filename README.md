# Solid Requests

A small library that provides HTTP requests using the [Solid protocol](https://solidproject.org/TR/protocol).
Requests use the `Session` object of this [Solid-OIDC implementation](https://github.com/uvdsl/solid-oidc-client-browser) to make authenticated requests.
We use [axios](https://www.npmjs.com/package/axios) as the underlying HTTP client.
We use [n3](https://www.npmjs.com/package/n3) for parsing RDF and provide a simple helper function (`parseToN3`) for that.

## Add via npm

```sh
npm add --save @uvdsl/solid-requests
```

## Example Usage
See the [Solid-OIDC implementation](https://github.com/uvdsl/solid-oidc-client-browser) for authenticating a session with your WebID!

Get a resource ... 
```ts
 // have a session (or not, it is optional)
 const session = ...;
 // HTTP GET 
 const uri = "https://uvdsl.solid.aifb.kit.edu/profile/card#me"
 const http_response = await getResource(uri, session) // or omit session
 const http_body = http_response.data;
 const { store, prefixes } = await parseToN3(data, dataset);
 // use data ...
```

Create a new container ...
```ts
 // have a session (or not, it is optional)
 const session = ...;
 // HTTP POST to create a container (with a name via slug header) in /mydata/
 const uri = "https://your.solid.pod/mydata/"
 const name = "poposedContainerName"
 const http_response = await createContainer(uri, name, session) // or omit session
 const location = getLocationHeader(http_response)
 // use new container at that location ...
```