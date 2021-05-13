# Webpack 5 build  

*A webpack 5 build to boost your front-end development experience*

## Installation
1. Start new project by clicking on "Use this template" button

2. Clone your repo and open it in your code editor

3. Install dependencies
```bash
npm i
```
4. Start a development server
```bash
npm start
```
5. Compress your images:
```bash
npm run jpgmin
```
  Or convert them to WebP:
```bash
npm run towebp
```
6. Create a production build
```bash
npm run build
```

## Features
 
### HTML 
  - auto-injection of JS and CSS | html-webpack-plugin
  - easy configuration for multipage site
    - in webpack/parts/loadHtml.js duplicate "new HtmlWebpackPlugin({..})" for every page you have
    - ```chunks: ['index']``` are your entry JS file, leave the same if you need one JS for all the pages 
    - ```filename: 'index.html'``` is required to be different for every page you create

### CSS
  - CSS and Scss loaders (you will have to add a Sass loader manually if you need it) 
  - inline CSS in development mode without all the optimizations listed below
  - separate CSS file in production build with hash | mini-css-extract-plugin
  - PostCSS plugins:
    - Tree Shacking | purgecss
    - sanitize.css / normalize.css to reset browser's default CSS | postcss-normalize
    - autoprefixer and experimental css transpilation | postcss-preset-env
    - [various optimizations](https://cssnano.co/docs/what-are-optimisations/) | nanocss
      -  sorter
      -  duplicates / comments / empty selectors discarding
      -  merge rules
      -  minification
      -  normalization
      -  etc 
    - implementation of Scss's
      - nested syntax | postcss-nested
      - variables, conditionals, and iterators | postcss-advanced-variables

### JavaScript
  - transpilation back to ES5 (babel) if the conditions are met
    - can be [configured in "browserslist"](https://github.com/browserslist/browserslist#full-list) option in package.json
    - the defaults are:  "> 0.25%", "not dead", "last 2 versions", "IE 11"
  - Bundle Splitting - separate main.js, vendor.js and runtime.js files with caching
  - Tree Shacking / Dead code elimination
  - minification

### Assets handling
Assets loaders configured for this build:
  - fonts: eot, otf, ttf, woff, 
  - images: jpeg, jpg, webp, ico, png, svg, gif  
   
Integrated **images compression** with just one script using Google's [Squoosh](https://squoosh.app)
  - run ```npm run jpgmin``` to 
    - compress everything inside /src/assets/images folder
    - replace the old files with the new compressed ones
      - do NOT create subfolders inside /images - the script will break!
  - run ```npm run towebp``` to 
    - convert everything inside /src/assets/images to WebP format 
    - place it into a dedicated ./src/assets/webp folder

### Webpack configuration
  - are split into a common / dev / prod files
  - loaders are in webpack/parts folder for easy configuration and clear look
  - lightweight dev server with live reload | webpack-plugin-serve
  - progress bar in integrated terminal | webpackbar

---
### Contributions
If you find a bug, please file an issue. 
