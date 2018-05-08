This example, a RESTful `/users` API, adds responses handling `PUT`, `DELETE` and `POST`.

```js
const users = [
  { id: 1, name: 'Lloyd', age: 40 },
  { id: 2, name: 'Mona', age: 34 },
  { id: 3, name: 'Francesco', age: 24 }
]

module.exports = MockBase => class MockUsers extends MockBase {
  mocks () {
    /* response mocks for /users */
    return [
      {
        route: '/users',
        responses: [
          /* Respond with 400 Bad Request for PUT and DELETE requests (inappropriate on a collection) */
          { request: { method: 'PUT' }, response: { status: 400 } },
          { request: { method: 'DELETE' }, response: { status: 400 } },
          {
            /* for GET requests return the collection */
            request: { method: 'GET' },
            response: { type: 'json', body: users }
          },
          {
            /* for POST requests, create a new user and return its location */
            request: { method: 'POST' },
            response: function (ctx) {
              const newUser = ctx.request.body
              users.push(newUser)
              newUser.id = users.length
              ctx.status = 201
              ctx.response.set('Location', `/users/${newUser.id}`)
            }
          }
        ]
      }
    ]
  }
}
```

Launch `ws` passing in your mocks module:

```sh
$ ws --mocks example-mocks.js
Serving at http://newbluefx.local:8000, http://127.0.0.1:8000, http://192.168.0.100:8000
```

Test your mock responses. A `POST` request should return a `201` with an empty body and the `Location` of the new resource.

```sh
$ curl http://127.0.0.1:8000/users -H 'Content-type: application/json' -d '{ "name": "Anthony" }' -i
HTTP/1.1 201 Created
Vary: Origin
Location: /users/4
Content-Type: text/plain; charset=utf-8
Content-Length: 7
Date: Wed, 28 Jun 2017 20:31:19 GMT
Connection: keep-alive

Created
```

A `GET` to `/users` should return our mock user data, including the record just added.

```sh
$ curl http://127.0.0.1:8000/users
[
  {
    "id": 1,
    "name": "Lloyd",
    "age": 40
  },
  {
    "id": 2,
    "name": "Mona",
    "age": 34
  },
  {
    "id": 3,
    "name": "Francesco",
    "age": 24
  },
  {
    "id": 4,
    "name": "Anthony"
  }
```

## /users/:id

An example mock module handling typical RESTful requests to the `/users/:id` resource.

```js
const users = [
  { "id": 1, "name": "Lloyd", "age": 40, "nationality": "English" },
  { "id": 2, "name": "Mona", "age": 34, "nationality": "Palestinian" },
  { "id": 3, "name": "Francesco", "age": 24, "nationality": "Italian" }
]

module.exports = MockBase => class MockUsers extends MockBase {
  mocks () {
    return [
      {
        route: "/users/:id",
        responses: [
          /* no support for POST on this route */
          { request: { method: 'POST' }, response: { status: 400 } },

          /* for GET requests, return a particular user */
          {
            request: { method: 'GET' },
            response: (ctx, id) => {
              ctx.body = users.find(user => user.id === Number(id))
            }
          },

          /* for PUT requests, update the record */
          {
            request: { method: 'PUT', is: 'json' },
            response: (ctx, id) => {
              const updatedUser = ctx.request.body
              const existingUserIndex = users.findIndex(user => user.id === Number(id))
              users.splice(existingUserIndex, 1, updatedUser)
              ctx.status = 204
            }
          },

          /* DELETE request: remove the record */
          {
            request: { method: 'DELETE' },
            response: (ctx, id) => {
              const existingUserIndex = users.findIndex(user => user.id === Number(id))
              users.splice(existingUserIndex, 1)
              ctx.status = 204
            }
          }
        ]
      }
    ]
  }
}
```