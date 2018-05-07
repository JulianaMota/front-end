# The Terminal, NPM & git in the terminal
Mac users have an excellent terminal built in, Windows users should either use git-bash or the terminal in your editor
## Requirements
### codecademy, the command line
https://www.codecademy.com/learn/learn-the-command-line 
part 1, 2 & optionally 3

## using the terminal, cheatsheet
 - Remember, TAB is your friend, it can autocomplete a lot of stuff
 - Arrow up / down goes through your history, so you don't have to type the same over and over
 
| command | explanation | examples |
---|---|---
`cd`|change directory | `cd` navigates to your home folder
`cd ..`|go up one level|N/A
`cd ../../`|go up two levels|`cd ../..` does the same
`cd /`|go to the root of the machine/server|N/A
`cd folder`|go to the specified folder|`cd dist/js`
`pwd`|Print working directory| Prints out where you are
`ls`|list files in dir|N/A
`ls -lah`|List all files in dir, including hidden| N/A
`rm file.ext`|delete a file| can be used with a wildcard `rm *.html`
`rm -rf folder`|delete a folder and all sub folders| Beware `rm -rf /` would try to delete everything on your computer
`mv old new`|move/rename a file or folder|`mv out dist`
`touch file.ext`|create a new file or change it's "last edited status"|N/A
`open file.ext`|open the file in the preferred program|N/A
`>`|"pipe" the content from the terminal into a file|`ls -lah > out.txt`
`cmd1 && cmd2`|run commands after each other|`touch .gitignore && open .gitignore`

### Excercise
clone X from github, fire up the terminal, navigate to the root of the folder and perform the following tasks in groups of 2-3 people
1. delete all folders starting with `del_`
2. in the `src` folder, create the following structure
    - css/main.css
    - js/index.js
    - assets/gfx/
3. delete everything inside the `dist` folder
4. copy everything from the `src` folder to the `dist` folder

## git in the terminal
| action | command | notes |
---|---|---
add a file (stage) | `git add filename.ext` | 
add all changed files | `git add --all`| beware!
commit staged files | `git commit -m "my commit message"`| 
add and commit, one-liner | `git commit -am "my message"` | does NOT add new/untracked files
push commited to remote | `git push` |
status | `git status` | overview of staged files etc, **really** usefull
rm | `git rm filname` | remove a tracked file (and delete it) e.g `git rm main.js`
**branches** | |
list branches | `git branch -a` | 
checkout a branch | `git checkout branchname`| ex: `git checkout login`
merge branch | `git merge branchname` | standing on the branch you wish to merge in to, remember to checkout the new branch. ex: `git merge login`
"set upstream" | `git push --set-upstream origin branchname` | ex: `git push --set-upstream origin login`
**cloning / initializing** ||
clone a repository | `git clone repositoryname.git` | will create a local folder called 'repositoryname', pass ` .` to clone to an existing folder
setup a new repo locally | `git init`| 
**other** | |
list commits | `git log`| This one has **a lot of options**

### .gitignore
There are lots of files we do not wish to push, like platform dependent files ($Thumbs.db, mac hidden files, node_modules etc). Furthermore, it's considered bad practice to push "build" folders and minified source code.

We can create a file called `.gitignore` in the root of our project to lidt those files
1. `touch .gitignore`
2. `open .gitignore` or open it in your editor
3. Add a line for each folder / file to exclude from git, e.g.
    * `node_modules/`
    * `build/`
    * `TODO.md`

So if you add the line `node_modules` git status will no longer show it as being changed/added when you do a `git status`

### git workflow
There's no fixed way to do it, but here's a rule-of-thumb-aproach
1. `git branch todays-tasks`
2. `git checkout todays-tasks`
3. do some coding
4. `git add newfile.ext`
5. `git commit -m "some message"`
6. goto 4
7. Something is working: `git push --set-upstream origin todays-tasks` (only done once?)
8. `git push` and goto 4
9. Everything is awesome: `git checkout master && git merge todays-tasks`

### merge conflicts
They are bound to happen, and one of the main reasons we use git
First up, two ways to merge
1. From github.com
With two branches pushed to github, go to "Pull requests", select "master" as base, and choose the branch you want to merge into master

Then follow the GUI / instructions

2. Manually / terminal /editor
Requires a bit more work, but it's oh so nice :-)

Once a conflict is encountered, open the file in VS Code (or WebStorm) and use the GUI to select the changes you like

## NPM
NPM is our package manager, it handles downloading / using JS libraries for us.

