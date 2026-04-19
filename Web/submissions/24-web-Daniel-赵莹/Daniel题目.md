# Write Up
## 一、[SWPUCTF 2021 新生赛]gift_F12
这道题考察 F12 开发者工具的使用，flag 藏在网页的前端 JS 代码中，通过查看网页源码（Ctrl+U），按Ctrl+F搜索就能直接获取
![1](题1.png)
![1](题1.2.png)
找到源码中flag

## 二、robots.txt
介绍：robots.txt：
它是一个纯文本文件，放在网站的根目录下（地址就是 域名/robots.txt），是网站给「搜索引擎爬虫」的一份访问规则说明书。
它的核心作用是：告诉搜索引擎哪些页面可以爬、哪些页面不要爬，避免网站的敏感内容被公开收录。
网站本意是 “不让搜索引擎看到敏感页面”
但它却把敏感页面的路径，写在了所有人都能看的 robots.txt 里，反而给攻击者提供了线索，也就是 CTF 里常说的 robots.txt 泄露漏洞
解题：
首先输入正确网址，添加\robots.txt
![2](题2.png)
发现Disallow 字段，会泄露网站的敏感路径，
访问这些被禁止的路径，就能拿到 flag
![2](题2.1.png)
再回到原登录页面获得flag
[2](题2.2.png)

## 三、[MoeCTF 2021]Web安全入门指北—GET
（向 AI 询问 GET/POST 请求，利用 AI 分析这段简单的php代码）

GET 是浏览器向服务器传数据的一种方式，数据会直接写在 URL 地址里，格式是：
域名?参数名=参数值
![3](题3.png)
代码含义：
给 URL 传一个 moe=flag 的参数，它就给你 flag；
不传 / 传别的值，它就只给你看源码。

现在的URL是http://node5.anna.nssctf.cn:26189

给它加上 ?moe=flag    
完整地址就是：
node5.anna.nssctf.cn:26189?moe=flag
![3](题3.1.png)
成功得到flag