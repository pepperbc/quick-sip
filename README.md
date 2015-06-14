# quick-sip
Gulp build process tasks that provide watchify and sass compilation.

## Project Layout
Here is an example project hierarchy that will work with the default settings:

```
project
  |-- package.json
  |-- gulpfile.js
  |-- app
       |-- scripts
       |      |-- main.js
       |      |-- chairModel.js
       |      |-- chairView.js
       |
       |-- styles
       |      |-- core.scss
       |      |-- whatever.scss
       |      |-- _chair.scss
       |      |-- _engraved.scss
       |
       |-- index.html
```

After running the build task, a "dist" directory will be created:
```
project
   | ...
   |-- dist
        |-- scripts
        |      |-- app.js
        |
        |-- styles
        |      |-- core.css
        |      |-- whatever.css
        |
        |-- index.html
```
**app.js** is the browserified application that main.js completely specifies.
**core.css & whatever.css** are the sass-lib compiled css files.

## Executing Tasks
Your **gulpfile.js** only needs the following to give you access to the build tasks:
```javascript
var gulp = require('gulp');
var buildProcess = require('quick-sip')(gulp);
```

The gulp tasks you care about are:
- **clean** - Remove the contents of the dist directory
- **build** - Builds the whole application; js, css, and resources.
- **watch** - Sets up watchify for your js, listens for scss changes, and handles other resource changes.
- **copy-resources** - Only copy the resources to dist (non-js and non-scss by default)
- **build-styles** - Only builds the styles to dist
- **build-app** - Only builds the javascript to dist

## Transforming Browserify
Easy!
```javascript
var gulp = require('gulp');
var buildProcess = require('quick-sip')(gulp);
/* Transforms */
buildProcess.transform('aliasify');
buildProcess.transform('hbsfy');
buildProcess.transform(yourCustomThroughTransform);
```

## Defining Resource Exclusion Extensions
Easy!
```javascript
var gulp = require('gulp');
var buildProcess = require('quick-sip')(gulp);
/* Assets */
buildProcess.nonResources('js|css|scss|hbs|frag|vert');
```