# 背景

公司内部各团队对 RESTful API 的设计规范不统一，制约着接口的可扩展性和可维护性，增加调用者的使用成本和排障成本

# 概念

资源：网络上的一个实体，或者说是网络上的一个具体信息，它可以是一段文本、一张图片、一首歌曲、一种服务。

- 一组资源：均用复数表示，表示一组集合，例如 resources、animals、people 等，以下未特殊说明，资源均默认指一组资源
- 单个资源：均用单数表示，表示单个资源，例如 resource、animal、people 等

资源 id：单个资源的唯一标识符，形如 resource_id

子资源：某个资源的从属资源，其不能独立存在，例如 subresources、tables、documents 等，以下未特殊，子资源均默认指一组子资源

子资源 id：单个子资源的唯一标识符，形如 subresource_id

表述：representation，基于一组资源或单个资源的静态表述，用于描述资源的状态、信息等，例如 info、status、progress、summary、result 等，是静态的名词

操作：action，基于一组资源或单个资源的动态操作，用于对资源执行操作等，例如 search、upload、start、stop、trigger、analyze、flush 等，是动态的动词

# 原则

参考大公司的设计规范、开发实践以及公司的实际情况，在 ROA（Resource Oriented Architecture）风格的 RESTful API 基础上，扩展 DDD（Domain-Driven Design） 方案

如 Elasticsearch 中的 index 相关的 API 是 ROA + DDD 结合的例子：

| 风格 | API 名称 | API 示例 | 类型 |
| --- | --- | --- | --- |
| ROA | Create index | PUT /<index_id> | Create |
| Delete index | DELETE /<index_id> | Delete |  |
| Put mapping | PUT /<index_id>/_mapping | Create/Update |  |
| Get mapping | GET /<index_id>/_mapping | Retrieve |  |
| DDD | Open index | POST /<index_id>/_open | Action |
| Close index | POST /<index_id>/_close | Action |  |
| Search API | GET /<index_id>/_search | Representation/Action |  |
| Search API | POST /<index_id>/_search | Action |  |

# 规范

## 协议（Protocol）

HTTP/HTTPS 1.1

## 端点（Endpoint）

基本要求：

- 要求以 /<project>/api 开头
- URL 路径不能使用大写，单词如果需要分隔，统一使用下划线
- 路径禁止携带表示请求内容类型的后缀

端点形式：

- 基于资源，其中 <resources>、<subresources> 均使用复数，<resource_id> 是 Path Parameter：
    - /api/<resources>
    - /api/<resources>/<resource_id>
    - /api/<resources>/<resource_id>/<subresources>
    - /api/<resources>/<resource_id>/<subresources>/<subresource_id>
- 基于资源的表述，其中 <representation> 为名词，例如 info、status、progress、summary、result 等，仅用于 GET：
    - /api/<representation>
    - /api/<resources>/<representation>
    - /api/<resources>/<resource_id>/<representation>
    - /api/<resources>/<resource_id>/<subresources>/<representation>
    - /api/<resources>/<resource_id>/<subresources>/<subresource_id>/<representation>
- 基于资源的操作，其中 <action> 为动词，例如 search、upload、start、stop、trigger、analyze、flush 等，仅用于 POST：
    - /api/<action>
    - /api/<resources>/<action>
    - /api/<resources>/<resource_id>/<action>
    - /api/<resources>/<resource_id>/<subresources>/<action>
    - /api/<resources>/<resource_id>/<subresources>/<subresource_id>/<action>

## 请求方法（Request Method）

方法及对应端点：

- GET：查询
    - /api/<resources>：获取资源列表
    - /api/<resources>/<resource_id>：获取单个资源
    - /api/<resources>/<resource_id>/<subresources>：获取子资源列表
    - /api/<resources>/<resource_id>/<subresources>/<subresource_id>：获取单个子资源
- POST：创建
    - /api/<resources>：创建资源（返回<resource_id>）
    - /api/<resources>/<resource_id>/<subresources>：创建子资源（返回<subresource_id>）
- PUT：更新
    - /api/<resources>：更新多个资源
    - /api/<resources>/<resource_id>：更新单个资源
    - /api/<resources>/<resource_id>/<subresources>：更新多个子资源
    - /api/<resources>/<resource_id>/<subresources>/<subresource_id>：更新单个子资源
