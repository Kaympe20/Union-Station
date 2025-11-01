# Union Station

A Calendar-like multimodal trip planner

[![Athena Award Badge](https://img.shields.io/endpoint?url=https%3A%2F%2Faward.athena.hackclub.com%2Fapi%2Fbadge)](https://award.athena.hackclub.com?utm_source=readme)
---
I made this project because on all of my trips, I generally use [The Transit App](https://transitapp.com/), and it doesn't always have reliable data of transfers, durations, and whether you can bring your bike on **with no way to override the info**. It also drains your battery like crazy when open. I wanted an app that addressed both of these, which is why Union Station is based on user-inputed data and creates static descriptions that don't require GPS.

I made this using SvelteKit for the framework, SveltyPicker for the calendar widget, JSON in cookies for storage, and Cloudflare Pages for hosting.

Making this, I really struggled to understand cross-page storage, and especially JSON parsing. I also started this project without knowing any kind of Svelte and learned my way through this as I went. Overall, I like this project, but want to completely revamp it with a different build in the future now that I know what I am doing with Svelte(Kit).

<details>
<summary>Development</summary>
  
# sv

Everything you need to build a Svelte project, powered by [`sv`](https://github.com/sveltejs/cli).

## Creating a project

If you're seeing this, you've probably already done this step. Congrats!

```sh
# create a new project in the current directory
npx sv create

# create a new project in my-app
npx sv create my-app
```

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```sh
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

To create a production version of your app:

```sh
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://svelte.dev/docs/kit/adapters) for your target environment.
</details>
