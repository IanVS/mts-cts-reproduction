This is an exploration of the use of TypeScript `.cts` and `.mts` files, and how they 
influence TypeScript module resolution when importing from a node_modules package using 
an `"exports"` map in its package.json.

I'm finding that TypeScript is using ESM mode with an `"import"` condition to resolve
imports in both `src.cts` and `src.mts`, which results in their definition files being
the same.

I expected `src.d.cts` to use the `require` condition, and wind up with `cjs` in the definition.

To make matters even stranger, VSCode intellisense shows `"cjs"` for both files, 
whereas tsc generates definitions showing `"esm"`.

Run the following to see the module resolution trace:

```
npm install
npm run generate-export-types
```


Here's part of the resolution trace:

```
======== Resolving module 'exports' from '/Users/ianvs/example/src/NodeNext/test/foo.cts'. ========
Explicitly specified module resolution kind: 'NodeNext'.
Resolving in ESM mode with conditions 'node', 'import', 'types'.
```
