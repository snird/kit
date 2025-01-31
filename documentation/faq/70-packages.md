---
question: How do I fix the error I'm getting trying to include a package?
---

Most of these issues come from Vite trying to deal with non-ESM libraries. You may find it helpful to search for your error message in [the Vite issue tracker](https://github.com/vitejs/vite/issues). 

The most common solutions would be to try moving the package between `dependencies` and `devDependencies` or trying to `include` or `exclude` it in `optimizeDeps`. SvelteKit currently asks Vite to bundle all your `dependencies` for easier deployment to serverless environment. This means that by moving a dependency to `devDependencies` Vite is no longer asked to bundle it. This may sidestep issues Vite encounters in trying to bundle certain libraries. Avoiding Vite bundling especially works for `adapter-node` and `adapter-static` where the bundling isn't necessary since you're not running in a serverless environment. We are considering [better alternatives](https://github.com/sveltejs/kit/issues/1016) to make this setup easier.

Packages which use `exports` instead of `module.exports` are currently failing due to a [known Vite issue](https://github.com/vitejs/vite/issues/2579). You should also consider asking the library author to distribute an ESM version of their package or even converting the source for the package entirely to ESM.

You should also add any Svelte components to `ssr.noExternal`. [We hope to do this automatically in the future](https://github.com/sveltejs/kit/issues/904).
