![Serve-Authed Logo](https://raw.githubusercontent.com/F/serve-authed/main/media/banner.png)

<div align="center">
  <a aria-label="Fork of Vercel's serve" href="https://github.com/vercel/serve">
    <img src="https://img.shields.io/badge/forked%20from-vercel%2Fserve-%23000000">
  </a>
  <br>
  <a aria-label="Install Size" href="https://packagephobia.com/result?p=serve-authed">
    <img src="https://packagephobia.com/badge?p=serve-authed">
  </a>
  <a aria-label="Stars" href="https://github.com/Alex-Kaff/serve-authed/stargazers">
    <img src="https://img.shields.io/github/stars/Alex-Kaff/serve-authed">
  </a>
  <a aria-label="Build Status" href="https://github.com/Alex-Kaff/serve-authed/actions/workflows/ci.yaml">
    <img src="https://github.com/Alex-Kaff/serve-authed/actions/workflows/ci.yaml/badge.svg">
  </a>
</div>

---

`serve-authed` helps you serve a static site, single page application or just a static file (no matter if on your device or on the local network) with optional authentication support. It also provides a neat interface for listing the directory's contents:

![Listing UI](https://raw.githubusercontent.com/Alex-Kaff/serve-authed/main/media/listing-ui.png)

> Once it's time to push your site to production, we recommend using [Vercel](https://vercel.com).

> **Note:** This is a fork of the original [serve](https://github.com/vercel/serve) package by Vercel, with added authentication capabilities.

## Usage

> `serve-authed` v14 onwards requires Node v14 to run. Please use `serve-authed` v13 if you cannot upgrade to Node v14.

The quickest way to get started is to just run `npx serve-authed` in your project's directory.

If you prefer, you can also install the package globally (you'll need at least [Node LTS](https://github.com/nodejs/Release#release-schedule)):

```bash
> npm install --global serve-authed
```

Once that's done, you can run this command inside your project's directory...

```bash
> serve-authed
```

...or specify which folder you want to serve:

```bash
> serve-authed folder-name/
```

Finally, run this command to see a list of all available options:

```bash
> serve-authed --help
```

Now you understand how the package works! :tada:

## Authentication

`serve-authed` supports optional token-based authentication to protect your files. When enabled, all requests must include a valid authentication token.

### Basic Usage

To enable authentication, use the `--token` (or `-t`) flag:

```bash
> serve-authed --token YOUR_SECRET_TOKEN
```

### Providing the Token

Clients can authenticate using one of two methods:

1. **Authorization Header** (recommended):

```bash
curl -H "Authorization: YOUR_SECRET_TOKEN" http://localhost:3000
# or with Bearer prefix
curl -H "Authorization: Bearer YOUR_SECRET_TOKEN" http://localhost:3000
```

2. **Query Parameter**:

```bash
curl http://localhost:3000?authentication=YOUR_SECRET_TOKEN
```

### Example

```bash
# Start server with authentication
> serve-authed --token mySecretToken123

# Access from browser or API client
curl -H "Authorization: Bearer mySecretToken123" http://localhost:3000/index.html
```

Unauthenticated requests will receive a `403 Forbidden` response.

## Configuration

To customize `serve-authed`'s behavior, create a `serve.json` file in the public folder and insert any of [these properties](https://github.com/vercel/serve-handler#options).

## API

The core of `serve-authed` is [`serve-handler`](https://github.com/vercel/serve-handler), which can be used as middleware in existing HTTP servers:

```js
const handler = require('serve-handler');
const http = require('http');

const server = http.createServer((request, response) => {
  // You pass two more arguments for config and middleware
  // More details here: https://github.com/vercel/serve-handler#options
  return handler(request, response);
});

server.listen(3000, () => {
  console.log('Running at http://localhost:3000');
});
```

> You can also replace `http.createServer` with [`micro`](https://github.com/vercel/micro).

## Issues and Contributing

If you want a feature to be added, or wish to report a bug, please open an issue [here](https://github.com/Alex-Kaff/serve-authed/issues/new).

If you wish to contribute to the project, please read the [contributing guide](contributing.md) first.

## Credits

This project is a fork of the original [serve](https://github.com/vercel/serve) package by Vercel.

The original project used to be called `list` and `micro-list`. But thanks to [TJ Holowaychuk](https://github.com/tj) handing the name to Vercel, it's now called `serve` (which is much more definite).

## Original Author

Leo Lamprecht ([@leo](https://x.com/leo))
