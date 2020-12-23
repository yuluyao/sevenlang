Java 基础
    Java 数据类型
        基本类型
            byte：8位
            char：16位
            short：16位
            int：32位
            long：64位
            float：32位
            double：64位
            boolean
            ｜ boolean 只有两个值：true、false，可以使用 1 bit 来存储，但是具体大小没有明确规定。JVM 会在编译时期将 boolean 类型的数据转换为 int，使用 1 来表示 true，0 表示 false。JVM 支持 boolean 数组，但是是通过读写 byte 数组来实现的。
        包装类型
            每种基本类型都有与之对应的包装类型
            自动拆装箱
                拆箱条件
                    包装类型赋值给基本类型
                    包装类型与基本类型比较、运算
                    包装类型之间进行运算
                装箱条件
                    基本类型赋值给包装类型
                装箱缓存机制
                    整数值区间-128 至 +127，自动装箱时，会使用常量池中的缓存包装类型对象。
    Java String类
        不可变的好处
            可变将会影响已经计算过的hash值
            不可变所以线程安全
        StringBuilder、StringBuffer
            后者是线程安全的，但效率更低
        字符串常量池
            编译时确定的字符串常量
            intern()方法添加的字符串常量
    Java 关键字
        final
            final变量不可以重新赋值
            final方法不可以被重写
            final类不可以被继承
        static
            static变量属于类，只有1份
            static方法不能是抽象的
            static代码块在类初始化时执行1次
            static内部类可以直接创建其对象，而非static内部类必须依赖外部类的实例才可以创建对象。
            初始化顺序
                父类（静态变量、静态语句块）
                子类（静态变量、静态语句块）
                父类（实例变量、普通语句块）
                父类（构造函数）
                子类（实例变量、普通语句块）
                子类（构造函数）

    Java 抽象类与接口
        抽象类
            不能直接实例化
            可以没有抽象方法，但有抽象方法的类就必须声明为抽象
        接口
            不能直接实例化
            只能有抽象方法，但Java 8以后可以有默认方法实现
            接口的成员默认为public，也只能是public。
            接口的字段默认是static final的。
    Java 异常
        继承关系
            Throwable
                Error：错误
                    错误是应用程序无法处理的。
                Exception：异常
                    RuntimeException：运行时异常
                    IOException：非运行时异常
        异常的分类
            1. 可查异常（非运行时异常）
                除了RuntimeException及其子类，其它异常都是可察异常
                要么try-catch捕获异常，要么throws抛出异常
            2. 不可查异常（运行时异常）
                运行时异常
                    RuntimeException及其子类
        异常处理机制
            对于一个可查异常，要么抛出，要么捕获。
            捕获异常（try-catch-finally）
                try：用于捕获异常。其后可接零个或多个catch块，如果没有catch块，则必须跟一个finally块。
                catch：用于处理try捕获到的异常。
                finally：无论是否捕获或处理异常，finally块里的语句都会被执行。注意：当在try块或catch块中遇到return语句时，finally语句块将在方法返回之前被执行。
            抛出异常
                throws：在方法声明中抛出异常，可抛出多个。
                throw：在方法体中抛出异常对象。
    Java 泛型
        三种泛型
            1. 泛型类
                静态方法无法访问类上定义的泛型。
            2. 泛型方法
                泛型方法可以存在于泛型类中，也可以存在于普通类中。
                优先使用泛型方法而不是泛型类去解决问题。
            3. 泛型接口
        泛型擦除
            泛型参数只保留到编译时期。
            泛型参数在运行时会被擦除。
            擦除到该泛型的第一个边界，由extends定义，如果没有extends则边界就是Object类型。
        泛型通配符
            上界通配符<? extends T>
            下界通配符<? super T>
            <?>无限通配符
        参考：深入理解Java泛型 -- 掘金
        ｜ https://juejin.im/post/5b614848e51d45355d51f792#heading-13
    Java 反射
        什么是Java反射
            Java 反射机制在程序运行时，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性。这种 动态的获取信息 以及 动态调用对象的方法 的功能称为 java 的反射机制。
        使用反射获取类的信息
            反射需要用到的几个类：Class，Field，Method，Constructor。
            获取类名
            ｜ getName()
            获取所有public变量
            ｜ getFields()
            获取所有声明的变量（包括public与非public）
            ｜ getDeclaredMethods()
            获取某个public变量
            ｜ ​getField(String name)
            获取某个声明的变量
            ｜ getDeclaredField(String name)
            获取访问修饰符
            ｜ getModifiers()
            获取所有public方法
            ｜ getMethods()
            ...
        使用反射访问类的私有属性
            访问私有方法
            修改私有变量
            修改私有常量
        Java反射由浅入深 -- 掘金
        ｜ https://juejin.im/post/598ea9116fb9a03c335a99a4
