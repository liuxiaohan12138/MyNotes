---
title: java笔记
---

[TOC]

# 字符串处理

1.多个空格替换为一个空格

```
str.replaceAll( "\\s+", " " );
```

2.删除最后一个字符

```
str.substring(0, buf.length()-1)
```

3.删除最后一个斜线后的字符串

```
// http://stackoverflow.com/questions/ask -> http://stackoverflow.com/questions/
String str="http://stackoverflow.com/questions/ask";
int index=str.lastIndexOf('/');
str = str.substring(0,index);
```



# 多线程数据传递

1.通过构造函数传递

```
public class MyThread extends Thread
{
	private String name;
	public MyThread1(String name)
	{
	   this.name = name;
	}
	public void run()
	{
	   System.out.println("hello " + name);
	}
	public static void main(String[] args)
	{
	   Thread thread = new MyThread("world");
	   thread.start();        
	 }
}
```

2.通过变量和方法传递

```
public class MyThread2 implements Runnable
{
    private String name;
    public void setName(String name)
    {
        this.name = name;
    }
    public void run()
    {
        System.out.println("hello " + name);
    }
    public static void main(String[] args)
    {
        MyThread2 myThread = new MyThread2();
        myThread.setName("world");
        Thread thread = new Thread(myThread);
        thread.start();
    }
}
```

3.调用回调函数传递数据

```
package mythread;
 
class Data
{
    public int value = 0;
}
class Work
{
    public void process(Data data, Integer numbers)
    {
        for (int n : numbers)
        {
            data.value += n;
        }
    }
}
public class MyThread3 extends Thread
{
    private Work work;
 
    public MyThread3(Work work)
    {
        this.work = work;
    }
    public void run()
    {
        java.util.Random random = new java.util.Random();
        Data data = new Data();
        int n1 = random.nextInt(1000);
        int n2 = random.nextInt(2000);
        int n3 = random.nextInt(3000);
        work.process(data, n1, n2, n3);   // 使用回调函数
        System.out.println(String.valueOf(n1) + "+" + String.valueOf(n2) + "+"
                + String.valueOf(n3) + "=" + data.value);
    }
    public static void main(String[] args)
    {
        Thread thread = new MyThread3(new Work());
        thread.start();
    }
}
```

4.从线程中获取返回值的方法

```
public class MyThread3 extends Thread {
    private String value1;
    private String value2;

    public void run() {
        value1 = "value1";
        value2 = "value2";
    }

    public static void main(String[] args) throws Exception {
        MyThread3 thread = new MyThread3();
        thread.start();
        // join方法会等待线程执行结束后才会继续执行
        thread.join();
        System.out.println("value1:" + thread.value1);
        System.out.println("value2:" + thread.value2);
    }
}
```



# WebSocket

pom.xml添加依赖

```
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-websocket</artifactId>
        </dependency>
```

添加配置类

```
@Configuration
public class WebSocketConfig {
    @Bean
    public ServerEndpointExporter serverEndpointExporter() {
        return new ServerEndpointExporter();
    }
}
```

添加服务类

```
@ServerEndpoint("/websocket")
@Component
public class WebSocketServer {

    static Logger logger = LoggerFactory.getLogger(WebSocketServer.class);
    
    private static CopyOnWriteArraySet<WebSocketServer> webSocketSet = new CopyOnWriteArraySet<WebSocketServer>();
    
    private Session session;

    @OnOpen
    public void onOpen(Session session) {
        this.session = session;
        webSocketSet.add(this);
        try {
            sendMessage("连接成功");
        } catch (IOException e) {
            logger.error("IO异常");
        }
    }

    @OnClose
    public void onClose() {
        webSocketSet.remove(this);
        logger.info("连接关闭");
    }

    @OnMessage
    public void onMessage(String message) {
        for (WebSocketServer item : webSocketSet) {
            try {
                item.sendMessage(message);
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }

    @OnError
    public void onError(Throwable error) {
        error.printStackTrace();
    }

    public static void sendInfo(String message){
        for (WebSocketServer item : webSocketSet) {
            try {
                item.sendMessage(message);
            } catch (IOException e) {
                continue;
            }
        }
    }

    public void sendMessage(String message) throws IOException {
        this.session.getBasicRemote().sendText(message);
    }
    
}
```



# maven

依赖搜索

https://developer.aliyun.com/mvn/search

打包

```
mvn clean install -Dmaven.test.skip=true
```

