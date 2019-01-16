<p align="center"><img height="100" src="../assets/logo.svg" /></p>
<h1 align="center">EDGEMESH BROWSER</h1>

<p align="center">
  <img src="https://img.shields.io/badge/%20-browser-lightgrey.svg?&longCache=true&style=for-the-badge" alt="Browser" />
  <a href="https://www.npmjs.com/package/edgemesh">
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

The edge**mesh** browser installation method enables support for any website stack.  You just need to have access to your SSL secured web server in order to get started.

<br />

## Installation

1. Add the edge**mesh** [service worker](https://signal.edgeme.sh/service-worker.min.js) to the root of your website. Make sure its named `service-worker.min.js` and accessible from `https://your-site.com/service-worker.min.js.`
2. Include the edge**mesh** runtime in the `<head>` of your `index.html` (more on this below).
3. Verify your site on the edge**mesh** [portal](https://portal.edgemesh.com).

🚀 You're done!  Your website is now running edge**mesh**! You should start seeing performance metrics in the real-time portal as users visit your site.

## Instantiation

The easiest way to instantiate edge**mesh** is adding the following line of code to your `<head>` tag:

```html
<script
  type="text/javascript"
  href="https://signal.edgeme.sh/client.min.js"
  onload="window.edgemesh = new window.Edgemesh()">
</script>
```

But we can do a little better by adding `preconnect` and `prefetch` tags to stream-line things a bit.  At the top of your `<head>` tag among your other `<link>` tags put the following:

```html
<link rel="preconnect" href="https://signal.edgeme.sh" crossorigin />
<link rel="prefetch" as="script" href="/service-worker.min.js" />
```

What we are doing here is preconnecting to the edge**mesh** backplane and prefetching your service worker.  That way when the edge**mesh** runtime goes to do its work. it already has its resources.

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

```html
<script
  type="text/javascript"
  href="https://signal.edgeme.sh/client.min.js"
  onload="window.edgemesh = new window.Edgemesh({
    host: 'your.private.backplane',
    swPath: '/custom/subdirectory',
    optIn: true
})">
</script>
```

<br />

#### externalMount `boolean`

Prevent the edge**mesh** client from mounting its own service worker.  Useful for when you are using two service workers and need to import one into the other. See our [documentation](https://edgemesh.com/docs/getting-started/custom-sw) for more info.

```html
<script
  type="text/javascript"
  href="https://signal.edgeme.sh/client.min.js"
  onload="window.edgemesh = new window.Edgemesh({
    externalMount: true
})">
</script>
```

<br />

## Runtime Methods

The running edge**mesh** client is attached to the `window` object.  The runtime can be accessed through `window.edgemesh` in your application javascript or javascript console.  You can call any of the public methods listed below.  For instance, turn on the debug logging:

```javascript
window.edgemesh.debug(true)
// or just
edgemesh.debug(true)
```

> You need to make sure you are on the correct context in dev-tools to issue commands.  Edge**mesh** resides in the `top` context.

<br />

#### debug ( `boolean` )

Set the debug output.

<br />

#### devmode ( `boolean` )

Enable or disable developer mode.

While `devmode` is enabled, your browser will skip the Edgemesh cache and pull the requested assets directly from origin.  Note that this is only true for your browser, other clients will continue to be served cached responses from their local Edgemesh caches.

Once you are ready to commit your changes, call `edgemesh.devmode(false)` and refresh your site. Your changes will then be replicated out to the global cache.

> Enabling `devmode` is important if you are editing your files directly on the origin server without changing file names for each iteration.  It also allows you to incrementally update your cache as you work on your site.

<br />

#### optIn ()

Opts the current browser in to edge**mesh**. Used when `options.optIn` is set to `true`.

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
