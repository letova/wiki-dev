# Environment

## Start

Создаст package.json с настройками по умолчанию
```npm init -y```

## Git

```git init``` - создать репозиторий

```rm -r .git``` - удалить репозиторий

```touch .gitignore``` - создать .gitignore

```git add .``` -  добавить все файлы

```git rm —cached <file>``` - удалить файлы из add

```git status``` - статус

```git commit -m "some change"``` - коммит

```git commit -am "some change"``` - добавить минуя ```git add .```

```git commit —amend``` - прибавить к последнему коммиту

```git remote add origin https://github.com/username/repositoryname.git```

```git push -u origin master```

## Gulp

```sudo npm install gulp -g```
```npm install gulp -D```
```touch gulpfile.js```

**Сборка CSS**

```gulp-sass``` - CSS препроцессор/шаблонизатор
```gulp-stylus``` - альтернатива
```gulp-cssnano``` - CSS компрессор
```gulp-autoprefixer``` - автоматическое добавление вендорных префиксов.

**Сборка JS**

```gulp-uglify``` - JS компрессор
```gulp-concat``` - объединение JS

**Оптимизация изображений**

```gulp-imagemin`` - компрессор изображений
```imagemin-pngquant``` - PNG плагин для ```gulp-imagemin```
```gulp.spritesmith``` - объединяет изображения в спрайты, формирует вызов из CSS
```gulp-cache``` - формирует кэш из временных файлов, необходим для оптимизации работы с изображениями

**Оптимизация SVG изображений**

```gulp-svgmin``` - минификация SVG/SVGO
```gulp-svg-spritesheet``` - объединяет SVG изображения в спрайты, формирует вызов из CSS

**Автоматическая перезагрузка страницы браузера**

```browser-sync``` - сервер, перезагрузка страницы при внесении изменений
```gulp-livereload``` - альтернатива

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

