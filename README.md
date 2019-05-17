# [Next.js](https://github.com/zeit/next.js) IE11 syntax error reproduction

> See the original issue here: [zeit/next.js#3330](https://github.com/zeit/next.js/issues/3330)

When running `next dev` command (alias `next`), babel is not transpiling some specific arrow functions, causing a `Syntax error` on any browser which does not implement arrow functions.

It is important to note that it does not occur when we run `next build` followed by `next start`

The lines of code which are not transpiling on a fresh install of Next.js are these:

`node_modules/next/node_modules/strip-ansi/index.js:4`:
```
module.exports = input => typeof input === 'string' ? input.replace(ansiRegex(), '') : input;
```

`node_modules/next/node_modules/ansi-regex/index.js:3`:
```
module.exports = () => {
		'(?:(?:\\d{1,4}(?:;\\d{0,4})*)?[\\dA-PRZcf-ntqry=><~]))'
```

## Workaround

In case you have to test IE11 on development, simply run `next build` and then `next start`.
