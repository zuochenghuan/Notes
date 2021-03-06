## http与https区别

1、https协议需要到ca申请证书，一般免费证书较少，因而需要一定费用。

2、http是超文本传输协议，信息是明文传输，https则是具有安全性的ssl加密传输协议。

3、http和https使用的是完全不同的连接方式，用的端口也不一样，前者是80，后者是443。

4、http的连接很简单，是无状态的；HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议，比http协议安全。

5、https占用更多的服务器资源。HTTP使用TCP三次握手建立连接，客户端和服务器需要交换3个包，HTTPS除了TCP的三个包，还要加上ssl握手需要的9个包，所以一共是12个包。与http相比，https占用资源主要来源于SSL/TLS本身消耗多少服务器资源。

详细来源：[https://juejin.im/entry/58d7635e5c497d0057fae036](https://juejin.im/entry/58d7635e5c497d0057fae036)

## GET POST PUT DELETE操作的区别

**GET操作是安全的**。所谓安全是指不管进行多少次操作，资源的状态都不会改变。比如我用GET浏览文章，不管浏览多少次，那篇文章还在那，没有变化。当然，你可能说每浏览一次文章，文章的浏览数就加一，这不也改变了资源的状态么？这并不矛盾，因为这个改变不是GET操作引起的，而是用户自己设定的服务端逻辑造成的。

**PUT，DELETE操作是幂等的**。所谓幂等是指不管进行多少次操作，结果都一样。比如我用PUT修改一篇文章，然后在做同样的操作，每次操作后的结果并没有不同，DELETE也是一样。顺便说一句，因为GET操作是安全的，所以它自然也是幂等的。

**POST操作既不是安全的，也不是幂等的**，比如常见的POST重复加载问题：当我们多次发出同样的POST请求后，其结果是创建出了若干的资源。  
**安全和幂等的意义在于**：当操作没有达到预期的目标时，我们可以不停的重试，而不会对资源产生副作用。从这个意义上说，POST操作往往是有害的，但很多时候我们还是不得不使用它。

还有一点需要注意的就是，创建操作可以使用POST，也可以使用PUT，区别在于POST 是作用在一个集合资源之上的（/uri），而PUT操作是作用在一个具体资源之上的（/uri/xxx），再通俗点说，**如果URL可以在客户端确定，那么就使用PUT，如果是在服务端确定，那么就使用POST**，比如说很多资源使用数据库自增主键作为标识信息，而创建的资源的标识信息到底是什么只能由服务端提供，这个时候就必须使用POST。

### SSL/STL加密的过程以及SSL协议

阮老师有讲到过SSL加密的过程以及SSL协议：

[SSL/TLS协议运行机制的概述](http://www.ruanyifeng.com/blog/2014/02/ssl_tls.html)

[图解SSL/TLS协议](http://www.ruanyifeng.com/blog/2014/09/illustration-ssl.html)

[SSL延迟有多大](http://www.ruanyifeng.com/blog/2014/09/ssl-latency.html)

**握手过程**：

第一步，爱丽丝给出协议版本号、一个客户端生成的随机数（Client random），以及客户端支持的加密方法。

第二步，鲍勃确认双方使用的加密方法，并给出数字证书、以及一个服务器生成的随机数（Server random）。

第三步，爱丽丝确认数字证书有效，然后生成一个新的随机数（Premaster secret），并使用数字证书中的公钥，加密这个随机数，发给鲍勃。

第四步，鲍勃使用自己的私钥，获取爱丽丝发来的随机数（即Premaster secret）。

第五步，爱丽丝和鲍勃根据约定的加密方法，使用前面的三个随机数，生成"对话密钥"（session key），用来加密接下来的整个对话过程。

握手成功之后使用对话密钥（对称密钥）加密数据，客户端使用对话密钥解密数据。

整个握手阶段都不加密（也没法加密），都是明文的。因此，如果有人窃听通信，他可以知道双方选择的加密方法，以及三个随机数中的两个。整个通话的安全，只取决于第三个随机数（Premaster secret）能不能被破解。

#### http/0.9

- HTTP 是基于 TCP/IP 协议的应用层协议。它不涉及数据包（packet）传输，主要规定了客户端和服务器之间的通信格式，默认使用80端口。
- 只有`GET`请求
- 协议规定，服务器只能回应HTML格式的字符串，不能回应别的格式。
- 服务器发送完毕，就关闭TCP连接。

#### http/1.0

- 任何格式的内容都可以发送。这使得互联网不仅可以传输文字，还能传输图像、视频、二进制文件。这为互联网的大发展奠定了基础。
- 除了GET命令，还引入了`POST`命令和`HEAD`命令，丰富了浏览器与服务器的互动手段。
- HTTP请求和回应的格式也变了。除了数据部分，每次通信都必须包括头信息（HTTP header），用来描述一些元数据。
- 其他的新增功能还包括状态码（`status code`）、多字符集支持、多部分发送（multi-part type）、权限（authorization）、缓存（cache）、内容编码（`content` `encoding`）等。

**缺点：**

- 每个TCP连接只能发送一个请求。发送数据完毕，连接就关闭，如果还要请求其他资源，就必须再新建一个连接。
- TCP连接的新建成本很高，因为需要客户端和服务器三次握手，并且开始时发送速率较慢（slow start）

#### http/1.1

- 引入了持久连接（persistent connection），即TCP连接默认不关闭，可以被多个请求复用，不用声明`Connection: keep-alive`
- 使用`connection: close`关闭TCP连接
- 引入了管道机制（pipelining），即在同一个TCP连接里面，客户端可以同时发送多个请求。这样就进一步改进了HTTP协议的效率。但是服务器还是要按照顺序来回应请求。
- 可以使用分块传输编码。
- 新增了许多动词方法：`PUT`、`PATCH`、 `OPTIONS`、`DELETE`。
- 客户端请求的头信息新增了`Host`字段，用来指定服务器的域名。

**缺点：**

虽然1.1版允许复用TCP连接，但是同一个TCP连接里面，所有的数据通信是按次序进行的。服务器只有处理完一个回应，才会进行下一个回应。要是前面的回应特别慢，后面就会有许多请求排队等着。这称为"队头堵塞"。

为了避免这个问题，只有两种方法：一是减少请求数，二是同时多开持久连接。

#### http/2

注意，不叫http/2.0，因为不打算发布子版本了，下一个版本应该直接是http/3

1. **二进制协议**：HTTP/2 则是一个彻底的二进制协议，头信息和数据体都是二进制，并且统称为"帧"（frame）：头信息帧和数据帧。
2. **多工**： HTTP/2 复用TCP连接，在一个连接里，客户端和浏览器都可以同时发送多个请求或回应，而且不用按照顺序一一对应，这样就避免了"队头堵塞"。
3. **数据流**：HTTP/2 将每个请求或回应的所有数据包，称为一个数据流（stream）。每个数据流都有一个独一无二的编号。数据包发送的时候，都必须标记数据流ID，用来区分它属于哪个数据流。另外还规定，客户端发出的数据流，ID一律为奇数，服务器发出的，ID为偶数。
4. **头信息压缩**：引入了头信息压缩机制（header compression）。一方面，头信息使用gzip或compress压缩后再发送；另一方面，客户端和服务器同时维护一张头信息表，所有字段都会存入这个表，生成一个索引号，以后就不发送同样字段了，只发送索引号，这样就提高速度了。
5. **服务器推送**：允许服务器未经请求，主动向客户端发送资源，这叫做服务器推送