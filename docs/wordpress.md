<p align="center"><img height="100" src="../assets/logo.svg" /></p>
<h1 align="center">EDGEMESH WORDPRESS</h1>

<p align="center">
  <a href="https://github.com/edgemesh/edgemesh/blob/master/docs/browser.md">
    <img src="https://img.shields.io/badge/%20-browser-7E57C2.svg?&longCache=true&style=for-the-badge" alt="Browser" />
  </a>
  <a href="https://github.com/edgemesh/edgemesh/blob/master/docs/node.md">
    <img src="https://img.shields.io/badge/%20-node-CB3837.svg?&longCache=true&style=for-the-badge" alt="NPM" />
  </a>
  <img src="https://img.shields.io/badge/%20-wordpress-lightgrey.svg?&longCache=true&style=for-the-badge" alt="Wordpress" />
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

This plugin provides full edge**mesh** support for the Wordpress platform.  It exposes a configuration page in the Wordpress admin area to add configuration options. The plugin is delivered ad hoc through our [releases]().

<br />

## Installation

1. Download the latest [release](https://github.com/edgemesh/edgemesh/releases/latest).
2. Upload `edgemesh-wordpress-plugin.zip` to your wp-admin [(instructions)](https://codex.wordpress.org/Managing_Plugins).
3. Activate the plugin.
4. Verify your origin on our [portal](https://portal.edgemesh.com).

🚀 Thats it! Edge**mesh** is now enabled on your Wordpress site.  Deactivating or removing the plugin will remove edge**mesh** from your site.

<br />

## Configuration Options

The plugin is configured through `settings > edgemesh` in your Wordpress admin area. In most cases you will not need to touch these settings.

<br />

#### host `string`

If you are an enterprise customer, you will need to use these options to connect to your dedicated edge**mesh** backplane.

<br />

#### optIn `boolean`

Change edge**mesh** from `opt-out` mode to `opt-in` mode.  The edge**mesh** client will remain disabled until `edgemesh.optIn()` is called.  This will require you to add a dialog in your theme to prompt the user and decide wether or not to call `edgemesh.optIn()`.

<br />

## Runtime Methods

The running edge**mesh** client is attached to the `window` object.  The runtime can be accessed through `window.edgemesh` in your theme javascript or javascript console.  You can call any of the public methods listed below.  For instance, turn on the debug logging:

```javascript
window.edgemesh.debug(true)
```

You need to make sure you are on the correct context in dev-tools to issue commands.  Edge**mesh** resides in the `top` context.

<br />

#### debug ( `boolean` )

Set the debug output.

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
