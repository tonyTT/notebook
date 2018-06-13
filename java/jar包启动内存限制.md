
### java包启动内存限制

```bash
java -jar -Xms1024m -Xmx1536m -XX:PermSize=128M -XX:MaxPermSize=256M car.jar
```
 

#### 说明：
>1.堆内存：最小1024M，最大1536M。（对象使用的内存）

>2.永久内存：最小128M，最大256M。（类使用的内存，PermGen）
