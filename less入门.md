LESS 简介:
  LESS 将 CSS 赋予了动态语言的特性，如 变量， 继承， 运算， 函数. LESS 既可以在 客户端 上运行 (支持 IE 6+, Webkit, Firefox),也可以借助 Node.js 或者 Rhino 在服务端运行。

变量
  变量允许我们单独定义一系列通用的样式，然后在需要的时候去调用。所以在做全局样式调整的时候我们可能只需要修改几行代码就可以了。
  例如:
    @nice-blue: #ccc;
    @light-blue: @nice-blue + #111;

    #header { color: @nice-blue; }
    输出为:
    #header { color: #ccc; } 

混合
  在 LESS 中我们可以定义一些通用的属性集为一个class，然后在另一个class中去调用这些属性.
  任何 CSS class, id 或者 元素 属性集都可以以同样的方式引入. 下面有这样一个class:
    .bordered { border: 1px solid red }
  那如果我们现在需要在其他class中引入那些通用的属性集，那么我们只需要在任何class中像下面这样调用就可以了:
    #menu a {
      color: #111;
      .bordered;
    }
    .post a {
      color: red;
      .bordered;
    }
  .bordered class里面的属性样式都会在 #menu a 和 .post a中体现出来

带参数混合
  在 LESS 中，你还可以像函数一样定义一个带参数的属性集合,还可以给参数设置默认值:
    .border-radius(@radius:5px) {
      border-radius: @radius;
      -moz-border-radius: @radius;
      -webkit-border-radius: @radius;
    }
  然后在其他class中像这样调用
    #header {
      .border-radius();
    }
    .button {
      .border-radius(6px);  
    }

@arguments 变量
  @arguments包含了所有传递进来的参数. 如果你不想单独处理每一个参数的话就可以像这样写:
    .box-shadow (@x: 0, @y: 0, @blur: 1px, @color: #000) {
      box-shadow: @arguments;
      -moz-box-shadow: @arguments;
      -webkit-box-shadow: @arguments;
    }
    .box-shadow(2px, 5px);

模式匹配和导引表达式
  有些情况下，我们想根据传入的参数来改变混合的默认呈现，比如下面这个例子：
    .mixin (@s, @color) { ... }

    .class {
      .mixin(@switch, #888);
    }
  如果想让.mixin根据不同的@switch值而表现各异，如下这般设置：
    .mixin (dark, @color) {
      color: darken(@color, 10%);
    }
    .mixin (light, @color) {
      color: lighten(@color, 10%);
    }
    .mixin (@_, @color) {
      display: block;
    }
  引导
    当我们想根据表达式进行匹配，而非根据值和参数匹配时，导引就显得非常有用。
    为了尽可能地保留CSS的可声明性，LESS通过导引混合而非if/else语句来实现条件判断，因为前者已在@media query特性中被定义。

    以此例做为开始：
      .mixin (@a) when (lightness(@a) >= 50%) {
        background-color: black;
      }
      .mixin (@a) when (lightness(@a) < 50%) {
        background-color: white;
      }
      .mixin (@a) {
        color: @a;
      }
    when关键字用以定义一个导引序列(此例只有一个导引)。接下来我们运行下列代码：
      .class1 { .mixin(#ddd) }
      .class2 { .mixin(#555) }
    就会得到：
      .class1 {
        background-color: black;
        color: #ddd;
      }
      .class2 {
        background-color: white;
        color: #555;
      }
    导引中可用的全部比较运算有： > >= = =< <。此外，关键字true只表示布尔真值，下面两个混合是相同的：
      .truth (@a) when (@a) { ... }
      .truth (@a) when (@a = true) { ... }
    除去关键字true以外的值都被视示布尔假：
      .class {
        .truth(40); // Will not match any of the above definitions.
      }
    导引序列使用逗号‘,’—分割，当且仅当所有条件都符合时，才会被视为匹配成功。
      .mixin (@a) when (@a > 10), (@a < -10) { ... }
    导引可以无参数，也可以对参数进行比较运算：
      @media: mobile;
      .mixin (@a) when (@media = mobile) { ... }
      .mixin (@a) when (@media = desktop) { ... }
      .max (@a, @b) when (@a > @b) { width: @a }
      .max (@a, @b) when (@a < @b) { width: @b }
    最后，如果想基于值的类型进行匹配，我们就可以使用is*函式：
      .mixin (@a, @b: 0) when (isnumber(@b)) { ... }
      .mixin (@a, @b: black) when (iscolor(@b)) { ... }
    下面就是常见的检测函式：
      iscolor
      isnumber
      isstring
      iskeyword
      isurl
    如果你想判断一个值是纯数字，还是某个单位量，可以使用下列函式：
      ispixel
      ispercentage
      isem
    最后再补充一点，在导引序列中可以使用and关键字实现与条件：
      .mixin (@a) when (isnumber(@a)) and (@a > 0) { ... }
    使用not关键字实现或条件
     .mixin (@b) when not (@b > 0) { ... }

嵌套规则
  LESS 可以让我们以嵌套的方式编写层叠样式. 让我们先看下面这段 CSS:
    #header { color: black; }
    #header .navigation {
      font-size: 12px;
    }
    #header .logo { 
      width: 300px; 
    }
    #header .logo:hover {
      text-decoration: none;
    }
  在 LESS 中, 我们就可以这样写:
    #header {
      color: black;
      .navigation {
        font-size: 12px;
      }
      .logo {
        width: 300px;
        &:hover { text-decoration: none }
      }
    }

运算
  任何数字、颜色或者变量都可以参与运算. 来看一组例子:
    @base: 5%;
    @filler: @base * 2;
    @other: @base + @filler;
    color: #888 / 4;
    background-color: @base-color + #111;
    height: 100% / 2 + @filler;
  LESS 的运算已经超出了我们的期望，它能够分辨出颜色和单位。如果像下面这样单位运算的话:
    @var: 1px + 5;
    LESS 会输出 6px.
  括号也同样允许使用:
    width: (@var + 5) * 2;
  并且可以在复合属性中进行运算:
    border: (@width * 2) solid black;

Color 函数
  LESS 提供了一系列的颜色运算函数. 颜色会先被转化成 HSL 色彩空间, 然后在通道级别操作:
    lighten(@color, 10%);     
    darken(@color, 10%);      
    saturate(@color, 10%);    
    desaturate(@color, 10%);  
    fadein(@color, 10%);      
    fadeout(@color, 10%);     
    fade(@color, 50%);        
    spin(@color, 10);         
    spin(@color, -10);        
    mix(@color1, @color2);    
  使用起来相当简单:
    @base: #f04615;
    .class {
      color: saturate(@base, 5%);
      background-color: lighten(spin(@base, 8), 25%);
    }
  你还可以提取颜色信息:
    hue(@color);        
    saturation(@color); 
    lightness(@color);  
  如果你想在一种颜色的通道上创建另一种颜色，这些函数就显得那么的好用，例如:
    @new: hsl(hue(@old), 45%, 90%);
    @new 将会保持 @old的 色调, 但是具有不同的饱和度和亮度.

Math 函数
  LESS提供了一组方便的数学函数，你可以使用它们处理一些数字类型的值:
    round(1.67); 
    ceil(2.4);   
    floor(2.6);  
  如果你想将一个值转化为百分比，你可以使用percentage 函数:
    percentage(0.5); 

命名空间
  有时候，你可能为了更好组织CSS或者单纯是为了更好的封装，将一些变量或者混合模块打包起来, 你可以像下面这样在#bundle中定义一些属性集之后可以重复使用:
    #bundle {
      .button () {
        display: block;
        border: 1px solid black;
        background-color: grey;
        &:hover { background-color: white }
      }
      .tab { ... }
      .citation { ... }
    }
  你只需要在 #header a中像这样引入 .button:
    #header a {
      color: orange;
      #bundle > .button;
    }

