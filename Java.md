# Java笔记

## 多线程数据传递

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
        thread.join();
        System.out.println("value1:" + thread.value1);
        System.out.println("value2:" + thread.value2);
    }
}
```

