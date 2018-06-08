# Encryption for file, folders or whole project via gulp

### Instaling:
> npm i encryption-gulp -D
 ________________________________________________________
 ________________________________________________________
 #### Props
| Name | Type | Default | Description |
| --- | --- | --- | --- |
| **password** | `string` | *password* | you secret password for encrypting / decrypting  |
| **decrypt** | `boolean` | *false* | is should do decryption |

 ________________________________________________________
 ________________________________________________________
 ### Usage encryption for one file
 in your gulpfile.js:
 ```javascript
const gulp = require('gulp');
const encryption = require('encryption-gulp');

gulp.task('encrypt', function() {
  gulp.src('src/index.js')
    .pipe(encryption({
      password: 'password',
      decrypt: false,
    }))
    .pipe(gulp.dest('dist-enc'));
});

 ```
  ### Usage encryption for whole project

 ```javascript
const gulp = require('gulp');
const encryption = require('encryption-gulp');

gulp.task('encrypt', function() {
  gulp.src('src/**/*'')
    .pipe(encryption({
      password: 'password',
      decrypt: false,
    }))
    .pipe(gulp.dest('dist-enc'));
});
 ```

 ### Usage decryption
 just need set `decrypt: true`
 ```javascript
const gulp = require('gulp');
const encryption = require('encryption-gulp');

gulp.task('decryption', function() {
  gulp.src('dist-enc/index.js')
    .pipe(encryption({
      password: 'password',
      decrypt: true,
    }))
    .pipe(gulp.dest('src-dec'));
});
 ```
________________________________________________________
________________________________________________________
If you have any issue go here
**[ISSUES](https://github.com/sakalx/encrypt/issues)**
 ________________________________________________________
 ________________________________________________________
License
----

MIT

**Free, Hell Yeah! 😈**