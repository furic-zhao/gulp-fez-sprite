## gulp-fez-sprite

> 自动合并雪碧图并自动生成对应的样式.(支持高清屏 @2x, @3x 图)

## 安装

```javascript
npm install gulp-fez-sprite --save-dev
npm install gulp-if --save-dev
```

## 使用

**gulpfile.js** 

```javascript
var gulpif = require('gulp-if');
var fezsprite = require('gulp-fez-sprite');

gulp.src('./src/css/*.less')
    .pipe(fezsprite())
    .pipe(gulpif('*.png', gulp.dest('./dist/sprite/'), gulp.dest('./dist/css/')));

```

**Options**
雪碧图路径

```javascript
var gulpif = require('gulp-if');
var fezsprite = require('gulp-fez-sprite');

gulp.src('./src/css/*.less')
    .pipe(fezsprite({slicePath: '../slice'}))
    .pipe(gulpif('*.png', gulp.dest('./dist/sprite/'), gulp.dest('./dist/css/')));

```

## 示例

**源码** -> `index.less`


```css
.icon-test {
  width: 32px;
  height: 32px;
  background-image: url(../slice/test.png);
}
```

**输出** -> `index.css`

```css
.icon-test {
  background-image: url(../sprite/index.png);
}

// Retina 2x supported
@media only screen and (-webkit-min-device-pixel-ratio: 2),
only screen and (min--moz-device-pixel-ratio: 2),
only screen and (-webkit-min-device-pixel-ratio: 2.5),
only screen and (min-resolution: 240dpi) {
.icon-test { 
  background-image:url("../sprite/index@2x.png");
  background-position: -36px -66px;
  background-size: 32px;
}
}
```

## 注意事项

* 两倍雪碧图的尺寸必须是偶数, 比如： `24x26@2x.png` 不能是： `23x27@2x.png`

