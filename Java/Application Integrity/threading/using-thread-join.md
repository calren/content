# Using `Thread.join`
author: adamMontgomerie

levels:

  - medium

type: normal

category: feature

links:

- '[docs.oracle.com](https://docs.oracle.com/javase/tutorial/essential/concurrency/join.html)'
- '[More on Joining](https://docs.oracle.com/javase/tutorial/essential/concurrency/join.html)'
- '[More on InterruptedException](https://docs.oracle.com/javase/7/docs/api/java/lang/InterruptedException.html)'

---
## Content

On the other hand, `join()` method is not static and is specific to every thread. The key point of this function is to wait until the thread finishes running and terminates. This can be useful when each of the running threads performs a calculation and then you want to combine the results in some way. In order to do that you must ensure that all the threads have finished their calculations otherwise it will result a wrong answer in the end.

An example of using `join()`:

```
class Add extends Thread {
  public int result;
  public void run() {
		value = 3+5;
	}
}

class Mul extends Thread {
  public int result;
  public void run() {
    value = 3*5;
  }
}

public class Main{
	public static void main(String[] args){
		Add t1 = new Add();
		Mul t2 = new Mul();

		t1.start();
		t2.start();

    //try to wait until both
    //threads calculate the result
		try {
			t1.join();
			t2.join();
		} catch (InterruptedException e) {
			e.printStackTrace();
		}

    //only combine results after
    //both threads finished
    double n =
          ((double)t2.result/t1.result);
	}
}
```

In this case `n` is calculated after we get the results form t1 an t2. If there was no joining module the result would not necessarily be 15/8 and could lead to a `null` result.

The try/catch block is important as when we call `join()` methods on our threads we are relying on the fact that they finish their execution. During this process they might get interrupted for whatever reason which will cause incorrectness of the end result.

---
## Practice

What does `join()` method do?

???

* It waits until a thread finished executing
* It pauses execution of a thread for a certain time
* It pauses all the threads in a queue
* It frees all the resources that the current thread is holding

---
## Revision

What method waits until a thread has finished executing?

???

Consider the following snippet:
```
Thread t1 = new Thread();
Thread t2 = new Thread();
t1.start();
t2.start();
t1.join();
```

The `t1.join()` method call will? ???

* join()
* wait until t1 to dies
* sleep()
* wait()
* combine()
* immediately start t2
* pause t1 until t2 dies
* speed up t1
