## Web攻击

### [1] SQL 注入攻击
**---> 指针对 Web 应用使用的数据库，通过运行非法的 SQL 而产生的攻击。**
- 非法查看或篡改数据库内的数据。
- 规避认证。
- 执行和数据库服务器业务关联的程序等
  
### [2] OS 命令注入攻击
**---> 指通过 Web 应用，执行非法的操作系统命令达到攻击的目的。只要在能调用 Shell 函数的地方就有存在被攻击的风险。**

### 跨站脚本攻击（Cross-Site Scripting，XSS）
**---> 指通过存在安全漏洞的 Web 网站注册用户的浏览器内运行非法的 HTML 标签或 JavaScript 进行的一种攻击。**
- 利用虚假输入表单骗取用户个人信息。
- 利用脚本窃取用户的 Cookie 值，被害者在不知情的情况下，帮助攻击者发送恶意请求。
- 显示伪造的文章或图片。
  
### [3] HTTP 首部注入攻击
**---> 指攻击者通过在响应首部字段内插入换行（%0D%0A），添加任意响应首部或主体的一种攻击。**
- 设置任何 Cookie 信息。
- 重定向至任意 URL。
  
### [4] HTTP 响应截断攻击
**---> 将两个 %0D%0A%0D%0A 并排插入字符串后发送。利用这两个连续的换行就可作出 HTTP 首部与主体分隔所需的空行了，这样就能显示伪造的主体，达到攻击目的。**

### [5] 跨站点请求伪造（Cross-Site Request Forgeries，CSRF）
**---> 指攻击者通过设置好的陷阱，强制对已完成认证的用户进行非预期的个人信息或设定信息等某些状态更新。**

### [6] 点击劫持
**---> 指利用透明的按钮或链接做成陷阱，覆盖在 Web 页面之上。又叫界面伪装（UI Redressing）。**

### [7] DoS 攻击（Denial of Service attack）
**---> 是一种让运行中的服务呈停止状态的攻击。有时也叫做服务停止攻击或拒绝服务攻击。**
```
    主要DoS攻击方式：
        1、集中利用访问请求造成资源过载，资源用尽的同时，实际上服务也就呈停止状态。
        2、通过攻击安全漏洞使服务停止。
```