Two new kids on the block are Yarn & Turbo, they do exactly the same, but a re a bit more shiny. NPM is still the standard, we'll use that
### Requirements
Install [Node](https://nodejs.org/en/) which will also install NPM (you should probably choose the LTS version)

### Global vs. Local
Global packages can be used everywhere, in the terminal. But only a few modules should be installed globally. They take up space, needs manual updates, and it's kinda hard to cleanup.

Local modules can only be used in the current project (but can of course be installed for every project), and cannot be run from the terminal directly, for that we need to setup NPM (more later).

Warning, almost all modules indicate you should install the module globally, that is rarely the case.

### [npmjs.com](https://npmjs.com)
Is where you'll find all your modules, there's a short description, and usage instructions for each. But it's hard to read, and often not suited for "command-line-usage", the modules github repo is often the best place to find answers.

### Installing a global module
When you have found a module, open up the terminal and write `npm install -g modulename`

Then it's available everywhere by typing modulename (or something close to that, for instance, the module `pageres-cli` is run by typing `pageres`). The documentation states what you need to do.

### Fun global modules to play with
These are a few of my favourites, let me know if you have any fun ones :-) None of these modules have to be global, but they are modules I often want to use outside a project, which makes them perfect candidates for global modules.

Note: With a service running, you can press `ctrl+c`to stop it

1. `npm install -g live-server`

[live-server](https://www.npmjs.com/package/live-server) gives us a development server. Everytime we change a file, it reloads the webpage. Just like Brackets' live preview, except this one won't break. In the terminal, navigate to any old project you have and type `live-server`

2. `npm install -g pageres-cli`
[pageres-cli](https://github.com/sindresorhus/pageres-cli) takes a screenshot of a webpage in various resolutions.

#### Usage
`pageres website.com widthxheight widthxheight widthxheight [--crop]`
By default we supply a height, and pageres ignores it, unless we supply the argument `--crop``

- Take a screenshot of facebook: `pageres facebook.com 768x300`
- Take a screenshot of facebook, cropping it to 300 px (height): `pageres acebook.com 768x300 --crop`
- Take several screenshots of facebook: `pageres facebook.com 1600x800 1200x800 1000x800 600x800 --crop`

Note: pageres uses a thing called phantomjs (a browser that doesn't show anything :) and is not always updated with the latest JS features, meaning, that the screenshots we get might be a bit off.

3. `npm install -g svgo`
[svgo](https://www.npmjs.com/package/svgo) Used to optimize/minify SVG's, this time *you* take a look at [the documentation](https://www.npmjs.com/package/svgo)



### setup NPM for the current project
`npm init`
This will give us a file called package.json. We can add scripts/commands to it, to automate our workflow.

show cat css/*.css > bundle.css
convert to npm script
npm run myfirstscript

"bundlecss": "cat a.css b.css > bundle.css"
`cat styles/*.css > out/bundle.css`

evt https://github.com/giakki/uncss
4. `npm install -g purifycss`
OMG this is so cool (but not perfect). It looks through your html/js/css files and finds selectors that are not used, and removes them. Really awesome if you use a framework.

https://github.com/purifycss/purifycss
purifycss src/css/main.css src/css/bootstrap.css src/js/main.js --min --info --out src/dist/index.css
(læser filer ind fra venstre til højre)
"purify": "purifycss index.html  a.css b.css bootstrap.min.css --info --out dist.css" virker
"purify": "purifycss index.html  bootstrap.min.css a.css b.css  --info --out dist.css" ocverser enkelte styles i a.css
purify skal nok kun bruges på framework css? evt på en fil af gangen?
 "p2": "purifycss *.html *.css *.js --info --out out/dist.css"
 
npm run ....
npm start, test, pre?
--save --save-dev

## restoring node_modules
rm -rf node_modules
npm install

## transpiling / bundling
The next section is fully explained (and very well) in https://medium.com/the-node-js-collection/modern-javascript-explained-for-dinosaurs-f695e9747b70
### pure babel
TODO webpack has changed to v4
https://www.valentinog.com/blog/webpack-4-tutorial/#webpack_4_as_a_zero_configuration_module_bundler

browser-sync start --server 'dist' --files 'dist'
https://gist.github.com/adamreisnz/9edf1f48e19c104b81f8102a27de0940
http://lucasmreis.github.io/blog/npm-is-an-amazing-build-tool/


``` "purebabel": "babel index.js --presets babel-preset-env --out-dir distribution" ```
But that won't enable "require", we need a bundler
Enter webpack

npm install webpack babel-core babel-preset-env babel-loader --save-dev

create webpack.config.js

// webpack.config.js
module.exports = {
  entry: './index.js',
  output: {
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['env']
          }
        }
      }
    ]
  }
};


## linting

//TODO https://www.npmjs.com/package/critical
//TODO https://github.com/pwa-builder/ManifoldJS