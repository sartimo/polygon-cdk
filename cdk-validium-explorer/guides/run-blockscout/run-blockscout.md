# Run Blockscout in development

This document describes how to run the blockscout service in development in both `dev` and `prod` modes.

## Connect to the zkEVM network

You can connect blockscout to the zkEVM network in two different ways:

### Local zkEVM network

First, you need to clone the [zkevm-bridge-service](https://github.com/0xPolygonHermez/zkevm-bridge-service) repo.
Next, you need to add this `network` setting to the [docker-compose.yml](https://github.com/0xPolygonHermez/zkevm-bridge-service/blob/main/docker-compose.yml)
file and run the following commands on the root of the project:

1. `make build`
2. `make run`

After it's deployed, you just need to point blockscout to the local zkEVM node. To do it, you just need to set the set the `ETHEREUM_JSONRPC_HTTP_URL`
env var to `http://zkevm-node:8123`.

### Deployed zkEVM network

If you just want to connect to a deployed instance of the zkEVM network, you just need to set the `ETHEREUM_JSONRPC_HTTP_URL` to the URL of the RPC
of the network.

## Select the desired environment

Blockscout has an env var `MIX_ENV` that is defined in the [docker-compose.yml](../../docker/docker-compose.yml). Set its value to either `dev` or `prod`:

* `dev` will instruct Blockscout to run in dev mode. This includes a file watch mechanism that will reload the browser whenever a file changes.
* `prod` will instruct Blockscout to run in prod mode.

## Build the app

Before you run the app you will have to build it. We have 2 build flavors according to the value of the `MIX_ENV` env var.

Access the `docker` folder and run `make build-dev` for `dev` or `make build-prod` for `prod`.

## Run the app

Once the build is ready you can start the container with `make start-compose`. After about a minute it should be available at `http://localhost:4010`. Use `make stop-compose` to stop the container.
