# HTML 颜色
HTML 颜色是使用预定义的颜色名称或 RGB、HEX、HSL、RGBA 或 HSLA 值指定的。

<!DOCTYPE html>
<html>
<body>

<h1 style="background-color:Tomato;">番茄</h1>
<h1 style="background-color:Orange;">橙色</h1>
<h1 style="background-color:DodgerBlue;">道奇蓝</h1>
<h1 style="background-color:MediumSeaGreen;">绿色</h1>
<h1 style="background-color:Gray;">灰色</h1>
<h1 style="background-color:SlateBlue;">石板蓝</h1>
<h1 style="background-color:Violet;">紫色</h1>
<h1 style="background-color:LightGray;">浅灰色</h1>

</body>
</html>

## 背景颜色
可以设置 HTML 元素的背景颜色

<!DOCTYPE html>
<html>
<body>

<h1 style="background-color:DodgerBlue;">Hello World</h1>

<p style="background-color:Tomato;">
Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat.
Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
</p>

</body>
</html>

## 文字颜色
可以设置文本的颜色

<!DOCTYPE html>
<html>
<body>

<h3 style="color:Tomato;">Hello World</h3>

<p style="color:DodgerBlue;">Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat.</p>

<p style="color:MediumSeaGreen;">Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.</p>

</body>
</html>

## 边框颜色
可以设置边框的颜色
<!DOCTYPE html>
<html>
<body>

<h1 style="border: 2px solid Tomato;">Hello World</h1>

<h1 style="border: 2px solid DodgerBlue;">Hello World</h1>

<h1 style="border: 2px solid Violet;">Hello World</h1>

</body>
</html>

## 颜色值
在 HTML 中，还可以使用 RGB 值、HEX 值、HSL 值、RGBA 值和 HSLA 值指定颜色。

<!DOCTYPE html>
<html>
<body>

<p>Same as color name "Tomato":</p>

<h1 style="background-color:rgb(255, 99, 71);">rgb(255, 99, 71)</h1>
<h1 style="background-color:#ff6347;">#ff6347</h1>
<h1 style="background-color:hsl(9, 100%, 64%);">hsl(9, 100%, 64%)</h1>

<p>Same as color name "Tomato", but 50% transparent:</p>
<h1 style="background-color:rgba(255, 99, 71, 0.5);">rgba(255, 99, 71, 0.5)</h1>
<h1 style="background-color:hsla(9, 100%, 64%, 0.5);">hsla(9, 100%, 64%, 0.5)</h1>

<p>In addition to the predefined color names, colors can be specified using RGB, HEX, HSL, or even transparent colors using RGBA or HSLA color values.</p>

</body>
</html>

# HTML RGB和RGBA颜色
RGB 颜色值表示 RED、GREEN、BLUE光源。<BR>
RGBA颜色值是RGB的扩展，具有Alpha通道(不透明度)

## RGB 颜色值

在 HTML 中，可以使用以下公式将颜色指定为 RGB 值：

RGB（红、绿、蓝）

每个参数（红色、绿色和蓝色）定义颜色的强度，其值介于 0 和 255 之间。

这意味着有 256 x 256 x 256 = 16777216 种可能的颜色！

例如，rgb（255， 0， 0） 显示为红色，因为 red 设置为其最高值 （255），而其他两个值（绿色和蓝色）设置为 0。

另一个示例是 rgb（0， 255， 0） 显示为绿色，因为绿色设置为其最高值 （255），而其他两个值（红色和蓝色）设置为 0。

要显示黑色，请将所有颜色参数设置为 0，如下所示：rgb（0， 0， 0）。

要显示白色，请将所有颜色参数设置为 255，如下所示：rgb（255， 255， 255）。

<!DOCTYPE html>
<html>
<body>

<h1 style="background-color:rgb(255, 0, 0);">rgb(255, 0, 0)</h1>
<h1 style="background-color:rgb(0, 0, 255);">rgb(0, 0, 255)</h1>
<h1 style="background-color:rgb(60, 179, 113);">rgb(60, 179, 113)</h1>
<h1 style="background-color:rgb(238, 130, 238);">rgb(238, 130, 238)</h1>
<h1 style="background-color:rgb(255, 165, 0);">rgb(255, 165, 0)</h1>
<h1 style="background-color:rgb(106, 90, 205);">rgb(106, 90, 205)</h1>

</body>
</html>

# 灰度
灰色阴影通常使用所有三个参数的相等值来定义：

<!DOCTYPE html>
<html>
<body>

