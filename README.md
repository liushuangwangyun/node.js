# node.js

## 第二天笔记

## 异步式IO与事件驱动

阻塞模式下，一个线程只能处理一项任务，要想提高吞吐量必须通过多线程。而非阻塞 模式下，一个线程永远在执行计算操作，这个线程所使用的 CPU 核心利用率永远是 100%， I/O 以事件的方式通知。在阻塞模式下，多线程往往能提高系统吞吐量，因为一个线程阻塞时还有其他线程在工作，多线程可以让 CPU 资源不被阻塞中的线程浪费。而在非阻塞模式下，线程不会被 I/O阻塞，永远在利用 CPU。多线程带来的好处仅仅是在多核 CPU 的情况下利用更多的核，而Node.js的单线程也能带来同样的好处。

### 特点
（1）至少在两个对象之间需要协作

（2）两个对象都需要处理一系列的事情

## 阻塞和非阻塞

### 阻塞

阻塞的特点：是调用之后一定要等到系统内所有的操作完成后，调用才结束

阻塞的缺点：阻塞I/O造成CPU等待IO，浪费等待时间，CPU的处理能力不能得到充分利用

### 非阻塞

非阻塞的特点：调用之后会立即返回，返回之后CPU的时间片可以用来处理其他事件，性能明显提高

非阻塞的缺点：由于完整的I/O并没有完成, 立即返回的并不是业务层期望的数据, 而仅仅是当前调用的状态, 为了获取完整的数据, 应用程序需要重复调用I/O操作来确认是否完成. 这种重复调用判断操作是否完的技术叫轮询.

### 非阻塞的三种方法

* read 
* selsct 
* epoll 

## 异步IO

什么是异步：异步IO的概念和同步IO相对。当一个异步过程调用发出后，调用者不能立刻得到结果。实际处理这个调用的部件在完成后，通过状态、通知和回调来通知调用者。在一个CPU密集型的应用中，有一些需要处理的数据可能放在磁盘上。预先知道这些数 据的位置，所以预先发起异步IO读请求。等到真正需要用到这些数据的时候，再等待异步IO完成。使用了异步IO，在发起IO请求到实际使用数据这段时间 内，程序还可以继续做其他事情

异步IO就是把IO提交给系统，让系统替你做，做完了再用某种方式通知你, 通过信号，或者其他异步方式通知，这时候，操作系统已经帮你完成IO操作，具体来说就是你那个作为传入参数的的buffer的指针所指向的空间已经读到了数据或者你的buffer的数据已经写出去了.

例子：同步：CPU需要计算10个数据，没计算一个结果后，将其写入磁盘，等待写入成功后，再计算下一个数据，知道完成

异步：CPU需要计算十个数据，每计算一个结果后，将其写入磁盘，不等待写入成功与否的结果，立刻返回继续计算下一个数据，
计算过程中可以收到之前写入是否成功的通知，知道完成。

* 回调函数
* 事件
* EventEmitter

## node.js的事件循环机制

node.js程序由事件循环开始到事件循环结束，始终都在事件循环中程序的入口就是事件循环第一个事件的回调函数，事件的回调函数在执行过程中可以会出现IO请求或直接触发（emit）事件，在执行完毕后再返回事件循环，事件循环会检查事件队列中有没有未处理的事件，直到程序结束。