作用域
  LESS 中的作用域跟其他编程语言非常类似，首先会从本地查找变量或者混合模块，如果没找到的话会去父级作用域中查找，直到找到为止.
    @var: red;
    #page {
      @var: white;
      #header {
        color: @var; // white
      }
    }
    #footer {
      color: @var; // red  
    }

注释
  CSS 形式的注释在 LESS 中是依然保留的:
    /* Hello, I'm a CSS-style comment */
    .class { color: black }
  LESS 同样也支持双斜线的注释, 但是编译成 CSS 的时候自动过滤掉:
    // Hi, I'm a silent comment, I won't show up in your CSS
    .class { color: white }

Importing
  你可以在main文件中通过下面的形式引入 .less 文件, .less 后缀可带可不带:
    @import "lib.less";
    @import "lib";
  如果你想导入一个CSS文件而且不想LESS对它进行处理，只需要使用.css后缀就可以:
    @import "lib.css";
  这样LESS就会跳过它不去处理它.

字符串插值
  变量可以用类似ruby和php的方式嵌入到字符串中，像@{name}这样的结构:
    @base-url: "http://assets.fnord.com";
    background-image: url("@{base-url}/images/bg.png");
  避免编译
  有时候我们需要输出一些不正确的CSS语法或者使用一些 LESS不认识的专有语法.
  要输出这样的值我们可以在字符串前加上一个 ~, 例如:
    .class {
      filter: ~"ms:alwaysHasItsOwnSyntax.For.Stuff()";
    }
  我们可以将要避免编译的值用 “”包含起来，输出结果为:
    .class {
      filter: ms:alwaysHasItsOwnSyntax.For.Stuff();
    }

JavaScript 表达式
  JavaScript 表达式也可以在.less 文件中使用. 可以通过反引号的方式使用:
    @var: `"hello".toUpperCase() + '!'`;
  输出:
    @var: "HELLO!";
  注意你也可以同时使用字符串插值和避免编译:
    @str: "hello";
    @var: ~`"@{str}".toUpperCase() + '!'`;
  输出:
    @var: HELLO!;
  它也可以访问JavaScript环境:
    @height: `document.body.clientHeight`;
  如果你想将一个JavaScript字符串解析成16进制的颜色值, 你可以使用 color 函数:
    @color: color(`window.colors.baseColor`);
    @darkcolor: darken(@color, 10%);
