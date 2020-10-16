https://medium.com/@brianhan/watch-compile-your-sass-with-npm-9ba2b878415b

Create a package.json file and follow the prompts.

`npm init`

Now let’s set up our files. Create these folders:

`mkdir bin public scss && mkdir public/css`

scss folder is where I like to keep all of my scss files and directories.
public folder is where I keep all my static assets, inside I have a css folder for my css files.
bin folder is where we are going to put a command line script to compile our scss files.


Now let’s create some files:
`touch scss/main.scss .gitignore`

main.scss is where we will write out scss code.
(optional) 
.gitignore is a hidden file we use to tell GitHub what files and folders to exclude from our repo. I like to tell GitHub to ignore my node_modules folder. If me or anyone else needs to clone my repo, I usually tell them to npm install based on the packages in package.json.

Simple Sass compiler and watcher

When I started playing around with npm scripts, my original intention was to stop using gulp and try to write everything I needed using things like node-sass, autoprefixer, and browsersync without their respective gulp tasks.

In this section, I’ll show you how I made a simple sass compiler and watcher without using gulp.js and only using npm scripts.
This section will probably be the simplest example for understanding npm scripts so let’s diiiiive in.
Sploosh!

Install the things

Let’s install our dev-dependencies:
`$ npm install -D node-sass nodemon`


-D flag is another way of saying “write these node_modules into my package.json under devDependencies” (go look at your package.json)
node-sass is that thing gulp-sass uses to compile your scss files to css files. node-sass wraps Libsass.
nodemon is a thing we’ll use to watch for changes on our scss files. Normally, it’s used to watch for changes on your server-side Node.js code.

Compile the Sass
Before we write our first script, write some dummy scss in your main.scss file so node-sass can use that to compile.

`$badass: #bada55;
body { 
  margin: 0; 
  background-color: $badass; 
}`

Now, let’s write a command line script for compiling our scss files using node-sass.
In your package.json, find the “scripts” object and inside, write the following code:

`“scripts”: {
  “build-css”: “node-sass --include-path scss scss/main.scss   public/css/main.css”
},`

In your terminal, do this:

`npm run build-css`


Watch the Sass
Let’s update our scripts with a watch script. Inside package.json, make your scripts object look like this:

`“scripts”: {
 “build-css”: “node-sass --include-path scss scss/main.scss public/css/main.css”,
 “watch-css”: “nodemon -e scss -x \”npm run build-css\””
},`

Now let’s try it in the terminal!

`npm run watch-css`

`npm install lite-server`
