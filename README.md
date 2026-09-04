# scm-js plugin API

Type declarations for the plugin API of [scmJS](https://github.com/scm-js/scm-js), the
browser-based StarCraft: Brood War map editor.

**Nothing here is written by hand.** `index.d.ts` is generated from `src/plugins/api.ts`
in the editor by `npm run build:plugin-types` and pushed here — one file, so a plugin
repository carries a dependency instead of a copy. `main` is the tip of the contract; a
`v*` tag is the contract as of that editor release, which is why the package's version
is the editor's.

## Using it

```sh
npm i -D github:scm-js/plugin-api
```

```ts
import type { PluginApi } from "@scm-js/plugin-api";

export function activate(api: PluginApi) {
  api.ui.toast("Hello from a plugin.");
}
```

Types only: a plugin imports them with `import type`, which is erased before the editor's
loader ever sees the specifier — which is what keeps this a normal npm dependency without
breaking the rule that a plugin's *runtime* code cannot import packages by name.

Pin it if you want to (`github:scm-js/plugin-api#v0.1.0`); most plugins do not need to.
`PLUGIN_API_VERSION` is 1 and additions do not move it, so the tip is compatible with
everything written against it so far. The shared plugin CI in
[`scm-js/.github`](https://github.com/scm-js/.github) type-checks each plugin against the
tip on a schedule, so drift turns a check red rather than going unnoticed.

## What the API covers

[`docs/plugins.md`](https://github.com/scm-js/scm-js/blob/main/docs/plugins.md) in the
editor is the author's guide and the tour of what a plugin can do; this repository is only
the typings for it.

MIT, like the editor.
