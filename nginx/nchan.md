# nchan安装和测试

#### 下载源码
``` bash
wget http://nginx.org/download/nginx-1.14.0.tar.gz
wget https://github.com/slact/nchan/archive/v1.1.15.zip

#解压
tar -zxvf nginx-1.14.0.tar.gz
uzip v1.1.15.zip

#进入 nginx-1.14.0 
./configure --sbin-path=/usr/local/nginx --conf-path=/usr/local/nginx.conf --pid-path=/usr/local/nginx/nginx.pid --with-http_realip_module --with-http_sub_module --add-module=/home/software/nchan-1.1.15

#编译安装
make && make install

#到 /usr/local文件下
./nginx -v  #查看版本
./nginx -V  #查看配置
./nginx  #打开 nginx
./nginx -s reload|reopen|stop|quit  #重新加载配置|重启|停止|退出 nginx
```

##### 添加nchan 配置
``` bash
#在nginx.conf 的 server 下添加

   location = /sub {
      nchan_subscriber;
      nchan_channel_id $arg_id;
    }

    location = /pub {
      nchan_publisher;
      nchan_channel_id $arg_id;
    }
```


##### nginx 修改配置 重新加载
``` bash
./nginx -t -c /usr/local/nginx.conf    #执行后会打印 successful 标示成功
./nginx  -s  reload  -c  /usr/local/nginx.conf #标示重新加载配置文件
```


##### 模拟post发布nchan消息
``` bash
curl -H "Content-Type:application/json" -X POST -d '{"user": "admin", "passwd":"12345678"}' http://192.168.0.65/pub?id=demo
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
