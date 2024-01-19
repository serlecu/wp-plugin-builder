Source of Truth:
- [WP Dev 1](https://developer.wordpress.org/block-editor/getting-started/tutorial/)
- [WP Dev 1](https://developer.wordpress.org/block-editor/getting-started/fundamentals/javascript-in-the-block-editor/)

A JavaScript Build Process is recommended for most cases when working with Javascript for the Block Editor. With a build process, you’ll be able to work with ESNext and JSX (among others) syntaxes and features in your code while producing code ready for the majority of the browsers.

`@wordpress/scripts` package abstracts these libraries away to standardize and simplify development, so you won’t need to handle the details for configuring webpack or babel. Check the [Get started with wp-scripts](https://developer.wordpress.org/block-editor/getting-started/devenv/get-started-with-wp-scripts/) intro guide.

With wp-scripts package you can use Javascript modules to distribute your code among different files and get a few bundled files at the end of the build process (see [example](https://github.com/WordPress/block-development-examples/tree/trunk/plugins/data-basics-59c8f8))


## Install 'wp-scripts'

```npm instal @worpdpress/scripts --save-dev```

## Setup 

Commands that can be called to `wp-scripts` or inserted in `/package.json` to ease:
```
"scripts": {
        "start": "wp-scripts start",
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
        "test:e2e": "wp-scripts test-e2e",
        "test:unit": "wp-scripts test-unit-js"
    }
```

more info about further setup, build and stard functions at  [JavaScript Build Setup tutorial](https://github.com/WordPress/gutenberg/tree/HEAD/docs/how-to-guides/javascript/js-build-setup.md)


When using the `start` or `build` commands, the source code directory ( the default is `./src`) and its subdirectories are scanned for the existence of `block.json` files. If one or more are found, they are treated a entry points and will be output into corresponding folders in the build directory.


## Plug-in Structure
`index.php` -> main file for plug-in
This declares a plug-in for WordPress to list it in the available plug-ins tab.
```
<?php
/**
 * Plugin Name:       My plug-in
 * Description:       Interactivity API Quiz
 * Requires at least: 6.1
 * Requires PHP:      7.0
 * Version:           0.1.0
 * Author:            The WordPress Contributors
 * License:           GPL-2.0-or-later
 */
```



## Basic Block: [from here](https://developer.wordpress.org/block-editor/how-to-guides/block-tutorial/writing-your-first-block-type/)

### 1. Create the basic `block.json`
```
/* block.json */
{
    "apiVersion": Block API version
    "title": Block title shown in inserter
    "name": Unique name defines your block
    "category": Category in inserter (text, media, design, widgets, theme, embed)
    "icon": Dashicon icon displayed for block
    "editorScript": JavaScript file path to load for block
}
```

### 2. Register the block in a plug-in

With the `block.json` in place, the registration for the block is a single function call in PHP, this will setup the block and JavaScript file (`index.js`) specified in the `editorScript` property to load in the editor.

```
/* Apend to index.php */

function gutenberg_examples_01_register_block() {
    register_block_type( __DIR__ );
}
add_action( 'init', 'gutenberg_examples_01_register_block' );
```


### 3. Edit the block

The `editorScript` referenced in `block.json` (`index.js`) defines two important functions ( `edit()` and `save()`).

```
/* index.js */

import { registerBlockType } from '@wordpress/blocks';

// Register the block
registerBlockType( 'gutenberg-examples/example-01-basic-esnext', {
    edit: function () {
        return <p> Hello world (from the editor)</p>;
    },
    save: function () {
        return <p> Hola mundo (from the frontend) </p>;
    },
} );
```

The `edit` function is a component that is shown in the editor when the block is inserted.

The `save` function is a component that defines the final markup returned by the block and saved in post_content.


### 4. Build

In order to register the block, an asset php file is required in the same directory as the directory used in register_block_type() and must begin with the script’s filename.