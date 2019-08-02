## JMM Java内存模型

JMM解决的问题是它屏蔽了操作系统和各种硬件对内存访问的差异性问题。

* JMM
  * sync
  * happens-before（Java1.5之后Java增加了这个原则来解决乱序问题）
  * volatile
  * 

* 多线程情况下会有编译器优化和内存优化,而造成乱序的问题。


> 内存可见性问题，Java中是没有内存可见性问题的。CPU遵循了mesi协议，也就解决了硬件的L1 L2 L3 缓存一致性问题。
    mesi强一致性 mesif弱一致性
### CPU保证了一致性问题，那为什么会有JMM？  
因为JMM要屏蔽硬件的差异。
### 那么为什么会出现不一致的问题？   
一切的“可见性”问题都是由于编译优化，指令提取导致的，也就是说，编译后的代码是“优化”过的，跟你书写的意图只有在多线程的情况下才做优化，单线程是不会做优化的。

``` java
public class Demo{

    boolean flag = true;

    public void test() {

        Thread t1 = new Thread(() -> {
            while (flag){

            }
        });
        t1.start();

        Thread t2 = new Thread(() -> {
            flag = false;
        });
        t2.start();
    }
}
```
