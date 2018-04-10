---
layout:     post
title:      Thread VS Runnable,concurrent
date:       2016-09-15 21:35:18
summary:    Thread VS Runnable,concurrent
categories: Thread VS Runnable,concurrent
thumbnail: MutiThread
author: "shadow"
tags:
 - MutiThread
 - shadow grand
---

java 多线程 thread runnable

```java
import java.util.Date;

public class RunnableClass  implements Runnable{
	private int count=6;
	@Override
	public void run() {
			for (int i = 0; i < count; count--) {
System.out.println(new Date()+"\t"+Thread.currentThread().getName()+"\t"+(char)('g'-count));
			}
	}
}
```

 ![runnable](/image/runnable.png)



```java
import java.util.Date;

public class ThreadClass extends Thread{
	private int count=6;
	public ThreadClass() {
		super();
	}
	@Override
	public void run() {
		for (int i = 0; i < count; count--) {
			System.out.println(new Date()+"\t"+this.getName()+"\t"+(char)('a'-count));
		}
	}
}

```

 ![thread](/image/thread.png)

此问题也很好理解，runnable 对象表示一个期望执行的任务，他通过将自己传递给一个线程，依附线程执行，而同一个runnable对象内部的变量必然是自己共享的，（多线程下的操作数据都是存在线程的工作内存中，而这些数据来自于主内存中拷贝副本，如果是同一个runnable对象生成的线程，其资源必然是共享的，为了线程安全可以实现synchronized等进行加锁机制执行保证不会产生脏数据。而另一种情况，通过extends实现的多线程方式，多个线程之间是独立的，使用不同的runnable对象，必然产生的内存都是各自取各自的，只是达到了并发执行的结果而已，实际任务都是单独进行的。他们之间也可以实现共享数据）这就使得多线程下资源共享成为可能.

那么通过这个实例可以理解两个方法的区别，结合实际情况合理使用是最终目的。



如上说到过，线程共享会产生一定错误，比如两个线程对于共享数据同时进行读写，则容易产生脏数据，或者写无效等等。为了规避这些不希望出现的错误，JAVA提供了许多方法实现，现在我们来学习一下JAVA的同步锁机制。

1. synchronized 
   1. 通过synchronized修饰实例方法时，该方法被执行的唯一条件是获得当前实例的内置锁，方法执行完自动释放锁。同一个类的不同实例拥有不同的内置锁，每一个实例只有一个内置锁，当有多个方法被synchronized 修饰，那么当多个线程同时调用同一个实例的不同方法时，需要竞争内置锁。那么此处可以回想一下为什么当时说hashtable是线程安全的，但是没有被广泛采用，就是因为在其实现时存在许多synchronized 修饰的方法，使得读和读，读和写，写合写，无法做到并发执行。
      接着就有jdk2.0 引入的hashmap类，线程不安全，原因就是内部没有并发同步机制，所以在并发条件下，一般建议采用ConcurrentHashMap。一个更加灵活高效的哈希表实现。
   2. 当synchronized 修饰静态方法，该方法的执行需要获取该类的class对象的内置锁，而这个锁每一个类是唯一的，
   3. 而如果修饰代码块，则需要获得该入参位置的对象所拥有的内置锁。
2. volatile 并不属于同步机制决定作用的修饰符，他的主要作用是为了保证数据的线程可见性，（可见性：当一个线程修改了共享变量的值，其他线程能够立即得知这个值的修改）
3. wait(),notify(),notifyAll()>>>>await(),signal,signalAll()
