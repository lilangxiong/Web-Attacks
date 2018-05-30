## Web攻击

### [1] SQL 注入攻击
**---> 指针对 Web 应用使用的数据库，通过运行非法的 SQL 而产生的攻击。**
```
影响：
    1、非法查看或篡改数据库内的数据。
    2、规避认证。
    3、执行和数据库服务器业务关联的程序等
    
案例：
    正常get请求链接：https://xxx.com/orderList.php?userId=1
    查询语句：$sql = "SELECT * FROM orderList WHERE userId =",$userId 
    此时只会返回userId = 1的用户的订单信息
    
    加入SQL攻击的get请求链接：https://xxx.com/orderList.php?userId=-1OR1=1
    userId = -1 || 1=1 运行结果是true，所以where条件相当于没有加where条件，那么查询的结果相当于整张表的内容，返回所有用户的订单信息
    
预防措施：
    1、参数化的查询语句，可以强制开发者首先定义所有的 sql 代码，之后再将每个参数传递给查询语句。
    2、使用语言自带的存储程序，而不是自己直接操纵数据库。
    3、验证用户的输入。
    4、对用户提供的所有输入都进行编码、转义。
```

### [2] 跨站点请求伪造（Cross-Site Request Forgeries，CSRF）
**---> 网站 A 对用户建立信任关系后，在网站 B 上利用这种信任关系，跨站点向网站 A 发起一些伪造的用户操作请求，以达到攻击的目的。**
```
案例：
    A银行网站的转账接口：bankA.com/transfer?toId=1&cash=1200，此接口只能在已经验证用户身份的情况下调用。
    B网站（攻击网站），包含调用以上接口的恶意代码，如果用户在A网站验证身份后，在身份验证有效期内访问了B网站，恶意代码就会执行成功。
    
预防措施：
    1、验证HTTP Referer字段，但Referer毕竟是由请求者发起的，依然是可以伪造的。
    2、服务器生成一个token，以token为密钥生成密文，发送给前端，前端请求时将token以及密文发送到后台验证。
```

### [3] 跨站脚本攻击（Cross-Site Scripting，XSS）
**---> 指通过在存在安全漏洞的 Web 网站内运行非法的 HTML 标签或 JavaScript 的一种攻击。**
```
影响：
    1、利用虚假输入表单骗取用户个人信息。
    2、利用脚本窃取用户的 Cookie 值，被害者在不知情的情况下，帮助攻击者发送恶意请求。
    3、显示伪造的文章或图片。
    
案例：
    如果服务器没有验证数据类型，直接接受任何数据时，攻击者可以会将 <script src='https://www.xxxx.com/xss.js'></script> 当做一个数据写入数据库。
    前端从后台获取数据（<script src='https://www.xxxx.com/xss.js'></script>）后，直接添加到页面上，一旦script被加到页面上就会立即开始执行恶意代码。

XSS的类型：
    1、存储型XSS：注入的脚本永久的存在于目标服务器上，每当受害者向服务器请求此数据时就会重新唤醒攻击脚本。
    2、反射性XSS：受害者点击一个恶意链接，提交伪造的表单，恶意代码会和正常的返回数据一起作为响应内容发送到客户端。
    3、DOM型XSS：本地更新 DOM 时导致了恶意脚本执行。
    
预防措施：
    1、客户端、服务器端都需要验证所有输入的数据。
    2、对所有的数据进行编码、转义，如 "，'，<，>，&等。
    3、设置HTTP Header：X-XSS-Protection: 1，xhr.setRequestHeader("X-XSS-Protection", 1);
```
**X-XSS-Protection详解：**
<table>
    <tr>
        <th>语法</th>
        <th>说明</th>
    </tr>
    <tr>
        <td>X-XSS-Protection: 0</td>
        <td>禁止XSS过滤</td>
    </tr>
    <tr>
        <td>X-XSS-Protection: 1</td>
        <td>启用XSS过滤（通常浏览器是默认的）。 如果检测到跨站脚本攻击，浏览器将清除页面（删除不安全的部分）</td>
    </tr>
    <tr>
        <td>X-XSS-Protection: 1; mode=block</td>
        <td>启用XSS过滤。 如果检测到攻击，浏览器将不会清除页面，而是阻止页面加载</td>
    </tr>
    <tr>
        <td>X-XSS-Protection: 1; report=<reporting-uri></td>
        <td>启用XSS过滤。 如果检测到跨站脚本攻击，浏览器将清除页面并使用CSP report-uri指令的功能发送违规报告</td>
    </tr>
</table>

### [4] DDoS， 分布式拒绝服务（Distributed Denial of Service）
**---> DoS 攻击就是通过大量恶意流量占用带宽和计算资源以达到瘫痪对方网络的目的。**
```
    主要DoS攻击方式：
        1、集中利用访问请求造成资源过载，资源用尽的同时，实际上服务也就呈停止状态。
        2、通过攻击安全漏洞使服务停止。
```

### [5] HTTP 首部注入攻击
**---> 指攻击者通过在响应首部字段内插入换行（%0D%0A 或者 %0D%0A%0D%0A），添加任意响应首部或主体的一种攻击。**
```
影响：
    1、设置任何 Cookie 信息。
    2、重定向至任意 URL。
预防措施：
    1、过滤所有的response headers，除去header中出现的非法字符，尤其是CRLF。
```