Source of Truth:
- [WP Dev 1](https://developer.wordpress.org/block-editor/getting-started/tutorial/)
- [WP Dev 1](https://developer.wordpress.org/block-editor/getting-started/fundamentals/javascript-in-the-block-editor/)

A JavaScript Build Process is recommended for most cases when working with Javascript for the Block Editor. With a build process, you’ll be able to work with ESNext and JSX (among others) syntaxes and features in your code while producing code ready for the majority of the browsers.

@wordpress/scripts package abstracts these libraries away to standardize and simplify development, so you won’t need to handle the details for configuring webpack or babel. Check the [Get started with wp-scripts](https://developer.wordpress.org/block-editor/getting-started/devenv/get-started-with-wp-scripts/) intro guide.

With wp-scripts package you can use Javascript modules to distribute your code among different files and get a few bundled files at the end of the build process (see [example](https://github.com/WordPress/block-development-examples/tree/trunk/plugins/data-basics-59c8f8))


## Install 'wp-scripts'

``` npm instal @worpdpress/scripts --save-dev```

## Setup 

Commands that can be called to 'wp-scripts' or inserted in '/package.json' to ease:
```
"scripts": {
        "build": "wp-scripts build",
        "check-engines": "wp-scripts check-engines",
        "check-licenses": "wp-scripts check-licenses",
        "format": "wp-scripts format",
        "lint:css": "wp-scripts lint-style",
        "lint:js": "wp-scripts lint-js",
        "lint:md:docs": "wp-scripts lint-md-docs",
        "lint:pkg-json": "wp-scripts lint-pkg-json",
        "packages-update": "wp-scripts packages-update",
        "plugin-zip": "wp-scripts plugin-zip",
        "start": "wp-scripts start",
        "test:e2e": "wp-scripts test-e2e",
        "test:unit": "wp-scripts test-unit-js"
    }
```

more info about further setup, build and stard functions at  (JavaScript Build Setup tutorial)[https://github.com/WordPress/gutenberg/tree/HEAD/docs/how-to-guides/javascript/js-build-setup.md]