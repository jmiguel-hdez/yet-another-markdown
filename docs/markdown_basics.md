# Markdown Basics support

The most basic built-in support for markdown in vscode is done by the markdown basics driver. It is in the github repository for vscode [here](https://github.com/microsoft/vscode/tree/main/extensions/markdown-basics)

The grammar for markdown seems to be mantained in a separate [repository](https://github.com/microsoft/vscode-markdown-tm-grammar)

This is mantained in yaml and converted to textmate XML. Then that grammar gets converted back to json using another script [vscode-grammar-updater]
(https://github.com/microsoft/vscode-grammar-updater).

you could clone the grammar and run
```console
npm install
npm run build
```
to generate the xml

this other package is doing the update.
```
npm install vscode-grammar-updater
```

in the build system, you can see the command.
```json
"scripts": {
    "update-grammar": "node ../node_modules/vscode-grammar-updater/bin microsoft/vscode-markdown-tm-grammar syntaxes/markdown.tmLanguage ./syntaxes/markdown.tmLanguage.json"
  }
```

which means
```console
vscode-grammar-updater repoName (repoPath destinationPath)+
```

Now, one could use the json file to generate a basic template for a language extension using [Yeoman](https://yeoman.io/) and [VS Code Extension Generator](https://www.npmjs.com/package/generator-code)

That is documented very well in [your first extension](https://code.visualstudio.com/api/get-started/your-first-extension)


run the command:
`npx --package yo --package generator-code -- yo code`

and respond the questions
```shell
# ? What type of extension do you want to create? New Languge Support
# ? URL or file to import, or none for new: () https://raw.githubusercontent.com/microsoft/vscode/5c18500a4494a39a43c556b45721a2392620c733/extensions/markdown-basics/syntaxes/markdown.tmLanguage.json
# ? What's the name of your extension? yet another markdown basics
# ? What's the identifier of your extension?(markdown) ya-markdown-basics
# ? What's the description of your extension? basic support for markdown syntax
# Enter the id of the language. The id is an identifier and is single, lower-case name such as 'php', 'javascript'
# ? Language id: (markdown) LEAVE BLANk
# Enter the name of the language. The name will be shown in the VS Code editor mode selector.
# ? Language name: (Markdown) LEAVE BLANK
# Enter the file extensions of the language. Use commas to separate multiple entries (e.g. .ruby, .rb)
#? File extensions: (.md, .mdown, .markdown, .markdn) LEAVE BLANK
# Enter the root scope name of the grammar (e.g. source.ruby)
# ? Scope names: (text.html.markdown) LEAVE BLANK
# ? Initialize a git repository? (Y/n) Y

# Do you want to open the new folder with Visual Studio Code? Skip

```

There are 3 parts to the extension and the language extensions guides cover them.

1 .[The Syntax Hightlight guide](https://raw.githubusercontent.com/microsoft/vscode-markdown-tm-grammar/refs/heads/main/syntaxes/markdown.tmLanguage)

2. [Snippet Guide](https://code.visualstudio.com/api/language-extensions/snippet-guide)

3. [Language Configuration Guide](https://code.visualstudio.com/api/language-extensions/language-configuration-guide)


References:
https://code.visualstudio.com/docs/languages/markdown
