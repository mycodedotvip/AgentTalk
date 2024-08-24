代理模式（Proxy Pattern）是一种结构型设计模式，它为其他对象提供一种代理，以控制对这个对象的访问。代理模式在不改变客户端代码的前提下，通过代理对象来控制访问被代理的对象，可以增加额外的功能或者控制，如访问控制、延迟初始化、日志记录等。

### 代理模式的类型

1. **静态代理**：
   在编译期间由程序员创建代理类，代理类和目标类实现同一个接口。代理类中的方法会调用目标对象的对应方法。

2. **动态代理**：
   在运行时动态生成代理类，通常使用 Java 的 `java.lang.reflect.Proxy` 或 CGLIB 来实现动态代理。

### 代理模式的结构

1. **抽象主题（Subject）**：
   定义了真实对象和代理对象的共同接口，客户端可以通过这个接口与真实对象进行交互。

   ```java
   public interface Subject {
       void request();
   }
   ```

2. **真实主题（RealSubject）**：
   实现了抽象主题接口，是代理对象所代表的真实对象。

   ```java
   public class RealSubject implements Subject {
       @Override
       public void request() {
           System.out.println("RealSubject: Handling request.");
       }
   }
   ```

3. **代理对象（Proxy）**：
   代理对象内部持有一个对真实主题对象的引用，代理对象与真实主题实现相同的接口，从而可以代替真实对象进行操作。代理对象可以在调用真实对象之前或之后添加一些额外的操作。

   ```java
   public class Proxy implements Subject {
       private RealSubject realSubject;

       @Override
       public void request() {
           if (realSubject == null) {
               realSubject = new RealSubject();
           }
           System.out.println("Proxy: Additional operations before delegating the request.");
           realSubject.request();
           System.out.println("Proxy: Additional operations after delegating the request.");
       }
   }
   ```

4. **客户端（Client）**：
   通过代理对象来操作真实对象。

   ```java
   public class Client {
       public static void main(String[] args) {
           Subject proxy = new Proxy();
           proxy.request();
       }
   }
   ```

### 代理模式的应用场景

- **虚拟代理**：延迟加载，将创建开销较大的对象的实例化推迟到真正需要时才进行。
- **远程代理**：为在不同地址空间的对象提供代理，通过网络代理远程对象的操作。
- **保护代理**：控制对目标对象的访问权限，常用于权限控制。
- **缓存代理**：为一些耗时的操作提供缓存机制，避免重复操作。
- **日志记录代理**：在调用目标对象的操作时记录日志。
- **防火墙代理**：控制内部网络与外部网络之间的访问。

### 优点和缺点

**优点**：
- 代理模式可以在不修改客户端代码的前提下，增加对目标对象的功能扩展。
- 控制对目标对象的访问权限。
- 延迟实例化目标对象，节省资源。

**缺点**：
- 增加了系统的复杂性，因为需要引入额外的代理对象。
- 可能会引入性能开销，特别是在使用动态代理时。

### 动态代理示例（Java）

使用 Java 的动态代理可以更灵活地实现代理模式。以下是一个简单的动态代理示例：

```java
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

// 代理处理器
public class DynamicProxyHandler implements InvocationHandler {
    private Object target;

    public DynamicProxyHandler(Object target) {
        this.target = target;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("Before method: " + method.getName());
        Object result = method.invoke(target, args);
        System.out.println("After method: " + method.getName());
        return result;
    }
}

// 使用动态代理
public class Client {
    public static void main(String[] args) {
        RealSubject realSubject = new RealSubject();
        Subject proxyInstance = (Subject) Proxy.newProxyInstance(
                realSubject.getClass().getClassLoader(),
                realSubject.getClass().getInterfaces(),
                new DynamicProxyHandler(realSubject)
        );

        proxyInstance.request();
    }
}
```

在这个例子中，`DynamicProxyHandler` 是一个动态代理处理器，它在调用 `RealSubject` 的方法之前和之后添加了一些操作。客户端通过代理实例 `proxyInstance` 来调用方法，代理会将调用委派给 `RealSubject`，同时还能添加额外的逻辑。
