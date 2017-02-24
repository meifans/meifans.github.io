#编发包

## ThreadPoolExecutor
一个ExecutorService(接口)实现，使用几个线程执行每个提交的task，通常可以使用Executors的工厂方法来配置。

线程池解决了2个问题 ：
  + 当执行大量的异步任务时，它提供更高的性能，因为它减少了每个任务执行前创建线程的消耗。
  + 提供了一种手段，准备和管理执行一个集合的任务所需要的资源，包括线程，消耗。同时也统计了一些数据，例如完成任务的个数等。

为了便于使用，提供了Executors工厂 ：
  + newCachedThreadPool 线程数无限，自动扩容。
  + newFixedThreadPool 固定线程数量。
  + newSingleThreadExecutor 单个线程。

提供了参数调整 ：
  + corePoolSize：        线程池维护线程的最少数量
  + maximumPoolSize：     线程池维护线程的最大数量
  + keepAliveTime：       线程池维护线程所允许的空闲时间
  + unit：                线程池维护线程所允许的空闲时间的单位
  + workQueue：           线程池所使用的缓冲队列
    + 运行线程数<core    首选增加一个线程而不是放到队列
    + 运行线程数>=core   首选把新任务放到队里，而不是创建一个线程
    + 如果无法放到队列，新建一个线程处理任务，除非已经超过了最大线程数。此时任务被拒绝。
  + handler：             线程池对拒绝任务的处理策略

有三种Queue的选择 ：
  + SynchronousQueue ： 直接提交，而不是放到queue。通常需要无限的maximumPoolSize,CachedThreadPool使用。
    + 无界队列，但是由于本身的特性，`某次添加元素后必须等待其他线程取走后才能继续添加`。
    + 可以避免在处理具有内部依赖性的请求时出现锁。因为b依赖于a,先后提交a,b,可以保证a必定先被执行。

  + LinkedBlockingQueue ： 无限队列,当所有线程繁忙时，会把任务放到queue中等待。FixedThreadPool和SingleThreadExecutor 使用。
    > corePoolSize熟练的线程一直在跑，永远也不会触发新的线程 （因为队列无界）
    
  + ArrayBlockingQueue : 固定数量队列。当maximumPoolSize数量固定时，防止资源枯竭。
