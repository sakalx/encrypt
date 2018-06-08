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
  gulp.src('src/**/*')
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
 > One more example, **all together now**
  ```javascript
  const gulp = require('gulp');
const encryption = require('encryption-gulp');

const KEY = require('./KEY');

const path = {
  decrypted: 'src-decrypted',
  encrypted: 'src-encrypted',
};

const pathSrc = {
  assets: ['src/**/*', '!src/**/*.js'],
  js: 'src/**/*.js',
};

const pathEncrypt = {
  assets: [`${path.encrypted}/**/*`, `!${path.encrypted}/**/*.js`],
  js: `${path.encrypted}/**/*.js`,
};

const encrypt = (pathIn, pathOut, decrypt) => {
  gulp.src(pathIn)
    .pipe(encryption({
      password: KEY,
      decrypt: decrypt,
    }))
    .pipe(gulp.dest(pathOut));
};

const assets = (pathIn, pathOut) => {
  gulp.src(pathIn)
    .pipe(gulp.dest(pathOut));
};

gulp.task('addAssetsSrc', () => assets(pathSrc.assets, path.encrypted));
gulp.task('addAssetsEncrypt', () => assets(pathEncrypt.assets, path.decrypted));

gulp.task('encrypting', ['addAssetsSrc'], () => encrypt(pathSrc.js, path.encrypted, false));
gulp.task('decrypting', ['addAssetsEncrypt'], () => encrypt(pathEncrypt.js, path.decrypted, true));
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