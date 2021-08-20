# 网络编程（net网络包）

- 传输协议

&ensp;&ensp;&ensp;&ensp;[计算机网络](https://www.wolai.com/p32pAa7uQsf73sSkSP3PqP)

- 常用类

&ensp;&ensp;&ensp;&ensp;InterAddress：此类表示互联网协议 (IP) 地址

```Java
InetAddress ia = InetAddress.getLocalHost(); // 获取本机信息
InetAddress domainName = InetAddress.getByName("www.baidu.com"); // 使用域名获取信息
```


&ensp;&ensp;&ensp;&ensp;InetSocketAddress :此类实现 IP 套接字地址（IP 地址 + 端口号）。该类表示端口

&ensp;&ensp;&ensp;&ensp;URL类： URL 代表一个统一资源定位符

&ensp;&ensp;&ensp;&ensp;- UDP

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;UDP：Internet 协议集支持一个无连接的传输协议，该协议称为用户数据报协议（UDP，User Datagram Protocol）。UDP 为应用程序提供了一种无需建立连接就可以发送封装的 IP 数据报的方法。

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;用数据包（DatagramPacket）传输（DatagramSocke）

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;DatagramSocket：此类表示用来发送和接收数据报包的套接字（作用：应用层与传输层的通讯）

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;DatagramPacket数据包：此类表示数据报包，该类构造器中有接收和发送的构造器，数据

&ensp;&ensp;&ensp;&ensp;- TCP

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;TCP：输控制协议（TCP，Transmission Control Protocol）是一种面向连接的、可靠的、基于字节流的传输层通信协议。

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;注：使用基于TCP协议的Socket网络编程实现。用lO流实现数据输出

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;扩展：HTTP协议底层使用的也是TCP协议，TCP是请求-响应式的request response

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;服务器端：ServerSocket

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;客户端：Socket

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;传输使用IO操作

&ensp;&ensp;&ensp;&ensp;- 代码示例

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;URL 编码解码：URL Decoder  和 URL Encoder

```Java
    try {  
            // 将application/x-www-from-urlencoded字符串转换成普通字符串    
            String keyWord = URLDecoder.decode("%C4%E3%BA%C3", "GBK");    
            System.out.println(keyWord);  //输出你好  
            // 将普通字符创转换成application/x-www-from-urlencoded字符串    
            String urlString = URLEncoder.encode("你好", "GBK");  //输出%C4%E3%BA%C3  
            System.out.println(urlString);  
        } catch (UnsupportedEncodingException e) {  
            // TODO Auto-generated catch block  
            e.printStackTrace();  
        } 
```


&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;发送http请求实现聊天机器人

```Java
    // 将普通字符创转换成application/x-www-from-urlencoded字符串    
    String urlQuestion=URLEncoder.encode("你上学吗？","UTF-8");
    // URL
    URL url = new URL("https://api.ownthink.com/bot?appid=xiaosi&userid=user&spoken=" + urlQuestion);
    // 打开连接
    HttpURLConnection huc = (HttpURLConnection) url.openConnection();
    // 设置请求和请求的浏览器（User-Agent：用户代理指代浏览器）
    huc.setRequestMethod("GET");
    huc.setRequestProperty("User-Agent", "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.97 Safari/537.36");
    // 打开输入流+字节转换字符+缓冲流
    BufferedReader br = new BufferedReader(new InputStreamReader(huc.getInputStream(), "utf-8"));
    // 遍历
    String line = null;
    while ((line = br.readLine()) != null) {
      System.out.println(line);
    }  
    // 关闭流
    br.close();
```



