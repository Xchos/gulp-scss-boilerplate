# gulp-scss
Gulp + SCSS Boilerplate. Small example to play with.


# Requirements
- [node](http://nodejs.org)
- [gulp.js](http://gulpjs.com)


# Installation

To install all dependencies (specified in package.json)
```bash
npm install
```

# Usage

## Basic Usage

When all dependencies are installed execute `gulp` command in terminal. Now you are ready to edit `.html` and `.scss` files and play with this example. You don't need a server to run this example. Just open `index.html` file in your favorite browser.

## How it works?

### Configuration

When `npm install` command is executed it installs dependencies which are specified in `package.json` file (an `node_modules` folder will be created).
```javascript
{
  "devDependencies": {
    "gulp": "~3.9.0",
    "gulp-sass": "^2.2.0"
  }
}

```

`gulp` command executes `gulpfile.js`.
```javascript
/*-------------------------------------
	Register NPM Modules
-------------------------------------*/
var gulp = require('gulp'),
	sass = require('gulp-sass');
	

/*-------------------------------------
	Compile and process CSS
-------------------------------------*/
gulp.task('css', function () {
	// take files with extension .scss from /scss folder
	return gulp.src('/scss/*.scss')

		// use scss module on it
		.pipe(sass({
				// - - - - - - - - - - 
				// list of compile options you can see here:
				// https://github.com/sass/node-sass
				// - - - - - - - - - - 
				
				// allows easier debug scss files
	            // sourceComments: true,
	            
	            // when moving project on production - generate compressed version of css
	            // outputStyle: 'compressed'
        	}).on('error', sass.logError)
		)
		// return into css folder
		.pipe(gulp.dest('/css/style.css'))
});




/*-------------------------------------
	watch
-------------------------------------*/
// on specific file change execute task
gulp.task('watch', function() {
	// watch .scss files - on file-change execute css task (compile scss)
	gulp.watch('scss/**/*.scss', ['css']);
});

/*-------------------------------------
	default tasks
-------------------------------------*/
// when calling 
// > gulp
// execute css & watch tasks.
gulp.task('default', ['css', 'watch']);
```