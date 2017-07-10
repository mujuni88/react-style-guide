# Editor

1. Install [Visual Studio Code](https://code.visualstudio.com/docs/languages/javascript)
2. Install the following extensions:

   ```
   code --install-extension 

   DavidAnson.vscode-markdownlint
   EditorConfig.EditorConfig
   HookyQR.beautify
   IBM.output-colorizer
   JerryHong.autofilename
   MattiasPernhult.vscode-todo
   Orta.vscode-jest
   Orta.vscode-react-native-storybooks
   PKief.material-icon-theme
   Shan.code-settings-sync
   TimonVS.ReactSnippetsStandard
   alefragnani.project-manager
   andischerer.theme-atom-one-dark
   bierner.color-info
   carlosjs23.vscode-yarn-script
   chenxsan.vscode-standard-format
   chenxsan.vscode-standardjs
   christian-kohler.npm-intellisense
   codezombiech.gitignore
   cssho.vscode-svgviewer
   dbaeumer.vscode-eslint
   donjayamanne.githistory
   dzannotti.vscode-babel-coloring
   eg2.vscode-npm-script
   emmanuelbeziat.vscode-great-icons
   felipecaputo.git-project-manager
   fknop.vscode-npm
   flowtype.flow-for-vscode
   formulahendry.auto-rename-tag
   gcazaciuc.vscode-flow-ide
   iZDT.javascript-unit-test-snippet
   ianhoney.task-master
   jock.svg
   lihui.vs-color-picker
   ms-vscode.Theme-MarkdownKit
   msjsdiag.debugger-for-chrome
   octref.vscode-json-transform
   robertohuertasm.vscode-icons
   rtorr.vscode-flow
   rubbersheep.gi
   shinnn.standard
   vilicvane.es-quotes
   vscodevim.vim
   vsmobile.vscode-react-native
   waderyan.gitblame
   wmaurer.join-lines
   wsds.theme-hacker
   xabikos.ReactSnippets
   xabikos.JavaScriptSnippets
   zgudino.editorconfig-vscode-snippet
   zhuangtongfa.Material-theme
   ```

3. Create a `jsconfig.json`  in your root directory with the following content:

   ```
   {
    "compilerOptions": {
      "experimentalDecorators": true
    }
   }
   ```

4. Add the following to your `settings.json` file to enable linting:

   ```
   "standard.enable": true, 
   "standard.autoFixOnSave": true,
   ```



