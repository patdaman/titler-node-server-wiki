Config files are plain Javascript, giving you freedom to share and merge options however you like.

The config file accepts all options listed by `ws --help` except they should be written in "camel case". For example, the `--no-conditional-get` CLI option should be written `noConditionalGet` in the config file, `--cors.allow-methods` becomes `corsAllowMethods` etc.

The config file (`config.js` by default) should look something like this:

```js
module.exports = {
  rewrite: [
    {
      from: '/resources/*',
      to: 'http://remote-api.org:8080/resources/$1'
    }
  ],
  directory: 'src',
  logFormat: 'stats'
}
```

An example of how you might share and merge options:

```js
/* pull options from the env */
const remoteAPI = process.env.REMOTE_API

/* .. or an installed package */
const sharedOptions = require('shared-options')

/* merge them to taste */
const options = Object.assign({}, sharedOptions, {
  rewrite: [
    {
      from: '/resources/*',
      to: `http://${remoteAPI}/resources/$1`
    }
  ]
})

module.exports = options
```

To inspect the active config (merged from all sources) at any point, run:
```sh
$ ws --config
```

To use a config file other than the default, run: 

```
$ ws --config-file something.js
```