Java 集合
    Java 集合框架
        集合框架分为Collection体系，和Map体系。
        Collection
            List
            Set
            Queue
        Map
    常用集合分类
        非线程安全
            ArrayList
            LinkedList
            HashSet
            HashMap
        线程安全，过时
            Vector
            HashTable
        线程安全，推荐
            CopyOnWriteArrayList
            CopyOnWriteArraySet
            ConcurrentHashMap
    常见集合源码分析
        ArrayList源码分析
            底层数据结构：数组
            transient Object[] elementData;
            初始容量10
            private static final int DEFAULT_CAPACITY = 10;
            每次扩容为原来的1.5倍
            int newCapacity = oldCapacity + (oldCapacity >> 1);
            扩容使用Arrays.copy()方法
            elementData = Arrays.copyOf(elementData, newCapacity);
            Arrays.copy()调用了本地方法System.arraycopy()
        LinkedList源码分析
            底层数据结构：链表
                双向链表节点
            初始大小0
            transient int size = 0;
            头节点
            transient Node<E> first;
            尾节点
            transient Node<E> last;
            LinkedList源码解析
            ｜ https://blog.csdn.net/zxt0601/article/details/77341098
        HashMap源码分析
            底层数据结构：数组+链表或红黑树
                1. 数组，也称为哈希桶
                2. 链表或红黑树
                链表节点
                红黑树节点
            哈希定位
                对key的hashCode进行扰动，hash值更均匀
                用位运算实现求余（因为容量是2的幂），效率更高
            哈希碰撞
                链地址法
                链表长度到达8，则链表换为红黑树
            扩容
                每次扩容，长度保持为2的幂
                扩容后，将所有Node移动到新的哈希桶中，开销较大
                扩容后，所有Node重新定位
            HashMap源码解析
            ｜ https://blog.csdn.net/zxt0601/article/details/77413921
        LinkedHashMap源码分析
            节点数据结构
            继承HashMap，区别在于在节点中增加字段以维护双链表，目的是实现有序遍历
            LinkedHashMapEntry<K,V> before, after;
            同时，HashMap中红黑树的节点原本就继承了这里的LinkedHashMapEntry
            LinkedHashMap源码解析
            ｜ https://blog.csdn.net/zxt0601/article/details/77429150
    典型数据结构的实现