<h1 style="background-color:rgb(60, 60, 60);">rgb(60, 60, 60)</h1>
<h1 style="background-color:rgb(100, 100, 100);">rgb(100, 100, 100)</h1>
<h1 style="background-color:rgb(140, 140, 140);">rgb(140, 140, 140)</h1>
<h1 style="background-color:rgb(180, 180, 180);">rgb(180, 180, 180)</h1>
<h1 style="background-color:rgb(200, 200, 200);">rgb(200, 200, 200)</h1>
<h1 style="background-color:rgb(240, 240, 240);">rgb(240, 240, 240)</h1>

</body>
</html>

# RGBA 颜色值
 RGBA 颜色值是 RGB 颜色值的扩展，具有 Alpha 通道 - 指定颜色的不透明度。

RGBA 颜色值通过以下方式指定：


## RGBA（红、绿、蓝、alpha）
alpha 参数是一个介于 0.0（完全透明）和 1.0（完全不透明）之间的数字：

<!DOCTYPE html>
<html>
<body>

<h1 style="background-color:rgba(255, 99, 71, 0);">rgba(255, 99, 71, 0)</h1>
<h1 style="background-color:rgba(255, 99, 71, 0.2);">rgba(255, 99, 71, 0.2)</h1>
<h1 style="background-color:rgba(255, 99, 71, 0.4);">rgba(255, 99, 71, 0.4)</h1>
<h1 style="background-color:rgba(255, 99, 71, 0.6);">rgba(255, 99, 71, 0.6)</h1>
<h1 style="background-color:rgba(255, 99, 71, 0.8);">rgba(255, 99, 71, 0.8)</h1>
<h1 style="background-color:rgba(255, 99, 71, 1);">rgba(255, 99, 71, 1)</h1>

</body>
</html>

# 十六进制

十六进制颜色的指定方式为：#RRGGBB，其中 RR（红色）、GG（绿色）和 BB（蓝色）十六进制整数指定颜色的组成部分。

## 十六进制颜色值

在 HTML 中，可以使用表单中的十六进制值指定颜色：

### rrggbb
其中 rr （红色）、gg （绿色） 和 bb （蓝色） 是介于 00 和 ff 之间的十六进制值 （与十进制 0-255 相同）。

例如，#ff0000 显示为红色，因为 red 设置为其最高值 （ff），而其他两个值（green 和 blue）设置为 00。

另一个示例，#00ff00 显示为绿色，因为绿色设置为其最高值 （ff），而其他两个值（红色和蓝色）设置为 00。

<!DOCTYPE html>
<html>
<body>

<h1 style="background-color:#ff0000;">#ff0000</h1>
<h1 style="background-color:#0000ff;">#0000ff</h1>
<h1 style="background-color:#3cb371;">#3cb371</h1>
<h1 style="background-color:#ee82ee;">#ee82ee</h1>
<h1 style="background-color:#ffa500;">#ffa500</h1>
<h1 style="background-color:#6a5acd;">#6a5acd</h1>

</body>
</html>

## 灰度
灰色阴影通常使用所有三个参数的相等值来定义：
<!DOCTYPE html>
<html>
<body>

<h1 style="background-color:#404040;">#404040</h1>
<h1 style="background-color:#686868;">#686868</h1>
<h1 style="background-color:#a0a0a0;">#a0a0a0</h1>
<h1 style="background-color:#bebebe;">#bebebe</h1>
<h1 style="background-color:#dcdcdc;">#dcdcdc</h1>
<h1 style="background-color:#f8f8f8;">#f8f8f8</h1>

</body>
</html>

# HSL

## HTML HSL 和 HSLA 颜色

HSL 代表色相、饱和度和亮度。

HSLA 颜色值是 HSL 的扩展，具有 Alpha 通道（不透明度）。

## HSL 颜色值
在 HTML 中，可以使用表单中的色相、饱和度和亮度 （HSL） 指定颜色：

### HSL（色相、饱和度、亮度）
色相是色轮上从 0 到 360 的度数。0 为红色，120 为绿色，240 为蓝色。

饱和度是一个百分比值。0% 表示灰色阴影，100% 是全色。

亮度也是一个百分比值。0% 是黑色，100% 是白色。

<!DOCTYPE html>
<html>
<body>

<h1 style="background-color:hsl(0, 100%, 50%);">hsl(0, 100%, 50%)</h1>
<h1 style="background-color:hsl(240, 100%, 50%);">hsl(240, 100%, 50%)</h1>
<h1 style="background-color:hsl(147, 50%, 47%);">hsl(147, 50%, 47%)</h1>
<h1 style="background-color:hsl(300, 76%, 72%);">hsl(300, 76%, 72%)</h1>
<h1 style="background-color:hsl(39, 100%, 50%);">hsl(39, 100%, 50%)</h1>
<h1 style="background-color:hsl(248, 53%, 58%);">hsl(248, 53%, 58%)</h1>

