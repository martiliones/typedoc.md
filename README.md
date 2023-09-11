> ⚠️
> Typedoc.md plugin is currently in beta version. Some features may still be under development or may not function as expected.

<img src="preview-dark.png#gh-dark-mode-only"/>
<img src="preview-light.png#gh-light-mode-only"/>

<h1>
  <img src="down.svg" height="24"/>
  typedoc.md
</h1>

**Typedoc.md** is a powerful plugin inspired by Vue's API documentation style, it generates Markdown API Reference using types and comment descriptions from `.ts` and `.d.ts` files.

You can use it to create Markdown files for:
- 🔧 **Static Site Generators**: Vuepress, Jekyll, Hugo etc.
- 📚 **Knowledge Base Systems**: GitHub/Lab Wiki, Readme.io etc.

## Examples

Before going to know how deep does the rabbit hole go, you might want to check out [_examples_](https://github.com/martiliones/typedoc.md/blob/master/examples).

## Installation

To use **Typedoc.md**, you can install it using any Node.js package manager from the npm registry. Additionally, you need to have Typedoc installed:

```
npm i -D typedoc typedoc-md
```

## Usage

To use the plugin, simply specify the `plugin` option when running the `typedoc` command in one of the following ways:

- The `typedoc` CLI flag:

  ```sh
  typedoc --plugin typedoc-md --out docs src/index.ts
  ```

- `typedoc.json` configuration file:

  ```jsonc
  {
    "plugin": "typedoc-md"
  }
  ```

## Structure

The plugin _does NOT_ automatically categorize declarations by kind (such as Classes, Functions, Enums, etc.). Instead, you **must** manually group them based on their logical relationships.

### `@path`

To specify which file or directory each declaration should go in, use the `@path` tag:

<table>
<tr>
<td>
  
```ts
/**                                                               
 * @path Global Api
 */
export version = string

/**
 * @path Global Api/Application
 */
export function createSSRApp(/* ... */): App

/**
 * @path Advanced
 */
export function h(/* ... */): VNode
```

</td>
<td>

```bash
.
├── Global Api/
│   ├── README.md     
│   └── Application.md
└── Advanced.md       










```

</td>
</tr>
</table>

Notice that if you use the `@path` tag that matches a previously used directory name, a `README.md` will be created within that directory. For a specific file placement, add `.md` to the path.

Let's see how the structure has changed after appending the extension to the `version`'s path:

<table>
<tr>
<td>
  
```ts
/**                                                             
 * @path Global Api.md
 */
export version = string

// ...
```

</td>
<td>

```diff
  .
  ├── Global Api/
- │   ├── README.md     
  │   └── Application.md
  ├── Advanced.md       
+ └── Global Api.md    

```

</td>
</tr>
</table>

### `@module`

To declare shared options for file's declarations, you can use `@module` tag in the comment on top of the file. 

For example, if you want to keep all the functions from `utils.ts` together in one file you can specify `@path` in the top-level comment:

<table>
<tr>
<td>

```ts
/**
 * @module
 * @path Utilities
 */

/**
 * This declaration is placed under 'Utilities'    
 */
export function isRef(r: Ref): r is Ref

/**
 * And so is this one.
 */
export function unref<T>(ref: Ref<T>): T
```

</td>
<td>

## Utilities

### isRef

This declaration is placed under 'Utilities'.  

### unref

And so is this one.

<br><br><br>

</td>
</tr>
</table>

### `@ignore`

This tag marks declarations you want to exclude from documentation.

## Description

The content of the tags is copied exactly as it is, without any special character escaping. This means you can utilize all Markdown features in your JSDoc comments:

<table>
<tr>
<td>

```ts
/**
 * Exposes the current version of _Vue_
 *
 * @details
 * No parameters needed because it is a constant
 *
 * @example
 * This code will print '3.3.4' in the console  
 *
 * ```js
 * import { version } from 'vue'
 *
 * console.log(version)
 * ```
 *
 * @path Global Api
 */
export version = string

// ...
```

</td>
<td>

## Global Api: General

### version

Exposes the current version of _Vue_

- **Details**

  No parameters needed because it is a constant

- **Example**

  This code will print '3.3.4' in the console

  ```js
  import { version } from 'vue'       

  console.log(version)
  ```

</td>
</tr>
</table>

Please note that typedoc.md does NOT generate documentation from `@param` and `@return` tags. Instead, you have to manually describe your parameters and return values in the `@details` section.

<h1></h1>

<p align="center">
🌸 Have a nice day!
</p>
