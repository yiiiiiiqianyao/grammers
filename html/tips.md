# new Element

* track 为诸如 <video> 和 <audio> 元素之类的媒介规定外部文本轨道  

    ```
        <video width="320" height="240" controls>
            <source src="forrest_gump.mp4" type="video/mp4">
            <source src="forrest_gump.ogg" type="video/ogg">
            <track src="subtitles_en.vtt" kind="subtitles" srclang="en"
            label="English">
            <track src="subtitles_no.vtt" kind="subtitles" srclang="no"
            label="Norwegian">
        </video>
    ```

* datalist 定义选项列表。请与 input 元素配合使用该元素，来定义 input 可能的值

    ```
        <input list="browsers">
        <datalist id="browsers">
            <option value="Internet Explorer">
            <option value="Firefox">
            <option value="Chrome">
            <option value="Opera">
            <option value="Safari">
        </datalist>
    ```

    * embed <embed> 标签是 HTML 5 中的新标签

        ```
            <embed src="helloworld.swf">
        ```

* Server Sent Event (HTML5 服务器发送事件)
    ```
        var source=new EventSource("demo_sse.php")
        source.onmessage=function(event)
        {
            document.getElementById("result").innerHTML+=event.data + "<br>"
        };
    ```

* HTML5 WebSocket
    ```
        var Socket = new WebSocket(url, [protocol] )
        WebSocket 属性
            Socket.readyState 只读属性 readyState 表示连接状态，可以是以下值
                0 - 表示连接尚未建立。
                1 - 表示连接已建立，可以进行通信。
                2 - 表示连接正在进行关闭。
                3 - 表示连接已经关闭或者连接不能打开。
            Socket.bufferedAmount 只读属性 bufferedAmount 已被 send() 放入正在队列中等待传输，但是还没有发出的 UTF-8 文本字节数
        WebSocket 事件
            Socket.onopen       连接建立时触发
            Socket.onmessage    客户端接收服务端数据时触发
            Socket.onerror      通信发生错误时触发
            Socket.onclose      连接关闭时触发
        WebSocket 方法
            Socket.send()   使用连接发送数据
            Socket.close() 	关闭连接
    ```

* js 的解析机制
    ```
        遇到 script 标签的话 js 就进行预解析，将变量 var 和 function 声明提升，但不会执行 function，
        然后就进入上下文执行，上下文执行还是执行预解析同样操作，直到没有 var 和 function，就开始执行上下文
    ```

* Undefined 不是 Null
    ```
        在 JavaScript 中, null 用于对象, undefined 用于变量，属性和方法
        对象只有被定义才有可能为 null，否则为 undefined
    ```

* javascript:void(0) 含义
    ```
        javascript:void(0) 中最关键的是 void 关键字， void 是 JavaScript 中非常重要的关键字，该操作符指定要计算一个表达式但是不返回值

        语法格式如下
            void func()
            javascript:void func()
            或者
            void(func())
            javascript:void(func())

        href="#"与href="javascript:void(0)"的区别

            # 包含了一个位置信息，默认的锚是#top 也就是网页的上
    ```