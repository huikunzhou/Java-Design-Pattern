### 单例模式 (Singleton)

> 确保某一个类只有一个实例，而且自行实例化并向上整个系统提供这个实例。

**优点**：*只生产一个实例对象，减少内存开支，提升性能；避免对资源的多*				      *重占用；可设置一个全局访问点，优化和共享访问资源。*

**缺点**：*没有接口，难以扩展(是否可以增加接口)；不便于测试；与单一职责原则有冲突。*

**示例**：*创建一个类，私有其构造函数，实例化一个`private`的`static`的类变量，创建一个`public`的`getInstance`的方法用来获取对类变量的引用 。*

- 饿汉式单例（只产生一个实例，不需考虑线程同步）

```java
public class Singleton {
	private static final Singleton singleton = new 			
        	Singleton();
    //限制产生多个对象
    private Singleton(){
	}
    //通过该方法获得实例对象
    public static Singleton getSingleton(){
    	return singleton;
    }
    //类中其他方法，尽量是static
	public static void doSomething(){
 	}
}
```

- 懒汉式单例（需考虑线程同步）

```java
public class Singleton {
	private static final Singleton singleton = null;
    //限制产生多个对象
    private Singleton(){
	}
    //通过该方法获得实例对象（每次调用都需要同步）
    public static synchronized Singleton getSingleton(){
        if(singleton == null){
            singleton =  new Singleton();
        }
        return singleton;
    }
    // 双重检查锁形式
    public static Singleton getInstance(){
        if(singleton == null){
            synchronized(Singleton.class){
                if(singleton == null){
              		singleton = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

