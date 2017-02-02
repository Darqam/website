<div align="center">
    <a href="/"><img src="/assets/img/DiamondLogo.svg" width="546" alt="diamond" /></a>
</div>

## Installation
Using npm:
```bash
npm i -g diamondpkg
```

Or install the latest version from GitHub:
```bash
npm i -g diamondpkg/diamond
```

## Quick Start
Lets say you want to use Bootstrap in your next project.

### Installing
You can find Bootstrap under the package name `bootstrap@next` (`@next` means the next tag on npm, which is in sass, not less)  
You install with the `install` command
```bash
diamond install bootstrap@next
```
If the last log you see says `dia info ok`, then the install succeeded. If not you should troubleshoot your errors.

This generates a `diamond` folder in the following format.
```
diamond
|-- .internal
|   `-- packages.lock
|-- .staging
|-- packages
|   `-- bootstrap
|       `-- bootstrap files
|-- index.js
```
<p class="danger">Do not edit any files in this folder.</p>
The `diamond/.internal` folder is for files used by diamond.  
The `diamond/.staging` folder is a teporary location for files durning install.  
The `diamond/packages` folder is where all of your packages go.  
The `diamond/index.js` file is the JS file that handles all of your importing (See [compiling](#compiling))

### Importing
diamond uses a custom import format when importing packages.

Examples:
* `@import "[bootstrap]";` will import the main file from Bootstrap, or throw an error if the package does not have a main file.
* `@import "[bootstrap/file.scss]"` will import `file.scss` from the package Bootstrap.

We want to import Bootstrap's main file, so we will use `[bootstrap]`
```scss
@import "[boostrap]";

#foo {
  bar: baz;
}
```

### Compiling
Once we have written our sass, we are ready for compiling.

If you try
```bash
node-sass myfile.scss
```
it will give you errors about not being able to find the file `[boostrap]`. 
This is because you aren't using diamond's custom importer.

It is recommended to use the compile command to compile your Sass instead of node-sass.
While this is not required, some packages like `concise.css` use functionality only found
in the compile command.

```bash
diamond compile -o output.css input.scss
```

To compile with node-sass, use the `--importer` flag
```bash
node-sass --importer diamond -o output.css input.scss
```
where `diamond` is the generated `diamond` folder on install.