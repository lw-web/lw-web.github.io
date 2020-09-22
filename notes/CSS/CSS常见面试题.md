# CSS常见面试题

## IE盒模型和标准盒模型的区别

- IE盒模型的尺寸包括：内容区尺寸 + padding + margin
- 标准盒模型的尺寸只包括内容区的尺寸
- 对应CSS3属性：box-sizing：border-box、content-box

## 让元素在页面隐藏

- display：none
- visibility：hidden
- 区别
  - display：none 隐藏后的元素不占任何空间，visibility：hidden 依然占据元素尺寸的空间
  - visibility：hidden 具有继承性，给父元素设置 visibility：hidden，子元素也会继承，但是如果再给子元素设置 visibility：visible，子元素会重新显示出来，display：none 不会
  - visibility：hidden 属性不会影响计数器的计数，比如 ol - li 里面的自动计算
  - CSS3 里面的transition 支持 visibility属性，但并不支持 display

## 让元素在页面水平垂直居中

- flex实现  display：flex；justify-content：center；align-items：center；

```html
<!DOCTYPE html>
<head>
  <style>
    html, body {
      margin: 0;
      padding: 0;
    }
    #container {
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    #content {
      width: 50vw;
      height: 50vh;
      background-color: pink;      
    }
  </style>
</head>

<body>
  <div id='container'>
    <div id='content'></div>
  </div>
</body>
```

- 使用 position：fixed；然后上下左右都设置为 0，margin：auto

```html
<!DOCTYPE html>
<head>
  <style>
    html, body {
      margin: 0;
      padding: 0;
    }
    #container {
      height: 100vh;
    }
    #content {
      width: 50vw;
      height: 50vh;
      background-color: pink;
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      margin: auto;
    }
  </style>
</head>

<body>
  <div id='container'>
    <div id='content'></div>
  </div>
</body>
```

- position 和 transform 结合实现

```html
<!DOCTYPE html>
<head>
  <style>
    html, body {
      margin: 0;
      padding: 0;
    }
    #container {
      height: 100vh;
      position: relative;
    }
    #content {
      width: 50vw;
      height: 50vh;
      background-color: pink;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-25vw, -25vh)      
    }
  </style>
</head>

<body>
  <div id='container'>
    <div id='content'></div>
  </div>
</body>
```



































