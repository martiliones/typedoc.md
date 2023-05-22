> ⚠️
> Typedoc.md plugin is currently in beta version. Some features may still be under development or may not function as expected.

<img src="preview-dark.png#gh-dark-mode-only"/>
<img src="preview-light.png#gh-light-mode-only"/>

<h1>
  <img src="down.svg" height="24"/>
  typedoc.md
</h1>

**Typedoc.md** is a powerful plugin inspired by Vue's API documentation style, it generates Markdown documentation using types and comment descriptions from `.ts` and `.d.ts` files.

You can use it to create Markdown files for:
- 🔧 **Static Site Generators**: Vuepress, Jekyll, Hugo etc.
- 📚 **Knowledge Base Systems**: GitHub/Lab Wiki, Readme.io etc.

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

## License

MIT - [martiliones](https://github.com/martiliones)
