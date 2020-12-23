# Java Object类

- clone()：默认为浅克隆。
    默认为浅克隆。
    没有实现Clonable接口的类，调用clone()方法会抛出异常。
    实现深克隆的方式
        第一种方式：内部未使用引用类型，或引用类型都实现了Cloneable接口。
        第二种方式：实现Serializable接口，通过序列化深克隆。
- toString()：常用。
- wait()
    必须在同步代码中调用，即必须持有锁。
    会释放锁。
- notify()
    必须在同步代码中调用，即必须持有锁。
    随机唤醒一个线程。
- notifyAll()
    必须在同步代码中调用，即必须持有锁。
    唤醒所有线程。
- equals()：比较值，值相同则hashcode应该相同。
    == 和 equals()
        ==：对于基本类型，比较值。对于引用类型，比较引用的内存地址。
        equals()：默认使用了==，实际上，我们重写该方法用来比较对象值是否相同。
- hashcode()：hashcode相等，equals不一定为true。
- finalize()：对象被GC前，调用该方法。
- getClass()：获取该对象的类型的对象。（每个类型都有一个与之对应的Class对象。）