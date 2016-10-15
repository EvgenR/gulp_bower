В gulpfile.js мы будем писать таски для gulp.
В bower.json — сохранять зависимости проекта, a в
package.json будет сохранять все необходимые для разработки модули npm.

Искать пакеты
https://bower.io/search/

Генератор 
http://yeoman.io/generators/

----- BOWER ----
Инициализация Bower пакета. Файл манифест bower.json.
bower init


Поиск пакета: bower s jquery
Установка:
    
bower install jquery#1.6.4
bower i normalize.css
bower i jquery --save
bower i jquery -S
bower i zepto --save-dev
bower i zepto -D

Что установлено
    
bower list
bower list --path

Обновление
bower update jquery

Удаление
bower uninstall jquery
bower uninstall jquery normalizr.css -S
bower uninstall zepto -D

.bowerrc  - файл в котором указан путь до документов

{
"directory" : "app/bower"
}

mkdir app
mv bower_components app/bower

----- GULP -----

--Плагины
-main-bower-files
Данный плагин предлагает нам один из путей избавления от лишних файлов,
а точнее поможет нам извлечь из всех сотен файлов скаченных bower’ом в папку bower_components 
только нужные нам файлы.


var gulp = require('gulp');
var mainBowerFiles = require('main-bower-files');

gulp.task('mainfiles', function() {
    return gulp.src(mainBowerFiles())
    .pipe(gulp.dest('dist/mainfiles'))
});

npm i main-bower-files -D

Обязательно укажем место назначения — куда будут складываться главные файлы.
Место вы выбираете сами. В моём случае это будет папка dist/mainfiles

.pipe(gulp.dest('dist/mainfiles'))
    
gulp mainfiles

Переопределим главные файлы для bootstrap прямо внутри gulp таска:

gulp.task('mainfiles', function() {
    return gulp.src(mainBowerFiles({
      "overrides": {
        "bootstrap": {
            "main": [
                "./dist/js/bootstrap.min.js",
                "./dist/css/bootstrap.min.css",
                "./dist/css/bootstrap-theme.min.css"
                ]
        }
    }}))
    .pipe(gulp.dest('dist/mainfiles'))
  });

или внутри bower.json
"overrides": {
  "bootstrap": {
      "main": [
          "./dist/js/bootstrap.min.js",
          "./dist/css/bootstrap.min.css",
          "./dist/css/bootstrap-theme.min.css"
          ]
  }
}


------- ССЫЛКИ -----------
http://loftblog.ru/material/bower-podrobnoe-rukovodstvo-1/
