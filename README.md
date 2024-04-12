# Random User Agent

This is an adapted version of [rand-user-agent by WebScrapingAPI](https://www.npmjs.com/package/rand-user-agent) specifically designed for environments lacking access to server file systems (fs), such as Cloudflare Workers.

## Installation

Run the following command in the main folder of your project:

```shell
# Using npm
npm i @ivanmatthew/rand-user-agent-cjs

# Using pnpm
pnpm add @ivanmatthew/rand-user-agent-cjs

# Using yarn
yarn add @ivanmatthew/rand-user-agent-cjs
```

## Usage Example 

```js
import { randUA } from "@ivanmatthew/rand-user-agent-cjs";

// ...

const agent = randUA("desktop");

console.log(agent);
```

You can also provide a browser and an operating system in the parameters of randUA in order to filter out the user agents:

```js
import { randUA } from "@ivanmatthew/rand-user-agent-cjs";

// ...

const agent = randUA("desktop", "chrome", "linux");

console.log(agent);
```
