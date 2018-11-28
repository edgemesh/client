<p align="center"><img height="100" src="../assets/logo.svg" /></p>
<h1 align="center">EDGEMESH NODE</h1>

<p align="center">
  <a href="https://github.com/edgemesh/edgemesh/blob/master/docs/browser.md">
    <img src="https://img.shields.io/badge/%20-browser-7E57C2.svg?&longCache=true&style=for-the-badge" alt="Browser" />
  </a>
  <a href="https://npmjs.org/package/edgemesh">
    <img src="https://img.shields.io/badge/%20-npm-CB3837.svg?&longCache=true&style=for-the-badge" alt="NPM" />
  </a>
  <a href="https://github.com/edgemesh/edgemesh/blob/master/docs/wordpress.md">
    <img src="https://img.shields.io/badge/%20-wordpress-21759B.svg?&longCache=true&style=for-the-badge" alt="Wordpress" />
  </a>
  <a href="https://github.com/edgemesh/edgemesh/blob/master/docs/supernode.md">
    <img src="https://img.shields.io/badge/%20-supernode-yellow.svg?&longCache=true&style=for-the-badge" alt="Supernode" />
  </a>
</p>

<p align="center">
  <a href="https://edgemesh.com/docs">
    <img src="https://img.shields.io/badge/%20-docs-orange.svg?&longCache=true&style=for-the-badge" alt="Docs" />
  </a>
  <a href="https://discord.gg/K5ACGha">
    <img src="https://img.shields.io/badge/%20-discord-7289DA.svg?&longCache=true&style=for-the-badge" alt="Discord" />
  </a>
  <a href="https://github.com/orgs/edgemesh/projects/8">
    <img src="https://img.shields.io/badge/%20-roadmap-green.svg?&longCache=true&style=for-the-badge" alt="Roadmap" />
  </a>
</p>

<br />

This node module is designed for use with the browser only.  If you want a server side solution, check out the edge**mesh** [Supernode](https://github.com/edgemesh/edgemesh/blob/master/docs/supernode.md). Otherwise, if you are using an app bundler like [Webpack](https://webpack.js.org) or module bundlers like [Browserify](http://browserify.org/) and [Rollup](https://rollupjs.org/) then this module is for you.  

<br />

## Installation

`yarn add edgemesh` or `npm i edgemesh --save`

<br />

## Instantiation

#### ES5

```javascript
require('edgemesh')()
```

#### ES6

```javascript
import Edgemesh from 'edgemesh'
const edgemesh = new Edgemesh()
```

<br />

## Configuration Options

There are only three configuration options for edge**mesh**.  In most cases you will not need to use them and the above instantiation is enough.  

<br />

#### host `string`

If you are an enterprise customer, you will need to use these options to connect to your dedicated edge**mesh** backplane.

<br />

#### swPath `string`

If you want to accelerate content for only one subdirectory and its children, add your [service worker]() to that directory and set the `swPath` option.  

> For example: setting `swPath` to `/app` would accelerate content for `/app/**` but not `/` or `/store`.

<br />

#### optIn `boolean`

Change edge**mesh** from `opt-out` mode to `opt-in` mode.  The edge**mesh** client will remain disabled until `edgemesh.optIn()` is called.

```javascript
const edgemesh = new Edgemesh({
    host: 'your.private.backplane',
    swPath: '/custom/subdirectory',
    optIn: true
})
```

<br />

## Runtime Methods

Once edge**mesh** installs, the running edge**mesh** client is attached to `window.edgemesh`.  This module itself exports an event emitter that emits a `ready` event when edge**mesh** has loaded.  It passes back a reference to the running edge**mesh** client.  You can use it to call any of the public methods listed below.  For instance, set the debug parameter when edge**mesh** loads:

```javascript
const em = new Edgemesh()
em.on(ready, edgemesh => {
    edgemesh.debug(true)
})
```

You need to make sure you are on the correct context in dev-tools to issue commands.  Edge**mesh** resides in the `top` context.

<br />

#### debug ( `boolean` )

Set the debug output.

<br />

#### devmode ( `boolean` )

Enable or disable developer mode.

> Developer mode turns off edge**mesh** for your local browser.  If you edit files directly on your live server (Wordpress or another CMS), you might want to consider enabling `devmode` until you have your changes finalized.  This will prevent incomplete changes from getting replicated on the network.  This way you don't have to purge your cache.

<br />

#### optIn ()

Opts current browser in to edge**mesh**. Used when `options.optIn` is set to `true`.

<br />

#### optOut ()

Opts current browser out of edge**mesh**. Used when `options.optIn` is set to `false`.

<br />

#### event(`object`)

Log a custom event to correlate with performance metrics.  The event is displayed in the edge**mesh** portal so you can see how page performance affects various aspects of your online business (product sales, signup conversion, etc).

The event method takes an object as its only argument:

| Parameter | Type   | Description                                                  |
| --------- | ------ | ------------------------------------------------------------ |
| UID       | String | Unique ID for event, could be a uuid, order number etc.      |
| type      | String | Type of the event, could be `signup`, `sale`, etc.           |
| name      | String | Arbitrary name associated with the event, could be a product name or user name, etc. |
| value     | String | Arbitrary value tied to event, could be an email, price etc  |

Results are aggregated in the `portal` by type and `name` fields. Here is an example of an event for a product being sold:

```javascript
edgemesh.event({
    UID: '#4321231',
    type: 'sale',
    name: 'Purple Shirt - SKU: 232334 ',
    value: '39.99'
})
```

<br />

#### clear()

Clears the edge**mesh** client cache. This method is useful for forcing a revalidation on the edge**mesh** backplane.

<br />

#### disable()

Disables the edge**mesh** client.  This method will unmount the service worker and prevent all edge**cache**, edge**secure** and edge**route** products from functioning.

<br />

#### enable()

Enables the edge**mesh** client.  This method re-registers the service worker and enables all edge**cache**, edge**secure** and edge**route** products.

<br />

## Troubleshooting and Issues

If you discover any issues you can report them on our main repository [here](https://github.com/edgemesh/edgemesh/issues/new?template=edge-bug-report.md), but first make sure your issue has not been solved already by checking our [closed issues](https://github.com/edgemesh/edgemesh/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aclosed).  You can also join our [discord](https://discord.gg/K5ACGha) to get community support and join the discussion to help shape the future of edge**mesh**.

<br />
<br />
<br />

<p align="center">
  <a href="https://github.com/standard/standard">
    <img src="https://cdn.rawgit.com/standard/standard/master/badge.svg" alt="JavaScript Style Guide" />
  </a>
</p>
<p align="center">
  <a href="https://github.com/edgemesh/edgemesh/releases">
    <img src="https://img.shields.io/github/release/edgemesh/edgemesh.svg?&longCache=true&style=for-the-badge" alt="Version" />
  </a>
  <a href="LICENSE.md">
    <img src="https://img.shields.io/badge/license-mpl--2.0-orange.svg?&longCache=true&style=for-the-badge" alt="License" />
  </a>
</p>
