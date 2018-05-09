![NewBlueFX](img/NewBlueFX_logo.png)

This middleware enables you to override the default mime-type returned with any static resource served.

To override the default mappings, set a `mime` property in the stored config. The `mime` value should be a plain object containing a key for each MIME type you wish to override. The value of each key is a list of file extensions to apply the MIME type to. This value is passed directly to [mime.define()](https://github.com/broofa/node-mime#mimedefine). Example:

```js
module.exports = {
  mime: {
    'text/plain': [ 'php', 'pl' ]
  }
}
```
