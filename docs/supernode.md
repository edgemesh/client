<p align="center"><img height="100" src="../assets/logo.svg" /></p>
<h1 align="center">EDGEMESH SUPERNODE</h1>

<p align="center">
  <a href="https://github.com/edgemesh/edgemesh/blob/master/docs/browser.md">
    <img src="https://img.shields.io/badge/%20-browser-7E57C2.svg?&longCache=true&style=for-the-badge" alt="Browser" />
  </a>
  <a href="https://github.com/edgemesh/edgemesh/blob/master/docs/node.md">
    <img src="https://img.shields.io/badge/%20-node-CB3837.svg?&longCache=true&style=for-the-badge" alt="NPM" />
  </a>
  <a href="https://github.com/edgemesh/edgemesh/blob/master/docs/wordpress.md">
    <img src="https://img.shields.io/badge/%20-wordpress-21759B.svg?&longCache=true&style=for-the-badge" alt="Wordpress" />
  </a>
  <img src="https://img.shields.io/badge/%20-supernode-lightgrey.svg?&longCache=true&style=for-the-badge" alt="Supernode" />
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

The edge**mesh** Supernode is a single binary that enables you to run server based edge acceleration peers. Supernodes are self discovering, and require no infrastructure changes to direct visitors to their cache updates.   

<br />

## Installation

Edgemesh is delivered via docker image and is hosted at `quay.io/edgemesh/supernode`. To start a new Supernode run the following command on your docker host:

```bash
$ docker run -d \
  --name supernode_000 \
  --mount source=emsn-000,target=/usr/local/etc/edgemesh \
  quay.io/edgemesh/supernode
```

This command will automatically create a volume named `emsn-000` and run a container named `supernode_000` that is connected to the public edge**mesh** backplane.

> A note on volumes:  every Supernode container needs to have its own volume attached.  Any time you change the `--name` option you should also change the `--mount source=` option as well.

<br />

## Configuration

The Supernode can be configured with the options listed in the next section.  They are set by defining environment variables for your container at start up.  Here is an example of mounting to a non default volume target:

```bash
$ docker run -d \
  --name supernode_001 \
  --mount source=emsn-001,target=/your/target \
  --env SUPERNODE_PATH=/your/target \
  quay.io/edgemesh/supernode
```

Here is an example of logging all errors to a file on your volume at your custom target:

```bash
$ docker run -d \
  --name supernode_000 \
  --mount source=emsn-000,target=/your/target \
  --env SUPERNODE_PATH=/your/target \
  --env SUPERNODE_OUTPUT_LOG=true \
  --env SUPERNODE_LOG_DIR=/your/target/log \
  --env SUPERNODE_LOG_LEVEL=ERROR \
  quay.io/edgemesh/supernode
```

<br />

## Configuration Options

The options listed below 

#### SUPERNODE_ORIGINS `*`

A Supernode can be configured to service only a selected list of registered origins. You must supply `SUPERNODE_API_KEY` as well to use this feature.  This feature is for business tier and above.

<br />

#### SUPERNODE_BACKPLANE `signal.edgeme.sh`

If you are an enterprise customer, you will need to use this options to connect to your dedicated edge**mesh** backplane.  You will know what to do with it and if not, contact your dedicated edge**mesh** engineer.

<br />

#### SUPERNODE_PATH `/usr/local/etc/edgemesh`

This is the location where Supernode will store its data.  The examples above show how to set the path to a custom volume target. 

> If you change this option, the backplane will discover your Supernode as a brand new instance and will start re-syncing content you may already have. 

<br />

#### SUPERNODE_API_KEY `XXX`

If you are an edge**mesh** partner, enterprise customer or pro customer, enter your API Key here.

<br />

#### SUPERNODE_DISK `All Available Disk`

How much disk in megabytes the Supernode instance is allowed to use.

<br />

#### SUPERNODE_MAX_PEERS `256`

The maximum number of peer connections the Supernode will hold open simultaneously.

<br />

#### SUPERNODE_DEBUG_LEVEL `WARNING`

The debug level for the stdout logger.  Valid log levels are:

 `DEBUG` `INFO`  `NOTICE` `WARNING` `ERROR` `CRITICAL` 

<br />

#### SUPERNODE_OUTPUT_LOG `false`

Setting to `true` will enable an output log file.

<br />

#### SUPERNODE_LOG_LEVEL `ERROR`

The log level for the file logger.  Valid log levels are:

 `DEBUG` `INFO`  `NOTICE` `WARNING` `ERROR` `CRITICAL`

<br />

#### SUPERNODE_LOG_DIR `/usr/local/etc/edgemesh/log`

Override the default log file directory.

<br />

#### `EXPERIMENTAL` SUPERNODE_HTTP_PORT `0`

Enables transparent HTTP proxy on specified port.

<br />

## Embedded Applications

If you have an embedded application with a use case for Supernode and you need it compiled for a specific architecture, we would love to hear from you!  Send us an email with a brief overview of what you are working on and one of our engineers will get in touch. 

[contact@edgemesh.com](mailto:contact@edgemesh.com) 

<br />

## Troubleshooting and Issues

If you discover any issues you can report them on our main repository [here](https://github.com/edgemesh/edgemesh/issues/new?template=supernode-bug-report.md), but first make sure your issue has not been solved already by checking our [closed issues](https://github.com/edgemesh/edgemesh/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aclosed).  You can also join our [discord](https://discord.gg/K5ACGha) to get community support and join the discussion to help shape the future of edge**mesh**.

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
