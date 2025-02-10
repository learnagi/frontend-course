# HTML 引用和引用元素
<!DOCTYPE html>
<html>
<body>

<p>以下是 WWF 网站上的一段引述：</p>

<blockquote cite="http://www.worldwildlife.org/who/index.html">
60 年来，WWF 一直致力于帮助人类和自然繁荣发展。作为世界领先的保护组织，WWF 在近 100 个国家/地区开展工作。在各个层面，我们与世界各地的人们合作，开发和提供创新的解决方案，以保护社区、野生动物及其生活的地方。
</blockquote>

</body>
</html>

# HTML < blockquote > 用于报价

HTML
元素定义从其他来源引用的章节。

浏览器通常会缩进 < blockquote > 元素。
<!DOCTYPE html>
<html>
<body>

<p>以下是 WWF 网站上的一段引述：</p>

<blockquote cite="http://www.worldwildlife.org/who/index.html">
60 年来，WWF 一直致力于帮助人类和自然繁荣发展。作为世界领先的保护组织，WWF 在近 100 个国家/地区开展工作。在各个层面，我们与世界各地的人们合作，开发和提供创新的解决方案，以保护社区、野生动物及其生活的地方。
</blockquote>

</body>
</html>

# HTML <q> 用于简短的引用

<!DOCTYPE html>
<html>
<body>

<p>浏览器通常在 q 元素周围插入引号。

</p>

<p>WWF 的目标是： 构建人类与自然和谐相处的未来。<q>构建人类与自然和谐相处的未来。</q></p>

</body>
</html>

# HTML <abbr> 用于缩写
HTML 标记定义缩写或首字母缩略词，如“HTML”、“CSS”、“Mr.”、“Dr.”、“ASAP”、“ATM”。

标记缩写可以为浏览器、翻译系统和搜索引擎提供有用的信息。

提示： 将鼠标悬停在元素上时，使用全局 title 属性可显示缩写/首字母缩略词的描述。

<!DOCTYPE html>
<html>
<body>

<p>The <abbr title="World Health Organization">WHO</abbr> was founded in 1948.</p>

<p>Marking up abbreviations can give useful information to browsers, translation systems and search-engines.</p>

</body>
</html>

# HTML <address> 用于标注作者地址
HTML
标记定义文档或文章的作者/所有者的联系信息。

联系信息可以是电子邮件地址、URL、实际地址、电话号码、社交媒体用户名等。

元素中的文本
通常以斜体呈现，浏览器总是会在元素前后添加换行符。

<!DOCTYPE html>
<html>
<body>

<p>The HTML address element defines contact information (author/owner) of a document or article.</p>

<address>
Written by John Doe.<br> 
Visit us at:<br>
Example.com<br>
Box 564, Disneyland<br>
USA
</address>

</body>
</html>

# 作品标题的 HTML <cite>

HTML 标签定义了创意作品的标题（例如，一本书、一首诗、一首歌、一部电影、一幅画、一个雕塑等）。

注意：一个人的名字不是作品的标题。

<cite> 元素中的文本通常以斜体呈现。

<!DOCTYPE html>
<html>
<body>

<p>The HTML cite element defines the title of a work.</p>
<p>Browsers usually display cite elements in italic.</p>

<img src="img_the_scream.jpg" width="220" height="277" alt="The Scream">
<p><cite>The Scream</cite> by Edvard Munch. Painted in 1893.</p>

</body>
</html>

# HTML <bdo> 用于双向覆盖

BDO 代表 Bi-Directional Override。

HTML 标签用于覆盖当前文本方向：
<!DOCTYPE html>
<html>
<body>

<p>If your browser supports bi-directional override (bdo), the next line will be written from right to left (rtl):</p>

<bdo dir="rtl">This line will be written from right to left</bdo>

</body>
</html>


