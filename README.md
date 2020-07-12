# 🎢 openrct2-typescript-mod-template
[![wisnia74](https://circleci.com/gh/wisnia74/openrct2-typescript-mod-template/tree/master.svg?style=shield)](https://app.circleci.com/pipelines/github/wisnia74/openrct2-typescript-mod-template?branch=master)

Template repository for OpenRCT2 mods written in TypeScript.

## Demo
Upon saving the file, it gets compiled, placed in OpenRCT2 `plugin` folder and then OpenRCT2 hot reload feature does the rest. TypeScript features are supported, but on the demo I just show how it works using `console.log`.

![](https://github.com/wisnia74/openrct2-typescript-mod-template/blob/master/demo.gif)

## About

This repository was created to serve as a template TypeScript mod repository for OpenRCT2.

I wanted to leverage [OpenRCT2 hot reload feature](https://github.com/OpenRCT2/OpenRCT2/blob/develop/distribution/scripting.md#writing-scripts) to make it even more painless to write and debug mods in real time.

This template repository comes with [Nodemon](https://nodemon.io/), [ESLint](https://eslint.org/) and [TypeScript](https://www.typescriptlang.org/) on board.

The idea was to use Nodemon to start a local server that will be watching your mod files, then on each save make it build `.ts` files to ES5 `.js` files, place them inside OpenRCT2 `plugin` directory, and let hot reload feature do the rest (i.e. reload the mod in-game).

## Installation

- install latest versions of [Node](https://nodejs.org/en/) and [npm](https://www.npmjs.com/get-npm)
- create your own repository using this one as a template and clone it anywhere to your PC
- `cd` into it and edit `config/init.json` - refer to [this](https://github.com/wisnia74/openrct2-typescript-mod-template/tree/master/config) table to know what to edit
- run `node init.js`
  	- when the script runs `npm init` to generate your npm package, leave `entry` as `init.js`
  	- everything else is optional
- you now have a clean repository and npm package configured so you can start modding :)

## Usage

If you've set `compileTemplateMod` in `config/init.json` as `true`:
- make sure you've enabled OpenRCT2 hot reload feature - read more about how to enable it [here](https://github.com/wisnia74/openrct2-typescript-mod-template/blob/master/demo.gif)
- open `./src/<modName>.ts` in your code editor
- run `npm start`
- start OpenRCT2 with console and load save/start new game
- each time you save the file the server will compile `./src/<modName>.ts` and place it inside `<openrct2PluginFolderPath>/<modName>/` directory
- OpenRCT2 will notice file changes and it will reload the mods

If you've set `compileTemplateMod` in `config/init.json` as `false`:
- you still follow all the above steps, but before them you need to
	- `cd` into repo
	- run `npm run build:develop`
- this will place compiled `./src/<modName>.ts` inside `<openrct2PluginFolderPath>/<modName>/` directory

#### How it works
After the `node init.js` script finishes, you are left with a fully functioning npm package, Nodemon, ESLint and TypeScript configured, and also working npm scripts. All changes made by the script got pushed to your repository if you've set `pushToGithub` to `true` before running it.

Your mod files live in `./src` directory. That's the ones you will be writing code in. 
Upon starting Nodemon server, it will start watching changes you make to files in `./src`, and it will build them accordingly.

#### npm scripts:

|script|function|
|--|--|
|`npm start`|starts Nodemon server that will be watching `./src` folder for any changes you make to `.ts` files inside it|
|`npm run lint`|lints your `.ts` files from `./src` directory|
|`npm run build:develop`|compiles all `.ts` files from `./src` to ES5 `.js` files, and places them inside `<openrct2PluginFolderPath>/<modName>/` directory|
|`npm run build`|runs `npm run lint` and if no linting errors are found, compiles your `.ts` files to ES5 `.js` files and places them inside `./dist` folder - those are your final mod files|

## Notes

If you've added a new mod folder to `plugin`, and the OpenRCT2 didn't seem like it registered it (and you had a running park), just load the save/quit to menu and load the save/start a new park, so OpenRCT2 loads the mods again. Now when you overwrite them during development, there shouldn't be any problems with hot reload noticing file changes.

## Useful links

- [OpenRCT2 website](https://openrct2.io/)
- [OpenRCT2 on GitHub](https://github.com/OpenRCT2)
- [OpenRCT2 on Reddit](https://www.reddit.com/r/openrct2)
- [OpenRCT2 plugins website](https://openrct2plugins.org/)
- [OpenRCT2 example plugins repository](https://github.com/OpenRCT2/plugin-samples)
- [OpenRCT2 scripting guide](https://github.com/OpenRCT2/OpenRCT2/blob/develop/distribution/scripting.md)
- [OpenRCT2 hot reload feature presentation](https://www.youtube.com/watch?v=jmjWzEhmDjk)
