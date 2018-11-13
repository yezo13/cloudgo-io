
## 任务要求：
### 编程 web 应用程序 cloudgo-io，实现：

 - 支持静态文件服务
- 支持简单 js 访问
- 提交表单，并输出一个表格
- 对 /unknown 给出开发中的提示，返回码 5xx

---

## 参考资料：
老师的教程：https://blog.csdn.net/pmlpml/article/details/78539261

---
## 实现：

### 【前期准备】
文件一共引用了三个额外的库，需要先从对应的github地址中克隆到自己的github.com的文件夹里
三个库分别是

    "github.com/codegangsta/negroni" //库
    "github.com/gorilla/mux"         //路由功能
    "github.com/unrolled/render"

克隆的操作就是cd到gopath的src下的github.com文件夹中，然后mkdir对应的文件夹（如codegangsta），然后再cd进去 clone就可以了，操作如图示
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181113000615638.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1llem8xMw==,size_16,color_FFFFFF,t_70)

### 【文件结构】
其中【assets】放的是网页的素材和js文件，service里面放的是处理的逻辑实现，templates中是表格的模板
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181113000820802.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1llem8xMw==,size_16,color_FFFFFF,t_70)

### 【代码实现】
代码实现可以参考上面给出的老师的教程，非常详细，按照老师给出的代码模块进行适当的修改就能实现了。

### 【静态文件服务】

编写好文档后cd到文件的目录，go run main.go，此时显示占用的端口8080

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181113001152864.png)

打开网页可看到定义好的网页

【未放入html文件时候显示的是当前文件夹下的所有文件】

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181113001302875.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1llem8xMw==,size_16,color_FFFFFF,t_70)

【放入后显示具体的网页】
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181113001410424.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1llem8xMw==,size_16,color_FFFFFF,t_70)

【按照教程尝试时候handler实现不同后缀的相应】
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181113001503223.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1llem8xMw==,size_16,color_FFFFFF,t_70)

### 【简单js访问】

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181113001615367.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1llem8xMw==,size_16,color_FFFFFF,t_70)

### 【提交表单并输出表格】

【输入】
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181113001648571.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1llem8xMw==,size_16,color_FFFFFF,t_70)

【输出表格】（submit后）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181113001704284.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1llem8xMw==,size_16,color_FFFFFF,t_70)

【控制台记录】
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181113001727939.png)

### 【对 /unknown 给出开发中的提示，返回码 501】

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181113001851837.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1llem8xMw==,size_16,color_FFFFFF,t_70)

具体实现可以参考我的github：

### 【一些坑】
1.写web的时候更新代码后需要刷新页面甚至清理缓存，否则有可能不能同步最新的代码，也可以安装一个chorme的插件实现同步更新。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181113002221514.png)

2.之前实现的时候如果直接ctrl+c退出，程序虽然退出了，但占用的端口并没有被释放。因此再次go run main.go的时候就会提示8080端口已经被占用，如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181113002326695.png)

此时可以通过 `netstat -ano | findstr 8080` 这个指令找到占用端口的进程，然后用指令 `taskkill -PID 端口号 -F` 杀掉
如图示

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181113002425367.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1llem8xMw==,size_16,color_FFFFFF,t_70)