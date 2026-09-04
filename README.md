# @scm-js/plugin-api

Type declarations for the plugin API of [scmJS](https://github.com/scm-js/scm-js), the
browser-based StarCraft: Brood War map editor.

```sh
npm i -D @scm-js/plugin-api
```

```ts
import type { PluginApi } from "@scm-js/plugin-api";

export function activate(api: PluginApi) {
  api.ui.toast("Hello from a plugin.");
}
```

Types only. A plugin imports them with `import type`, which is erased before the editor's
loader ever sees the specifier — which is what lets this be a normal npm dependency
without breaking the rule that a plugin's *runtime* code cannot import packages by name.

## Versions

The major **is** `PLUGIN_API_VERSION`, so `"^1"` is the range to write and it means what
it says: the minor moves whenever the declarations change, and a change that would break a
plugin moves the major and `PLUGIN_API_VERSION` together. The editor's own version is
deliberately not in here — editor 0.1.0 to 0.2.0 is an ordinary release, and semver would
read it as a break.

`PLUGIN_API_VERSION` is 1 and has never moved. Your manifest's `"api": 1` is the version
your plugin *needs*; an editor providing an older one refuses to load it.

## This repository

**Nothing here is written by hand** except this README and the LICENSE. `index.d.ts` and
`package.json` are generated from `src/plugins/api.ts` in the editor by
`npm run build:plugin-types` and published from there, so the contract has one source and
one copy of its declarations. `main` is the tip; each `v*` tag is a published version.

It exists beside the registry as the audit trail behind the tarball, and as the way in for
anyone whose registry the package is not on — `npm i -D github:scm-js/plugin-api#v1.0.0`
works and installs exactly the same two files.

## What the API covers

[`docs/plugins.md`](https://github.com/scm-js/scm-js/blob/main/docs/plugins.md) in the
editor is the author's guide and the tour of what a plugin can do; this repository is only
the typings for it. [`plugin-hello-world`](https://github.com/scm-js/plugin-hello-world) is
the smallest working example.

MIT, like the editor.
