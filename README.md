# npm Workspaces Bug

npm does not update the `package.lock` when changing the dependencies of a workspace package.

To reproduce:

1. Use npm@7: `npm i -g npm@next-7`
1. `npm install`
1. Open `package-lock.json`
1. Search for `lodash` and find no mention of it.
1. Manually add `"lodash": "4.17.20"` to the `dependencies` of `packages/a/package.json`
1. `npm install`
1. Open `package-lock.json`
1. Search for `lodash` and find no mention of it.

In fact if you change the version of `once` used in `packages/a/package.json` and run `npm install` that will also be ignored.

Changing dependencies in the "root" `package.json` will work as normal.