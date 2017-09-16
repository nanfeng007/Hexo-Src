---
title: sleep和wait.md
date: 2017-08-12 10:20:34
tags:
categories: JAVA
---

### sleep（）方法
　　<p>sleep()使当前线程进入停滞状态（阻塞当前线程），让出CUP的使用、目的是不让当前线程独自霸占该进程所获的CPU资源，以留一定时间给其他线程执行的机会;
　　<p>sleep()是Thread类的Static(静态)的方法；因此他不能改变对象的机锁，所以当在一个Synchronized块中调用Sleep()方法是，线程虽然休眠了，但是对象的机锁并木有被释放，其他线程无法访问这个对象（即使睡着也持有对象锁）。
　　<p>在sleep()休眠时间期满后，该线程不一定会立即执行，这是因为其它线程可能正在运行而且没有被调度为放弃执行，除非此线程具有更高的优先级。

### wait（）方法
　　<p>wait()方法是Object类里的方法；当一个线程执行到wait()方法时，它就进入到一个和该对象相关的等待池中，同时失去（释放）了对象的机锁（暂时失去机锁，wait(long timeout)超时时间到后还需要返还对象锁）；其他线程可以访问；
　　<p>wait()使用notify或者notifyAlll或者指定睡眠时间来唤醒当前等待池中的线程。
　　<p>wiat()必须放在synchronized block中，否则会在program runtime时扔出”java.lang.IllegalMonitorStateException“异常。

---

所以sleep()和wait()方法的最大区别是：
　　　　sleep()睡眠时，保持对象锁，仍然占有该锁；
　　　　而wait()睡眠时，释放对象锁。
　　但是wait()和sleep()都可以通过interrupt()方法打断线程的暂停状态，从而使线程立刻抛出InterruptedException（但不建议使用该方法）。

---

```java
/**
 * Thread sleep和wait区别
 * @author DreamSea
 * 2012-1-15
 */
public class ThreadTest implements Runnable {
    int number = 10;

    public void firstMethod() throws Exception {
        synchronized (this) {
            number += 100;
            System.out.println(number);
        }
    }

    public void secondMethod() throws Exception {
        synchronized (this) {
            /**
             * (休息2S,阻塞线程)
             * 以验证当前线程对象的机锁被占用时,
             * 是否被可以访问其他同步代码块
             */
            Thread.sleep(2000);
            //this.wait(2000);
            number *= 200;
        }
    }

    @Override
    public void run() {
        try {
            firstMethod();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) throws Exception {
        ThreadTest threadTest = new ThreadTest();
        Thread thread = new Thread(threadTest);
        thread.start();
        threadTest.secondMethod();
    }
}

```

---

<p>我们来大致分析一下此段代码，main()方法中实例化ThreadTest并启动该线程，然后调用该线程的一个方法（secondMethod()），因为在主线程中调用方法，所以调用的普通方法secondMethod()）会先被执行（但并不是普通方法执行完毕该对象的线程方法才执行，普通方法执行过程中，该线程的方法也会被执行，他们是交替执行的，只是在主线程的普通方法会先被执行而已），所以程序运行时会先执行secondMethod()，而secondMethod()方法代码片段中有synchronized block，因此secondMethod方法被执行后，该方法会占有该对象机锁导致该对象的线程方法一直处于阻塞状态，不能执行，直到secondeMethod释放锁；
<p>使用Thread.sleep(2000)方法时，因为sleep在阻塞线程的同时，并持有该对象锁，所以该对象的其他同步线程（secondMethod()）无法执行，直到synchronized block执行完毕（sleep休眠完毕），secondMethod()方法才可以执行，因此输出结果为number*200+100；
<p>使用this.wait(2000)方法时，secondMethod()方法被执行后也锁定了该对象的机锁，执行到this.wait(2000)时，该方法会休眠2S并释当前持有的锁，此时该线程的同步方法会被执行（因为secondMethod持有的锁，已经被wait()所释放），因此输出的结果为：number+100;
* 【显示流程】
<p>sleep()和wait()方法的区别已经讲解完毕，若对线程有兴趣的童鞋我在诺诺的问问：在main方法中最后行加入“System.out.println("number="+threadTest.number);”猜猜会输出什么结果。。。J

---
