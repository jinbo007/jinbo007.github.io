# Kotlin协程初探
## 1.简介
### 1.1定义：
- 协程是一种**并发设计模式**，可以用于在 Android 平台上使用它来简化**异步执行**的代码。

示例代码:
```
suspend fun fetchDocs() {
    val result = get("developer.android.com")
    show(result)
}
```
之前的代码是这样的
```
fun fetchDocs() {
    get("developer.android.com") { result ->
        show(result)
    }
}
```
### 1.2 协程特性
协程是一种异步任务的解决方案，主要有以下几个特性:
- **轻量**

轻量是对比线程的，比如同时开启10万个协程
```
 repeat(100_000) {
        launch {
            delay(5000L)
            print(".")
        }
    }
```
试试用假如开启10万个线程
```
//Exception in thread "main" java.lang.OutOfMemoryError: unable to create new native thread
    repeat(100_000) {
         Thread {
             Thread.sleep(1000)
             print(".")
         }.start()
    }

```
- **内存泄漏更少**

- **内置(自动)取消支持**
 取消操作会自动在运行中的整个协程层次结构内传播

- **jetpack集成**

    [jetpackPack扩展](https://developer.android.com/kotlin/ktx)、[协程作用域](https://developer.android.com/topic/libraries/architecture/coroutines)

## 2. 协程名词及概念
### 2.1协程作用域（CoroutineScope)
- **CoroutineScope**([Android官网](https://developer.android.com/kotlin/coroutines/coroutines-adv#coroutinescope))会跟踪它使用 launch 或 async 创建的所有协程。

![图片](https://github.com/jinbo007/Course/blob/master/kotlin/img/CoroutineCoext%E6%93%8D%E4%BD%9C%E4%BC%98%E5%85%88%E7%BA%A7.png?raw=true)
#### 常见作用域
- GlobalScope(全局作用域)
- runBlocking （顶级函数，内置作用域）
- coroutineScope（独立作用域）
- supervisorScope（监督作用域）


### 2.2 协程上下文(CoroutineContext)
==**关键元素分析**==
#### 2.2.1 Job(作业)

Job 是协程的句柄，可以用于控制协程的生命周期。[Android官网-详细点击](https://developer.android.com/kotlin/coroutines/coroutines-adv?hl=zh-cn#job)
使用 launch 或 async 创建的每个协程都会返回一个 Job 实例，该实例是相应协程的唯一标识并管理其生命周期。您还可以将 Job 传递给 CoroutineScope 以进一步管理其生命周期，如以下示例所示
```
   val job = scope.launch {

   }
   job.cancel()//取消协程
   job.join()//等待协程完成

   val job2 = scope.async {
        "result"
   }

    job2.cancel()//取消协程
    job2.join()//等待完成
    job2.await()//返回结果

```
- 一个Job的生命周期
![Job生命周期](https://github.com/jinbo007/Course/blob/master/kotlin/img/Job生命周期图.png?raw=true)
#### 2.2.2 CoroutineDispatcher(协程调度器)
将工作分派到适当的线程（类似Rxjava 的 Schedulers.io())
Koltin提供了三个调度程序:[Android官网-详细点击](https://developer.android.com/kotlin/coroutines/coroutines-adv?hl=zh-cn#main-safety)
- Dispatchers.Main
###### 使用此调度程序可在 Android 主线程上运行协程。此调度程序只能用于与界面交互和执行快速工作。示例包括调用 suspend 函数，运行 Android 界面框架操作，以及更新 LiveData 对象。
- Dispatchers.IO IO
###### 此调度程序经过了专门优化，适合在主线程之外执行磁盘或网络 I/O。示例包括使用 Room 组件、从文件中读取数据或向文件中写入数据，以及运行任何网络操作。
- Dispatchers.Default ,
###### 此调度程序经过了专门优化，适合在主线程之外执行占用大量 CPU 资源的工作。用例示例包括对列表排序和解析 JSON

- 切换线程示例代码
```
suspend fun fetchDocs() {                      // Dispatchers.Main
    val result = get("developer.android.com")  // Dispatchers.Main
    show(result)                               // Dispatchers.Main
}

suspend fun get(url: String) =                 // Dispatchers.Main
    withContext(Dispatchers.IO) {              // Dispatchers.IO (main-safety block)
        /* 处理网络IO流程  */                     // Dispatchers.IO (main-safety block)
    }                                           // Dispatchers.Main
    //方法二
    launch(Dispatchers.Default){
        //
    }
}
```
- 动图说明
![示例图片](https://github.com/jinbo007/Course/blob/master/kotlin/img/%E5%AE%98%E7%BD%91%E5%8A%A8%E5%9B%BE_fetchDocs().gif?raw=true)

#### 2.2.3 CoroutineName (协程名称)
- 协程的名称，可用于调试时识别当前协程信息

#### 2.2.4 CoroutineExceptionHandler （协程异常捕获器）
- 处理未捕获的异常。

#### 问题Q1. CoroutineScope 和 CoroutineContext 区别
参考代码：
```
public interface CoroutineScope {
  public val coroutineContext: CoroutineContext
}
```
[谈谈 Kotlin 协程的 Context 和 Scope](https://blog.yujinyan.me/posts/kotlin-coroutine-context-scope/)

## 3.常用操作
### 3.1 开启作用域
#### 3.1.1 GlobalScope

 **全局作用域**，这意味着通过 GlobalScope 启动的协程的生命周期只受整个应用程序的生命周期的限制，只要整个应用程序还在运行且协程的任务还未结束，协程就可以一直运行
 GlobalScope **不会阻塞其所在线程**，所以以下代码中主线程的日志会早于 GlobalScope 内部输出日志。

调用示例:

```
        //直接使用
         GlobalScope.launch {
               delay(400)
               log("GlobalScope")
         }
```
```
        //指定线程
        GlobalScope.launch(Dispatchers.Default) {
              delay(400)
              log("GlobalScope")
        }

        //指定线程 和 异常捕获器
```
```
        //自定义异常捕获
         val exceptionHandler = CoroutineExceptionHandler { _, e ->
                println("捕捉到一异常$e")
         }
         GlobalScope.launch(Dispatchers.IO + exceptionHandler) {
               delay(400)
               log("GlobalScope")
         }

```
#### 3.1.2 runBlocking
    可以使用 runBlocking 这个顶层函数来启动协程，常用于测试场景

调用示例:

```
    fun main()= runBlocking {
        launch {
            delay(500)
            log("runBlocking")
        }
        log("runBlocking finish")
    }
```
#### 3.1.3 coroutineScope（独立作用域）
    coroutineScope 函数用于创建一个独立的协程作用域，直到所有启动的协程都完成后才结束自身
```
    runBlocking {
        launch {
            delay(100)
            log("Task from runBlocking")
        }
        coroutineScope {
            log("Task from coroutine scope")
            launch {
                delay(500)
                log("Task from nested launch")
            }
        }
    }
    log("Coroutine scope is over")
```
    输出结果
```
Task from coroutine scope
Task from runBlocking
Task from nested launch
Coroutine scope is over

```

- 独立作用域示意图

![示意图](https://github.com/jinbo007/Course/blob/master/kotlin/img/%E7%BB%93%E6%9E%84%E5%8C%96%E5%B9%B6%E5%8F%91-coroutineScope.gif?raw=true)

#### 3.1.4 supervisorScope（监督作用域）
    supervisorScope 函数用于创建一个使用了 SupervisorJob 的 coroutineScope，该作用域的特点就是抛出的异常不会连锁取消同级协程和父协程
```
    runBlocking {
        supervisorScope {
            launch {
            /*  job */
            }
        }
    }
```

#### 3.1.5 自定义CoroutineScope
```
     val handler = CoroutineExceptionHandler { _, e ->
            println("捕捉到一就异常$e")
        }
      CoroutineScope(Job() + Dispatchers.Main + CoroutineName("hello") + handler)
```

### 3.2 开启协程
#### 3.2.1 launch
- 不阻塞当前线程
- 返回Job对象
- 执行结果无返回

```
       coroutineScope {
            launch {
                repeat(3) {
                    delay(100)
                    log("launchA - $it")
                }
            }
           launch {
                repeat(3) {
                    delay(100)
                    log("launchB - $it")
                }
            }
        }
```
    执行结果
```
    [main] launchA - 0
    [main] launchB - 0
    [main] launchA - 1
    [main] launchB - 1
    [main] launchA - 2
    [main] launchB - 2
```

#### 3.2.2 async
   - 不阻塞当前线程
```
   coroutineScope {
       val startTime = System.currentTimeMillis()
       val asyncA = async {
           delay(3000)
           1
       }
       val asyncB = async {
           delay(3000)
           2
       }
       //打印结果: 结果是3,耗时3020
       println("结果是${asyncA.await() + asyncB.await()},耗时${System.currentTimeMillis()-startTime}")

   }
```


  -  说明：即使不调用 await(),coroutineScope也会等待子协程运行完成之后，才返回
   参考代码：

```
     val startTime = System.currentTimeMillis()
     coroutineScope {
         val asyncA = async {
             delay(3000)
             1
         }
         val asyncB = async {
             delay(3000)
             2
         }
         val listOf = listOf(asyncA, asyncB)
         listOf.awaitAll()

     }
     //打印结果：耗时3092
     println("耗时${System.currentTimeMillis()-startTime}")
```
Tips：
对于在作用域内创建的新协程，系统会为新协程分配一个新的 Job 实例，而从包含作用域继承其他 CoroutineContext 元素。可以通过向 launch 或 async 函数传递新的 CoroutineContext 替换继承的元素。请注意，将 Job 传递给 launch 或 async 不会产生任何效果，因为系统始终会向新协程分配 Job 的新实例。
示例代码是这样的
```
        val subJob = Job()//准备创建的Job

        val job1 = scope.launch {
        }

        val job2 = scope.launch(subJob + Dispatchers.Default) {
            //此处的subJob指定是无效的，会被创建一个新的
        }
```
![示意图](https://github.com/jinbo007/Course/blob/master/kotlin/img/父子协程不同的Job.png?raw=true)

### 3.3协程操作
#### 3.3.1 join()
- 等待协程结束
```
   coroutineScope {
       val job = launch {
           delay(100)
           println("子协程执行完成")
       }
       job.join()
       println("全部任务完成")
   }
    //打印结果
    子协程执行完成
    全部任务完成
```
#### 3.3.2 cancel()
- 取消协程
```
   coroutineScope {
       val job = launch {
           delay(100)
           println("子协程执行完成")
       }
       job.cancel()
       println("全部任务完成")
   }
   //打印结果
   全部任务完成
```
#### 3.3.3 cancelAndJoin()
- 取消协程并等待
```
    coroutineScope {
        val job = launch {
            println("打印1.子协程执行完成")
            Thread.sleep(200)
            //delay(200)
            println("打印2.我可以被打出来，是因为会等待")
        }
        delay(100)
        job.cancelAndJoin()
        println("打印3.全部任务完成")
    }
```
#### 3.3.3.4 await()
- 可以返回async执行的结果
```
    val job = async {
        delay(500)
        222
    }
    var value = job.await()
    //打印结果是:结果是222
    println("结果是$value")

```

#### 3.3.3.5 awaitAll()
- 等待全部结果都返回
```
  val time = measureTimeMillis {
      val job = async {
          delay(1000)
          222
      }

      val job2 = async {
          delay(2000)
          333
      }
      println("计算结果:${job.await() + job2.await()}")
      val jobs = listOf(job, job2)
      jobs.awaitAll()


  }

  println("总耗时: $time")

  //打印结果：
  计算结果:555
  总耗时: 2030

```

## 4.异常处理
### 4.1 异常传播机制
#### 4.1.1 独立作用域的传播机制（协同作用域）
- 取消它自己的子级
- 取消它自己
- 将异常传播并传递给它的父级
- 不能独立处理异常

[独立作用域传播特性]
![示意图片](https://github.com/jinbo007/Course/blob/master/kotlin/img/coroutineScope异常传播.gif?raw=true)

#### 4.2.2监督作用域的传播机制（主从作用域）

- 取消自己和子级
- 可以独立处理异常

##### 监督作用域传播特性
![示意图](https://github.com/jinbo007/Course/blob/master/kotlin/img/SuperVisor异常传播机制.png?raw=true)

##### 来个例子
![图片1](https://github.com/jinbo007/Course/blob/master/kotlin/img/%E5%8D%8F%E7%A8%8B%E5%BC%82%E5%B8%B8%E4%BC%A0%E6%92%AD%E5%88%86%E6%9E%90.png?raw=true)

路线图：
- C2-1发生异常的时候，C2-1->C2->C2-2->C2->C1->C3（包括里面的子协程）->C4
- C3-1-1发生异常的时候,C3-1-1->C3-1-1-1，其他不受影响
[本部分参考来源-协程异常机制与优雅封装](https://juejin.cn/post/6935472332735512606#heading-18)


### 4.2 细节

 - 取消异常会被忽略(不会取消它的父协程)- Cancellation
 - 父协程会等待子协程处理完成之后才开始处理异常
 - 异常聚合 如果有多个异常，将会处理第一个异常信息（其他异常信息附加后边）
 - 异常可以在try-catch包装执行后再上送
 - 监督任务，内部子协程之间的异常不会相互传递，即平级协程不影响
 - 监督子协程可以自行处理自己的异常信息

[详细参考-Kotlin官网-异常处理与监督](https://www.kotlincn.net/docs/reference/coroutines/exception-handling.html)

## 5.扩展
jetpack扩展
- viewModelScope(android-ktx)
- lifecycleScope(android-ktx)

协程就是Callback?
[CPS转换](https://juejin.cn/post/6883652600462327821#heading-13)

## 6.系列课程，下次一定？
#### **Kotlin系列二之Kotlin协程在Android上的应用**
#### **Kotlin系列三之Kotin之Chanel、Flow**

#### 官网资料

[ Kotlin 协程](https://developer.android.com/kotlin/coroutines)
[协程概览](https://play.kotlinlang.org/hands-on/Introduction%20to%20Coroutines%20and%20Channels/01_Introduction)
[协程官网推荐的学习资料](https://developer.android.com/kotlin/coroutines/additional-resources)

#### 协程上的取消和异常机制(Cancellation and Exceptions in Coroutines-Manuel Vivo)
[前提内容 First things first(Part 1)](https://medium.com/androiddevelopers/coroutines-first-things-first-e6187bf3bb21)
[协程的取消机制 Cancellation in coroutines (Part 2)](https://medium.com/androiddevelopers/cancellation-in-coroutines-aa6b90163629)
[协程中的异常处理 Exceptions in coroutines-part3](https://medium.com/androiddevelopers/exceptions-in-coroutines-ce8da1ec060c)
[协程不应该取消的设计模式 Coroutines & Patterns for work that shouldn’t be cancelled-Part 4](https://medium.com/androiddevelopers/coroutines-patterns-for-work-that-shouldnt-be-cancelled-e26c40f142ad)

#### 协程在Android上的应用-Sean McQuillan
[Coroutines on Android (part I): Getting the background](https://medium.com/androiddevelopers/coroutines-on-android-part-i-getting-the-background-3e0e54d20bb)
[Coroutines on Android (part II): getting started](https://medium.com/androiddevelopers/coroutines-on-android-part-ii-getting-started-3bff117176dd)
[Coroutines On Android (part III): real work ](https://medium.com/androiddevelopers/coroutines-on-android-part-iii-real-work-2ba8a2ec2f45b)

#### RicardoMJiang系列博客
[关于协程你应该知道的知识点](https://juejin.cn/post/6934337634831433736)
[协程到底是什么?](https://juejin.cn/post/6973650934664527885)
[协程到底是怎么切换线程的](https://juejin.cn/post/6981056016897015838)
[协程异常机制与优雅封装](https://juejin.cn/post/6935472332735512606)
[协程异常到底是怎么传播的?](https://juejin.cn/post/6988876911338323981)

#### 朱涛的自习室
[Kotlin Jetpack 实战 | 09. 图解协程原理](https://juejin.cn/post/6883652600462327821)

#### 其他
[一文快速入门 Kotlin 协程](https://juejin.cn/post/6908271959381901325#heading-32)
[一文看透 Kotlin 协程本质](https://juejin.cn/post/6987724340775108622#heading-25)