Java 多线程
    线程状态（6种）
        NEW
        RUNNABLE
            READY
            RUNNING
        BLOCKED
        WAITING
        TIME_WAITING
        TERMINATED
    Java 锁
        Monitor机制
            每一个对象都有一个monitor，即监视器。
            Monitor的机制如下图：
            The Owner：同一时刻，只能有一个对象持有monitor。
            Entry Set：当一个线程要获取monitor时，会首先进入entry-set排队，如果monitor没有被其它线程持有，这个线程会和wait-set中被唤醒的其它线程竞争monitor。
            Wait Set：当一个线程持有monitor时，该monitor关联的对象调用了wait()方法，那么这个线程会释放monitor，并且进入wait-set中等待。然后，当该monitor关联的对象调用了notify()或notifyAll()方法后，wait-set中的线程被唤醒，被唤醒的线程将与entry-set中的线程竞争monitor。（notify()方法会随机唤醒一个线程。）
        死锁的4个条件
            互斥条件：该资源任意一个时刻只由一个线程占用。
            请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放。
            不剥夺条件：线程已获得的资源在末使用完之前不能被其他线程强行剥夺，只有自己使用完毕后才释放资源。
            循环等待条件：若干进程之间形成一种头尾相接的循环等待资源关系。
        锁的分类
            线程是否锁住同步资源？
                锁住
                    悲观锁
                        认为自己在使用数据的时候一定有别的线程来修改数据。
                        synchronized关键字和Lock的实现类都是悲观锁。
                不锁住
                    乐观锁
                        认为自己在使用数据时不会有别的线程修改数据。
                        无锁编程，CAS算法，Java原子类。
            锁住同步资源失败，线程是否阻塞？
                阻塞
                不阻塞
                    自旋锁
                        避免线程切换的开销。
                        要占用处理器的时间。
                    适应性自旋锁
                        自动调节自旋等待时间。
                        CAS算法，Java原子类。
            多个线程竞争同步资源的流程细节区别？
                不锁住资源，多个线程中只有一个能修改资源成功，其它线程会重试。
                    无锁
                同一个线程执行同步资源时自动获取资源。
                    偏向锁
                多个线程竞争同步资源时，没有获取资源的线程自旋等待锁释放。
                    轻量级锁
                多个线程竞争同步资源时，没有获取资源的线程阻塞等待唤醒。
                    重量级锁
            多个线程竞争锁时要不要排队？
                排队
                    公平锁
                先插队，插队失败再排队
                    非公平锁
            一个线程中的多个流程能不能获取同一把锁？
                能
                    可重入锁
                不能
                    非可重入锁
            多个线程能不能共享一把锁？
                能
                    共享锁
                不能
                    排他锁
    线程调度相关方法
        Object
            wait()：释放锁。
            notify()：随机唤醒。
            notifyAll()：唤醒所有。
        Thread
            sleep()：不释放锁。线程暂停。
            yield()：使用线程从RUNNING回到RUNNABLE状态，以使其它相同优先级的线程有运行的机会。
            join()：等待子线程执行完。
    启动线程的方式
        Thread
        Runnable
        Callable
    Java 线程池
        ThreadPoolExecutor类
            构造方法参数
                int corePoolSize：核心池的大小，核心池在初始状态下，没有线程，当有任务过来时，会创建线程，直到达到corePoolSize个数。
                int maximumPoolSize：线程数的上限，当任务队列满时，会额外创建临时线程，临时线程与核心线程的总数达到maximumPoolSize后，会采用拒绝策略。
                long keepAliveTime：临时线程的空闲时长，超过corePoolSize的线程的idle时长，超过这个时间，多余的线程会被回收。
                TimeUnit unit：时间的单位
                BlockingQueue<Runnable> workQueue：任务队列，核心线程无空闲，则新任务进入队列中，队列满，则创建临时线程。
                ThreadFactory threadFactory：新线程的产生方式
                RejectedExecutionHandler handler：拒绝策略
            线程池的任务处理策略
                如果当前线程池中的线程数目小于corePoolSize，则每来一个任务，就会创建一个线程去执行这个任务；
                如果当前线程池中的线程数目>=corePoolSize，则每来一个任务，会尝试将其添加到任务缓存队列当中，若添加成功，则该任务会等待空闲线程将其取出去执行；若添加失败（一般来说是任务缓存队列已满），则会尝试创建新的线程去执行这个任务；如果当前线程池中的线程数目达到maximumPoolSize，则会采取任务拒绝策略进行处理；
                如果线程池中的线程数量大于 corePoolSize时，如果某线程空闲时间超过keepAliveTime，线程将被终止，直至线程池中的线程数目不大于corePoolSize；如果允许为核心池中的线程设置存活时间，那么核心池中的线程空闲时间超过keepAliveTime，线程也会被终止。
                总结：corePoolSize -> 任务队列 -> maximumPoolSize -> 拒绝策略
            任务队列种类
                直接提交队列synchronousQueue：这个队列比较特殊，它不会保存提交的任务，而是将直接新建一个线程来执行新来的任务。
                无界任务队列LinkedBlockingQueue：基于链表的先进先出队列，如果创建时没有指定此队列大小，则默认为Integer.MAX_VALUE。
                有界任务队列ArrayBlockingQueue：基于数组的先进先出队列，此队列创建时必须指定大小。
            拒绝策略种类
                AbortPolicy:丢弃任务并抛出RejectedExecutionException
                CallerRunsPolicy：只要线程池未关闭，该策略直接在调用者线程中，运行当前被丢弃的任务。显然这样做不会真的丢弃任务，但是，任务提交线程的性能极有可能会急剧下降。
                DiscardOldestPolicy：丢弃队列中最老的一个请求，也就是即将被执行的一个任务，并尝试再次提交当前任务。
                DiscardPolicy：丢弃任务，不做任何处理。
            提交任务的方式
                Future<T> submit(Callable<T> task)：有返回结果
                void execute(Runnable command)：无返回结果
                Future<?> submit(Runnable task)：返回结果为null
            线程池关闭
                shutdown()：不会立即终止线程池，而是要等所有任务缓存队列中的任务都执行完后才终止，但再也不会接受新的任务。
                shutdownNow()：立即终止线程池，并尝试打断正在执行的任务，并且清空任务缓存队列，返回尚未执行的任务。
        Executors类，常见的4种线程池
            newFixedThreadPoll()：固定大小线程池
                corePoolSize和maximumPoolSize相等
                队列使用的是LinkedBlockingQueue，默认为最大值
            newSingleThreadExecutor()：单一线程线程池
                corePoolSize和maximumPoolSize都是1
                队列使用的是LinkedBlockingQueue
            newCachedThreadPool()：缓存线程池
                corePoolSize是0，maximumPoolSize是最大值
                超时时间默认60秒
                队列使用的是SynchronousQueue
            newScheduledThreadPool()：定时线程池
                该线程池可用于周期性地去执行任务，通常用于周期性的同步数据。
    Java 定时任务
        都可以定时执行、周期执行。
        ScheduledThreadPoolExecutor
            基于线程池。
        Timer
            单一的任务队列。
