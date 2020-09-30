# 🎢 openrct2-typescript-mod-template
![GitHub](https://img.shields.io/github/license/wisnia74/openrct2-typescript-mod-template) ![GitHub code size in bytes](https://img.shields.io/github/languages/code-size/wisnia74/openrct2-typescript-mod-template) [![Dependabot](https://badgen.net/badge/Dependabot/enabled/green?icon=dependabot)](https://dependabot.com/)

Template repository for OpenRCT2 mods written in TypeScript.

## Table of contents
  * [About](#about)
  * [Installation](#installation)
  * [Usage](#usage)
     * [How it works](#how-it-works)
     * [npm scripts](#npm-scripts)
  * [Releasing your mod](#releasing-your-mod)
  * [Notes](#notes)
  * [Useful links](#useful-links)

## About

This repository was created to serve as a template TypeScript mod repository for OpenRCT2.

I wanted to leverage [OpenRCT2 hot reload feature](https://github.com/OpenRCT2/OpenRCT2/blob/master/distribution/scripting.md#writing-scripts) to make it even more painless to write and debug mods in real time.

This template repository comes with [Nodemon](https://nodemon.io/), [ESLint](https://eslint.org/) and [TypeScript](https://www.typescriptlang.org/) on board.

The idea was to use Nodemon to start a local server that will be watching your mod files, then on each save make it build `.ts` files to ES5 `.js` files, place them inside OpenRCT2 `plugin` directory, and let hot reload feature do the rest (i.e. reload the mod in-game).

## Installation

1. Install latest versions of [Node](https://nodejs.org/en/) and [npm](https://www.npmjs.com/get-npm)
2. Create your own repository using this one as a template and clone it anywhere to your PC
3. Find `openrct2.d.ts` TypeScript API declaration file in OpenRCT2 files and copy it to `lib` folder (this file can usually be found in `C:\Users\<user>\Documents\OpenRCT2\bin`)
4. Edit `./src/MOD_NAME.ts` and fill out `registerPlugin` function with right values (refer to [OpenRCT2 scripting guide](https://github.com/OpenRCT2/OpenRCT2/blob/master/distribution/scripting.md))
5. Edit `./tsconfig-develop.json` and replace `<path_to_openrct2>` with your path to OpenRCT2
6. Once you do all the above, you can remove `LICENSE` file, `.github` folder and `README.md` from `lib` folder.
7. You can start modding :)

Of course it's a template, so you can edit anything you like - `package.json` (which I recommend doing), `tsconfig` files and so on.

## Usage

1. `cd` into repo
2. run `npm run build:develop` (this will place compiled `./src/MOD_NAME.ts` inside `<path_to_openrct2>/plugin/<MOD_NAME>` directory)
3. Make sure you've enabled [OpenRCT2 hot reload feature](https://github.com/OpenRCT2/OpenRCT2/blob/master/distribution/scripting.md#writing-scripts)
4. Open `./src/MOD_NAME.ts` in your code editor
5. Run `npm start`
6. Start OpenRCT2 with console and load save/start new game
7. Each time you save the file the server will compile `./src/MOD_NAME.ts` and place it inside `<path_to_openrct2>/plugin/<MOD_NAME>` directory (to be precise, it watches **all files in `./src/`**, so if you have more than one folder and/or more than one file, they will all get compiled and moved there too)
8. OpenRCT2 will notice file changes and it will reload the mods

### How it works

Your mod files live in `./src/` directory. That's the ones you will be writing code in.
Upon starting Nodemon server, it will start watching changes you make to files in `./src/`, and it will build them accordingly.

### npm scripts

|script|function|
|--|--|
|`npm start`|starts Nodemon server that will be watching `./src/` directory for any changes you make to `.ts` files inside it|
|`npm run lint`|lints your `.ts` files from `./src/` directory|
|`npm run build:develop`|compiles all `.ts` files from `./src/` to ES5 `.js` files, and places them inside `<path_to_openrct2>/plugin/<MOD_NAME>` directory|
|`npm run build`|runs `npm run lint` and if no linting errors are found, compiles your `.ts` files to ES5 `.js` files and places them inside `./dist/` folder - those are your final mod files|

## Releasing your mod

After running `npm run build` locally, `./dist/` directory will be created that will contain all the compiled files from `./src/`.
It's up to you, if you want to edit `.gitignore` to actually include `./dist/` contents and push them to your remote or if you want to manually copy the contents of `./dist/` and publish them somewhere. However creating a GitHub release using zipped contents of `./dist/` directory sounds like a cool idea. You would have your mod file available for download straight from the repo.

## Notes

If you've added a new mod folder to `plugin`, and the OpenRCT2 didn't seem like it registered it (and you had a running park), just load the save/start a new park, so OpenRCT2 loads the mods again. Now when you overwrite them during development, there shouldn't be any problems with hot reload noticing file changes.

Nodemon will watch all the files in `./src/` directory. You can also freely create classes, modules, import them in your mod files. Sky's the limit :)

## Useful links

- [OpenRCT2 website](https://openrct2.io/)
- [OpenRCT2 on GitHub](https://github.com/OpenRCT2)
- [OpenRCT2 on Reddit](https://www.reddit.com/r/openrct2)
- [OpenRCT2 plugins website](https://openrct2plugins.org/)
- [OpenRCT2 example plugins repository](https://github.com/OpenRCT2/plugin-samples)
- [OpenRCT2 scripting guide](https://github.com/OpenRCT2/OpenRCT2/blob/develop/distribution/scripting.md)
- [OpenRCT2 hot reload feature presentation](https://www.youtube.com/watch?v=jmjWzEhmDjk)