- DELETE：删除
    - /api/<resources>：删除多个资源
    - /api/<resources>/<resource_id>：删除单个资源
    - /api/<resources>/<resource_id>/<subresources>：删除多个子资源
    - /api/<resources>/<resource_id>/<subresources>/<subresource_id>：删除单个子资源
- GET：表述
    - /api/<representation>：获取表述（例如 /health）
    - /api/<resources>/<representation>：获取资源列表表述
    - /api/<resources>/<resource_id>/<representation>：获取单个资源表述
    - /api/<resources>/<resource_id>/<subresources>/<representation>：获取子资源列表表述
    - /api/<resources>/<resource_id>/<subresources>/<subresource_id>/<representation>：获取单个子资源表述
- POST：操作
    - /api/<action>：操作（例如 /login、/logout）
    - /api/<resources>/<action>：资源列表操作
    - /api/<resources>/<resource_id>/<action>：单个资源操作
    - /api/<resources>/<resource_id>/<subresources>/<action>：子资源列表操作
    - /api/<resources>/<resource_id>/<subresources>/<subresource_id>/<action>：单个子资源操作

正则匹配冲突问题：

- 少数情况下以下三个端点可能存在冲突，1 和 2 存在 GET 冲突，1 和 3 存在 POST 冲突
    1. /api/<resources>/<resource_id>
    2. /api/<resources>/<representation>
    3. /api/<resources>/<action>
- 解决方案：
    1. 设计上规避可能出现的冲突情况，实际情况下，以上各个路径端点不会全部出现
    2. <resource_id> 是特定格式的情形下，例如数字、32位 hash 值等，则正则严格匹配时可以自动避免了冲突
    3. <resource_id> 是任意格式的情形下，匹配 <resource_id> 的正则表达式中，对 <representation> 和 <action> 取反
    4. <resource_id> 是任意格式的情形下，可以使用顺序机制进行正则匹配，先匹配 <representation> 和 <action>，再匹配 <resource_id>
    5. <resource_id> 是任意格式的情形下，可以要求 <resource_id> 不以 "_" 开头，而 <representation> 和 <action> 均以 "_" 开头，则可以避免冲突（参考 Elasticsearch）
- 建议优先使用解决方案 1、2、3 或 4

## 请求标头（Request Header）

客户端请求时要求 Header 中添加 Content-Type、Accept 字段

- Content-Type：表示客户端请求的媒体类型信息，也叫做 MIME 类型
    - application/json：JSON 类型数据（默认要求）
    - application/x-www-form-urlencoded：表单编码数据（前后端分离的情况下，不用考虑此类型）
    - multipart/form-data：表单数据，仅用于 POST，二进制文件，如上传文件
    - application/octet-stream：未知类型，如上传文件
    - 注意：
        - GET 没有 Content-Type
        - Form 表单数据只能使用 POST 提交
        - 没有 Request Body 的可以设置 Content-Type 为空
        - 有 Request Body 的应设置为 application/json 或者 multipart/form-data、application/octet-stream
- Accept：告知（服务器）客户端可以处理的内容类型
    - application/json：JSON 类型数据
- Authorization：表示客户端携带的认证信息，详见后面的“认证（Authentication）”

## 请求参数/实体（Request Parameter/Body）

基本使用：

- Path Parameter：例如 /api/animals/<animal_id>，其中 <animal_id> 是 Path 参数
- Query Parameter：例如 ?force=true、?page=2&per_page=100，主要用于 GET、DELETE
- Request Body：JSON 数据类型，主要用于PUT、POST，不能用于 GET

注意事项：

- 在分页场景中，用户输入参数的小于 1，则前端返回第一页参数给后端；后端发现用户输入的参数大于总页数，直接返回最后一页
- 在分页场景中，若要获取全部数据，需要单独开放一个接口，不要和分页接口混用
- 时间参数：要求为 Unix 时间戳，例如 10 位、13 位

## 响应状态码（Response Status Code）

仅能使用以下常见的状态码：

