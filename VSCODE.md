# My VS Code Settings

Theme: **Monokai Pro**

settings.json

```json
{
  "emmet.excludeLanguages": [],
  "emmet.includeLanguages": {
    "markdown": "html",
    "javascript": "javascriptreact",
    "typescript": "typescriptreact"
  },
  "emmet.triggerExpansionOnTab": true,
  "html.autoClosingTags": true,
  "javascript.autoClosingTags": true,
  "javascript.suggest.autoImports": true,
  "search.exclude": {
    "**/coverage": true,
    "**/node_modules": true
  },
  "typescript.autoClosingTags": true,
  "typescript.suggest.autoImports": true,
  "workbench.colorTheme": "Monokai Pro",
  "workbench.iconTheme": "vscode-icons",
  "editor.formatOnSave": true,
  "files.autoSave": "onFocusChange",
  "[jsonc]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "git.enableSmartCommit": false,
  "explorer.confirmDelete": false,
  "window.zoomLevel": 0,
  // ESLint Plugin Settings for VSCode (autofix on save, Jest aware, babel parser etc.
  "eslint.alwaysShowStatus": true,
  "eslint.format.enable": true,
  "eslint.lintTask.enable": true,
  "eslint.options": {
    "parser": "@babel/eslint-parser"
  },
  "eslint.validate": ["javascript"],
  "editor.fontFamily": "'FiraMono Nerd Font Mono', Menlo, Monaco, 'Courier New', monospace",
  "editor.fontSize": 15,
  "javascript.validate.enable": false, //disable all built-in syntax checking
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true,
    "source.fixAll.tslint": true,
    "source.organizeImports": true
  },
  "jest.autoRun": "off"
}
```
