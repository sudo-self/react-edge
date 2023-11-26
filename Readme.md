# React on the Edge

[`sveltekit-on-the-edge`](https://sveltekit-on-the-edge.vercel.app/) but on top of React. It uses `esbuild` for bundling and [Vercel Edge Functions](https://vercel.com/edge) for SSR.

Run `pnpm i` then:

- To build: `pnpm build`
- To run a local server: `pnpm start`

To build this demo with streaming (`renderToStream`) instead of `renderToString` run `USE_STREAMS=1 pnpm build`.
After building, `.vercel/output` will be created which you can deploy via `vc --prebuilt`.



- `util/build.mjs` implements the build process on top of `esbuild` that bundles `src/app` into an Edge Function.
- `util/start.mjs` implements a local server using the `edge-runtime` package that can locally run the build outputs.


Due to the absence of a dev server, [`watchexec`](https://github.com/watchexec/watchexec) can be used as a replacement. Use `brew install watchexec` to install.

```bash
watchexec -c -r --no-meta 'node util/build.mjs; node util/start.mjs'
```
