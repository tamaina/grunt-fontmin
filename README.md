grunt-fontmin-ex
===
[![NPM](https://nodei.co/npm/grunt-fontmin-ex.png)](https://nodei.co/npm/grunt-fontmin-ex/)

[THERE IS JAPANESE README](README.ja.md)

**Subset Fonts Maker**

grunt plugin to minimize CJK fonts

## Modifided by tamaina

* Deleted css output
  * You should write @font-face in your css by yourself
* Added woff2 output
  * By using **ttf2woff2**
  * It requires **node-gyp** to build itself
* Added Japanese readme

## Supported Font Type

### Import

ttf, ttc, otf, woff, woff2

### Output

ttf, woff, woff2

## How to use

1.  ~~~
    npm install grunt-fontmin-ex --save-dev
    ~~~
2. Add configuration in Gruntfile.js

### Configuration
```JavaScript
grunt.initConfig({
  fontmin: {
    options: {
      dest:    'www-bin/fonts/',  // default './'
      basedir: 'fonts/'           // default './'
      types:   ['ttf','woff','woff2'] // default
    },
    '{Source-hans*.otf}': {
      /* getText: (html) => string_of_characters_to_include
       * if not specified, use html-to-text
       */
      getText: getBody,
      src:  'www-bin/**/*.html'
    },
    'cn-cursive.ttf': {
      getText: getHeadings,
      src:  'www-bin/**/*.html'
    }
  }
})

grunt.loadNpmTasks('grunt-fontmin')
```

### options (task-wide)
* dest:
  * destination directory, include trailing slash
  * default: `./`
* basedir:
  * source font directory, include trailing slash
  * default: `./`
* types:
  * `*Array*`.
  * output extention(s)
  * 'ttf', 'woff', 'woff2' are supported.

### target options
* grunt's target name
  * relative to `basedir`, pattern of fonts to minimize
  * pass to `grunt.file.expand()`
* src:
  * pattern of files, relative to `Gruntfile`
  * src's content is passed to getText, it returns characters to included in minimized font
* getText:
  * filter function: (htmlContent) => string_of_chars_to_include
  * if not provided, use builtin `html-to-text`
  * you can write your own
* woff:
  * output compressed woff, anything other than `undefined`
  * default if no other output option is provided (like `css`)


## Information

You can't change output filename

**You are responsible to get proper license of fonts you minify!**  

or consider [free fonts](http://zenozeng.github.io/Free-Chinese-Fonts/) 

or [The 🇯🇵 Web Fonts](https://tmin.xyz/The-Japanese-Web-Fonts/)

## License
MIT (C) wacky6
MIT (C) tamaina