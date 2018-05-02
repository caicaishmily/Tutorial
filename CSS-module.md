# CSS-module入门

标签（空格分隔）： 未分类

---
## 什么是CSS-Module ##
    CSS Modules 是功能很单纯，只加入了局部作用域和模块依赖，用来保证某个组件的样式，不会影响到其他组件
    
---
## 局部作用域

    
    CSS的规则都是全局的，任何一个组件的样式规则，都对整个页面有效。产生局部作用域的唯一方法，就是使用一个独一无二的class的名字，不会与其他选择器重名。这就是 CSS Modules 的做法。
    
    CSS Modules 提供各种插件，支持不同的构建工具。本文使用的是 Webpack 的css-loader插件，因为它对 CSS Modules 的支持最好，而且很容易使用。
    
        
        module.exports = {
          entry: __dirname + '/index.js',
          output: {
            publicPath: '/',
            filename: './bundle.js'
          },
          module: {
            loaders: [
              {
                test: /\.jsx?$/,
                exclude: /node_modules/,
                loader: 'babel',
                query: {
                  presets: ['es2015', 'stage-0', 'react']
                }
              },
              {
                test: /\.css$/,
                loader: "style-loader!css-loader?modules"
              },
            ]
          }
        };
        




