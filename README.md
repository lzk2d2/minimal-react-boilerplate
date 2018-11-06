1.
mkdir minimal-react-boilerplate
cd minimal-react-boilerplate

2.
npm init -y

3. optional
npm config list

4.
mkdir dist
cd dist
vi dist/index.html
<!DOCTYPE html>
<html>
  <head>
    <title>The Minimal React Webpack Babel Setup</title>
  </head>
  <body>
    <div id="app"></div>
    <script src="/bundle.js"></script>
  </body>
</html>

5.
webpack: module bundler and build tool
webpack-dev-server: server the app in a localhost
webpack-cli: configure Webpack setup in a config file
npm install --save-dev webpack webpack-dev-server webpack-cli

6.
package.json
"scripts": {
  "start": "webpack-dev-server --config ./webpack.config.js --mode development",
  ...
},
...

7.
vi webpack.config.js
module.exports = {
  entry: './src/index.js',
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: ['babel-loader']
      }
    ]
  },
  resolve: {
    extensions: ['*', '.js', '.jsx']
  },
  output: {
    path: __dirname + '/dist',
    publicPath: '/',
    filename: 'bundle.js'
  },
  devServer: {
    contentBase: './dist'
  },
  serve: {
    port: 8081
  }
};

8.
mkdir src
cd src
vi src/index.js
console.log('My Minimal React Webpack Babel Setup');

9.
babel: enables old and new JavaScript language feature in most browser
npm install --save-dev @babel/core @babel/preset-env

10.
babel-loader: hook Babel with Webpack
npm install --save-dev babel-loader

11.
babel/preset-react: configuration to transfort the React's JSX syntax to vanilla JavaSrcript
npm install --save-dev @babel/preset-react

12.
babel configuration: .babelrc
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react"
  ]
}

13.
react+react-dom: to use react stuff...
npm install --save react react-dom

14.
src/index.js
import React from 'react';
import ReactDOM from 'react-dom';

const title = 'My Minimal React Webpack Babel Setup';

ReactDOM.render(
  <div>{title}</div>,
  document.getElementById('app')
);

15.
react-hot-loader: prohibits reloading the entire page, once the app was changed
npm install --save-dev react-hot-loader

16.
webpack.config.js
const webpack = require('webpack');
module.exports = {
  ...,
  plugins: [
    new webpack.HotModuleReplacementPlugin()
  ],
  devServer: {
    contentBase: './dist',
    hot: true
  }
}

16.
npm start