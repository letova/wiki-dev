# Environment

## Start

Создаст package.json с настройками по умолчанию
```npm init -y```

## Git

```git init```
```touch .gitignore```

```git add .```
```git status```
```git commit -m "some change"```

```git push -u origin master```

## Babel

```npm install --save-dev babel-loader babel-core babel-preset-env```

## Jest

```npm install --save-dev jest```

**package.json**
```
{
  "scripts": {
    "test": "jest"
  }
}
```

С использованием ES6

```npm install --dev babel-jest```

**.babelrc**
```
{
  "presets": ["env", "react"]
}
```

## Webpack

Не рекомендуется ставить глобально, во избежание несовместимости версий
```npm install --save-dev webpack webpack-dev-server```

**package.json**
```
"scripts": {
  "build": "webpack",
  "start": "webpack-dev-server --output-public-path=/dist/"
}
```

**webpack.config.js**
```
const path = require('path'); //из node.js
module.exports = {
  devtool: 'source-map', //ссылка на исходники
  entry: './src/js/index.js',
  output: {
    filename: 'webdev.js',
    path: path.resolve(__dirname, 'dist')
  }
};
```

С использованием ES6

**webpack.config.js**
```
module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /(node_modules|bower_components)/,
        use: {
          loader: 'babel-loader',
          options: {presets: ['env']} //"react" 
        }
      }
    ]
}
```

## React

```npm install --save react react-dom```

Преобразования файлов .jsx в файлы .js
```npm install --save-dev babel-preset-react```