</body>
</html>



## 饱和
饱和度可以描述为颜色的强度。

100% 是纯色，没有灰色阴影。

50% 是 50% 灰色，但您仍然可以看到颜色。

0% 完全为灰色;您无法再看到颜色。


<!DOCTYPE html>
<html>
<body>

<h1 style="background-color:hsl(0, 100%, 50%);">hsl(0, 100%, 50%)</h1>
<h1 style="background-color:hsl(0, 80%, 50%);">hsl(0, 80%, 50%)</h1>
<h1 style="background-color:hsl(0, 60%, 50%);">hsl(0, 60%, 50%)</h1>
<h1 style="background-color:hsl(0, 40%, 50%);">hsl(0, 40%, 50%)</h1>
<h1 style="background-color:hsl(0, 20%, 50%);">hsl(0, 20%, 50%)</h1>
<h1 style="background-color:hsl(0, 0%, 50%);">hsl(0, 0%, 50%)</h1>

<p>With HSL colors, less saturation mean less color. 0% is completely gray.</p>

</body>
</html>

## 亮度

颜色的亮度可以描述为您想要赋予颜色多少光，其中 0% 表示无光（黑色），50% 表示 50% 亮（既不暗也不亮），100% 表示完全亮（白色）。

<!DOCTYPE html>
<html>
<body>

<h1 style="background-color:hsl(0, 100%, 0%);">hsl(0, 100%, 0%)</h1>
<h1 style="background-color:hsl(0, 100%, 25%);">hsl(0, 100%, 25%)</h1>
<h1 style="background-color:hsl(0, 100%, 50%);">hsl(0, 100%, 50%)</h1>
<h1 style="background-color:hsl(0, 100%, 75%);">hsl(0, 100%, 75%)</h1>
<h1 style="background-color:hsl(0, 100%, 90%);">hsl(0, 100%, 90%)</h1>
<h1 style="background-color:hsl(0, 100%, 100%);">hsl(0, 100%, 100%)</h1>

<p>对于 HSL 颜色，0% 亮度表示黑色，100 亮度表示白色。</p>

</body>
</html>

## 灰度
 
 灰色阴影通常通过将色相和饱和度设置为 0 来定义，并将亮度从 0% 调整到 100% 以获得更暗/更亮的阴影：

 <!DOCTYPE html>
<html>
<body>

<h1 style="background-color:hsl(0, 0%, 20%);">hsl(0, 0%, 20%)</h1>
<h1 style="background-color:hsl(0, 0%, 30%);">hsl(0, 0%, 30%)</h1>
<h1 style="background-color:hsl(0, 0%, 40%);">hsl(0, 0%, 40%)</h1>
<h1 style="background-color:hsl(0, 0%, 60%);">hsl(0, 0%, 60%)</h1>
<h1 style="background-color:hsl(0, 0%, 70%);">hsl(0, 0%, 70%)</h1>
<h1 style="background-color:hsl(0, 0%, 90%);">hsl(0, 0%, 90%)</h1>

</body>
</html>

## HSLA  颜色值
HSLA 颜色值是 HSL 颜色值的扩展，具有 Alpha 通道 - 指定颜色的不透明度。

HSLA 颜色值由以下项指定：

### HSLA（色相、饱和度、亮度、Alpha）
alpha 参数是一个介于 0.0（完全透明）和 1.0（完全不透明）之间的数字：

<!DOCTYPE html>
<html>
<body>

<h1 style="background-color:hsla(9, 100%, 64%, 0);">hsla(9, 100%, 64%, 0)</h1>
<h1 style="background-color:hsla(9, 100%, 64%, 0.2);">hsla(9, 100%, 64%, 0.2)</h1>
<h1 style="background-color:hsla(9, 100%, 64%, 0.4);">hsla(9, 100%, 64%, 0.4)</h1>
<h1 style="background-color:hsla(9, 100%, 64%, 0.6);">hsla(9, 100%, 64%, 0.6)</h1>
<h1 style="background-color:hsla(9, 100%, 64%, 0.8);">hsla(9, 100%, 64%, 0.8)</h1>
<h1 style="background-color:hsla(9, 100%, 64%, 1);">hsla(9, 100%, 64%, 1)</h1>

</body>
</html>

















