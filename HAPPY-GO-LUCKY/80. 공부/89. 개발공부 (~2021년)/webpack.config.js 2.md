---
Created: Invalid date
Updated: Invalid date
---
const HtmlWebpackPlugin = require("html-webpack-plugin");

const MiniCssExtractPlugin = require("mini-css-extract-plugin");

const VueLoaderPlugin = require("vue-loader/lib/plugin");

const path = require('path');

function resolve (dir) {

return path.join(__dirname, '/', dir)

}

module.exports = (env) => {

let clientPath = path.resolve(__dirname, './src')

let outputPath = path.resolve(__dirname, './dist')

return {

mode: !env ? 'development' : env,

entry: {

index: clientPath + '/index.js'

},

output: {

path: outputPath,

publicPath: '/',

filename: '[name].js'

},

module: {

rules: [

{

test: /\.js$/,

exclude: /node_modules/,

use: {loader: "babel-loader"}

}, {

test: /\.html$/,

use: [{

loader: "html-loader",

options: {minimize: true}

}]

}, {

test: /\.(sa|sc|c)ss$/,

use: [

!env ? 'style-loader' : MiniCssExtractPlugin.loader,

'css-loader'

]

}, {

test: /\.vue$/,

loader: "vue-loader"

}]

},

resolve: {

alias: {

"vue$": "vue/dist/vue.esm.js",

"@": resolve('src')

},

extensions: ['*', '.js', '.vue', '.json']

},

devServer: {

historyApiFallback: true,

port:8788,

inline: true, //컴파일 된 코드를 일반적인 template html에 삽입하는 모드. iframe에 넣어 업데이트하는 iframe모드가 있다.

host: '0.0.0.0'

},

plugins: [

new HtmlWebpackPlugin({

template: "./src/index.html",

filename: "./index.html"

}),

new MiniCssExtractPlugin({

filename: "[name].css",

chunkFilename: "[id].css"

}),

new VueLoaderPlugin()

]

}

}