- 200 OK - [GET/POST/PUT]：表明请求已经成功
- 201 Created - [POST]：表示请求已经被成功处理，并且创建了新的资源，同时新增的资源会在应答消息体中返回
- 202 Accepted - [POST/PUT/DELETE]：表示服务器端已经收到请求消息，但是尚未进行处理。用来将请求交由另外一个进程或者服务器来进行处理，或者是对请求进行批处理的情形
- 204 No Content - [DELETE]：删除数据成功时，不返回数据
- 400 Bad Request - [*]：表示由于语法无效，服务器无法理解该请求，例如请求参数或实体不合法
- 401 Unauthorized - [*]：代表客户端错误，指的是由于缺乏目标资源要求的身份验证凭证。表示用户没有权限（令牌、用户名、密码错误）
- 403 Forbidden - [*] 代表客户端错误，指的是服务器端有能力处理该请求，但是拒绝授权访问。表示用户得到授权（与401错误相对），但是访问是被禁止的
- 404 Not Found - [*]：代表客户端错误，指的是服务器端无法找到所请求的资源
- 405 Method Not Allowed - [*]：表明服务器禁止了使用当前 HTTP 方法的请求
- 415 Unsupported Media Type - [*]：表示服务器由于不支持其有效载荷的格式，从而拒绝接受客户端的请求
- 500 Internal Server Error - [*]：表示服务器端错误的响应状态码，意味着所请求的服务器遇到意外的情况并阻止其执行请求

注意事项：

- 2XX：成功
- 4XX：客户端错误
    - 除 400 错误外，其它 4XX 错误都有明确含义，应优先使用该状态码，响应实体（Response Body）可以不用额外附加错误信息
    - 对 400 错误，应该在响应实体内对 code（错误码）和 msg（可读的错误消息）字段做详细错误说明，见响应实体
- 5XX：服务端错误

## 响应标头（Response Header）

服务端响应时要求 Header 中添加 Content-Type

- Content-Type：告诉客户端实际返回的内容的内容类型
    - application/json：JSON 类型数据（默认要求）
    - application/octet-stream：未知类型，一般用于数据传输下载

## 响应实体（Response Body）

返回 JSON 格式，如下所示：

- code 为错误码，msg 为错误信息，约定如下：
    - code 为 0 表示没有错误（默认为 0），code为 1 - 1000 用作通用错误码（参考附录），1000以上业务错误码（由业务自己定义）
    - msg 为可读的中文错误消息，默认为空“”
- data 为数据字段，为请求的返回结果，可以是单值、列表或字典（非必须，如果为 null 时建议不放入 data 字段）
    - 前后端数据列表相关的接口返回，如果为空，则返回空数组 [] 或空字典 {}
- data 中所有的 key 必须为小写字母开始的 lowerCamelCase 风格，符合英文表达习惯，且表意完整（禁止用缩写）
- data 中所有的 key（除 msg 字段外）都需要全拼，不使用缩写
- 对于需要使用超大整数的场景，服务端一律使用 String 字符串类型返回，禁止使用 Long 类型
- 时间字段：要求为 Unix 时间戳，例如 10 位、13 位，尽量避免时间格式；如有必要，时间格式统一为 "yyyy-MM-dd HH:mm:ss"，统一为 GMT+8

| Column 1 |
| --- |
| {  "code": 0,  "msg": "",  "data": value or {} or []} |

## 版本（Version）

两种方式

Path 中添加版本号：

- 例如 /api/v1

Header 中添加版本号：

- 客户端请求时要求 Header 中添加 Accept-Version，否则返回版本错误，例如：Accept-Version: v1
- 在接口路径中不要加入版本号，版本控制在 HTTP 头信息中体现，有利于向前兼容

统一使用在 Path 中添加版本号的方式

## 认证（Authentication）

请求 Header 包含有用来向服务器证明用户代理身份的凭证，需要指明验证的类型，其后跟有凭证信息，该凭证信息可以被编码或者加密，取决于采用的是哪种验证方案

例如常见的验证类型有：Basic、Bearer，其中 Basic Auth 基于 Basic，JWT 基于 Bearer


| Column 1 | |
 --- |----
| Authorization: <type> <credentials> |123|

## 压缩（Compression）

HTTP 请求头 Accept-Encoding 会将客户端能够理解的内容编码方式——通常是某种压缩算法——进行通知（给服务端）。通过内容协商的方式，服务端会选择一个客户端提议的方式，使用并在响应头 Content-Encoding 中通知客户端该选择

例如采用 gzip 压缩，则

- 请求 Header 中应包含 Accept-Encoding: gzip
- 响应 Header 中应包含 Content-Encoding: gzip

## 跨源资源共享（CORS）

前后端分离的情形下，前端访问后端接口需要设置 CORS，具体的，在响应 Header 中主要设置以下两条：

