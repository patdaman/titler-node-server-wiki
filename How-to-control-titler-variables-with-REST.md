[![NewBlueFX](img/NewBlueFX_logo.png)](Home.md)

## Titler Live REST Connection

Full CRUD is available for Titler Live.

_No alerts are sent to client from server via REST, must make GET call for updated value or use Websockets_

```js
        route: "/variables/",
        responses: [
          /* no support for POST on this route */
          { request: { method: 'POST', is: 'json' },             
            response: (ctx, id) => {
              const updatedVariable = ctx.request.body
              const existingVariableIndex = users.findIndex(variable => variable.id === Number(id))
              variables.splice(existingVariableIndex, 1, updatedVariable)
              ctx.status = 204; 
            } 
          },

          /* for GET requests, return all variables */
          {
            request: { method: 'GET' },
            response: (ctx) => {
              ctx.body = variables;
            }
          },

        route: "/variables/:id",
        responses: [
          /* no support for POST on this route */
          { request: { method: 'POST' }, response: { status: 400 } },

          /* for GET requests, return a particular variable */
          {
            request: { method: 'GET' },
            response: (ctx, id) => {
              ctx.body = variables.find(variable => variable.id === Number(id));
            }
          },

          /* for PUT requests, update the record */
          {
            request: { method: 'PUT', is: 'json' },
            response: (ctx, id) => {
              const updatedVariable = ctx.request.body
              const existingVariableIndex = users.findIndex(variable => variable.id === Number(id))
              variables.splice(existingVariableIndex, 1, updatedVariable)
              ctx.status = 204
            }
          },

          /* DELETE request: set the variable to null or default */
          {
            request: { method: 'DELETE' },
            response: (ctx, id) => {
              const existingVariableIndex = variables.findIndex(variable => variable.id === Number(id))
              variables.splice(existingVariableIndex, 1)
              ctx.status = 204
            }
          }
        ]
```
