# @scm-js/plugin-api

Type declarations for the plugin API of [scmJS](https://github.com/scm-js/scm-js), the
browser-based StarCraft: Brood War map editor.

```sh
npm i -D @scm-js/plugin-api
```

```ts
import type { PluginApi } from "@scm-js/plugin-api";

export function activate(api: PluginApi) {
  api.ui.toast({ title: "Hello from a plugin." });
}
```

The package has types only. Import them with `import type`. TypeScript removes those imports
before the editor's loader sees the plugin, so it can be an ordinary npm dependency. A
plugin's run-time code cannot import packages by name, and everything it needs at run time
arrives on `api`.

## Where to start

- [Plugins](https://docs.scmjs.dev/plugins/) is the author's guide: what a plugin can do and
  how to write, load and publish one.
- The [API reference](https://docs.scmjs.dev/api/) lists every call, generated from these
  declarations.
- [plugin-hello-world](https://github.com/scm-js/plugin-hello-world) is the smallest working
  plugin.

## Versions

The package's major version is `PLUGIN_API_VERSION`, which is 1 and has never changed. Write
`"^1"` as the range. The minor version moves whenever the declarations change. A change that
would break a plugin would move the major version and `PLUGIN_API_VERSION` together.

The editor's own version is not used here. Going from editor 0.1.0 to 0.2.0 is an ordinary
release, and semver would read it as a break.

Your manifest's `"api": 1` is the version your plugin needs. An editor that provides an
older one will not load it.

## This repository

Only this README and the LICENSE are written by hand. `index.d.ts` and `package.json` are
generated from `src/plugins/api.ts` in the editor by `npm run build:plugin-types`, and
published from there. `main` is the newest version, and each `v*` tag is a published one.

The repository is the record behind each npm release. It is also a way to install the
package without the npm registry:

```sh
npm i -D github:scm-js/plugin-api#v1.64.0
```

That installs the same files as the registry.

MIT, like the editor.