| Column 1 |
| --- |
| Access-Control-Allow-Origin: *Access-Control-Allow-Methods: GET, POST, PUT, DELETE, OPTIONS |

## 缓存（Caching）

服务器返回信息必须被标记是否可以缓存，如果缓存，客户端可能会重用之前的请求结果

| Column 1 |
| --- |
| Cache-Control: max-age=31536000Cache-Control: s-maxage=31536000 |

备注：此项不做严格要求，视情况而定

## 重定向（Redirection）

极少数在接入三方认证时会发生，一般不涉及此情形

## Cookie 和 Session

不涉及此情形

# 附录

## 通用错误码列表

| Column 1 | Column 2 |
| --- |
| 错误码 | 错误描述 |
| 1000-1999 | ilog |

# 参考

理解RESTful架构：[https://www.ruanyifeng.com/blog/2011/09/restful.html](https://www.ruanyifeng.com/blog/2011/09/restful.html)

RESTful API 设计指南：[http://www.ruanyifeng.com/blog/2014/05/restful_api.html](http://www.ruanyifeng.com/blog/2014/05/restful_api.html)

RESTful API 最佳实践：[https://www.ruanyifeng.com/blog/2018/10/restful-api-best-practices.html](https://www.ruanyifeng.com/blog/2018/10/restful-api-best-practices.html)

如何设计好的RESTful API：[https://www.infoq.cn/article/how-to-design-a-good-restful-api/](https://www.infoq.cn/article/how-to-design-a-good-restful-api/)

理解本真的REST架构风格：[https://www.infoq.cn/article/understanding-restful-style/](https://www.infoq.cn/article/understanding-restful-style/)

为什么说要用DDD替代CRUD来设计API：[https://www.infoq.cn/article/there-is-no-u-in-crud/](https://www.infoq.cn/article/there-is-no-u-in-crud/)

阿里研究员谷朴：API 设计最佳实践的思考：[https://mp.weixin.qq.com/s/9JfzgsJbzP3__odWVZ91dg](https://mp.weixin.qq.com/s/9JfzgsJbzP3__odWVZ91dg)

Restful API设计最佳实践：[http://kaelzhang81.github.io/2019/05/24/Restful-API%E8%AE%BE%E8%AE%A1%E6%9C%80%E4%BD%B3%E5%AE%9E%E8%B7%B5/](http://kaelzhang81.github.io/2019/05/24/Restful-API%E8%AE%BE%E8%AE%A1%E6%9C%80%E4%BD%B3%E5%AE%9E%E8%B7%B5/)

RESTful API Design. Best Practices in a Nutshell：[https://phauer.com/2015/restful-api-design-best-practices/](https://phauer.com/2015/restful-api-design-best-practices/)

RESTful Service API 设计最佳工程实践和常见问题解决方案：[https://www.jianshu.com/p/cf80d644727e](https://www.jianshu.com/p/cf80d644727e)

13 个设计 REST API 的最佳实践：[https://segmentfault.com/a/1190000017464263](https://segmentfault.com/a/1190000017464263)

Elasticsearch REST APIs：[https://www.elastic.co/guide/en/elasticsearch/reference/current/rest-apis.html](https://www.elastic.co/guide/en/elasticsearch/reference/current/rest-apis.html)

Google Could API 设计：[https://cloud.google.com/apis/design](https://cloud.google.com/apis/design)

Microsoft API 设计：[https://docs.microsoft.com/zh-cn/azure/architecture/best-practices/api-design](https://docs.microsoft.com/zh-cn/azure/architecture/best-practices/api-design)

GitHub REST API latest：[https://docs.github.com/cn/free-pro-team@latest/rest/overview](https://docs.github.com/cn/free-pro-team@latest/rest/overview)

GitHub REST API v3：[https://developer.github.com/v3/](https://developer.github.com/v3/)

OpenAPI-Specification：[https://swagger.io/specification/v2/](https://swagger.io/specification/v2/)

Anomaly RESTful API 设计原则：[Anomaly RESTful API 设计原则](https://wiki.bizseer.com/pages/viewpage.action?pageId=2886038)

HTTP Error 互联网公司设计方案：参考以下附件

[HTTP Error 互联网公司设计方案.pdf](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/63faa0c1-bae5-48fa-84a1-1ca1f3bc0d14/HTTP_Error_.pdf)