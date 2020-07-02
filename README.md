# sapper-rollup-css-issue

The repo is a reproduction attempt of a CSS bundling issue in [sapper-template-rollup](https://github.com/sveltejs/sapper-template-rollup) when upgrading from rollup version 1 to 2. The issue summary can be seen in https://github.com/sveltejs/sapper-template/issues/233 and https://github.com/rollup/rollup/issues/3655. 

## Getting started


### Using [`degit`](https://github.com/Rich-Harris/degit) to get started

```bash
# for Rollup v1
npx degit "habibrosyad/sapper-rollup-css-issue#rollupv1" rollup-v1
# for Roolup v2
npx degit "habibrosyad/sapper-rollup-css-issue#rollupv2" rollup-v2
```

### Using `git` to get started
``` bash
git clone https://github.com/habibrosyad/sapper-rollup-css-issue

# go to the project repo dir
cd sapper-rollup-css-issue 

# for Rollup v1
git checkout rollupv1

# for Rollup v2
git checkout rollupv2
```

### Running the project

However you get the code, you can install dependencies and run the project in development mode with:

```bash
cd my-app
npm install # or yarn
npm run dev
```

Open up [localhost:3000](http://localhost:3000) and start clicking around.

### Spotting issue with rollup version 1 and version 2

_Please watch the CSS files generated in `__sapper__/dev/client/` directory._

With rollup version 1 you will most likely got several CSS files (the hash might be different than yours):
```
[slug].8afac42c.css
client.6bfaa544.css
index.7be4ff0d.css
index.9bb43f04.css
main.237455804.css
```

Whereas with rollup version 2 you will get only one CSS file containing everything:
```
main.2065939480.css
```

It is not ideal if some routes have conflicting styles with the others. In this repro it might be not too noticeable, but in a bigger project this behaviour might not be desired (I've experienced this in my own project). Previously you can load the only necessary CSSes required for the current route, while in the case with rollup 2 all of those CSS bundled together into a single file (no matther what route you're in).
