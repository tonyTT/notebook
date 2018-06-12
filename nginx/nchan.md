# nchan安装和测试

##### 模拟post发布nchan消息
``` bash
curl -H "Content-Type:application/json" \
-X POST -d '{"user": "admin", "passwd":"12345678"}' \
http://192.168.0.65/pub?id=demo
``` 
##### js通过websocket订阅
``` 
 var ws = new WebSocket("ws://192.168.0.65/sub?id=demo");
   ws.onmessage = function (evt) 
   { 
      var received_msg = evt.data;
      console.log(received_msg);
   };
```
