* 基础知识
	* 为什么jdk动态代理要基于接口实现
		* 测试代码
```  java
public interface UserTpl {
    String getUserName();
}
public class User implements UserTpl{

    @Override
    public String getUserName(){
        print();
        return "tt";
    }

    public void print()
    {
        System.out.println(111);
    }
    
}
public class UserHandel implements InvocationHandler {
    private Object target;
    public UserHandel(Object target)
    {
        this.target = target;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("invocation handler");
        return method.invoke(target,args);
    }
}

public class Test {

    public static void main(String[] args)
    {
        System.getProperties().put("sun.misc.ProxyGenerator.saveGeneratedFiles", "true");
        UserTpl user = (UserTpl) Proxy.newProxyInstance(UserTpl.class.getClassLoader(),User.class.getInterfaces(),new UserHandel(new User()));
        System.out.println(user.getUserName());
    }
}

代理对象对比的.class文件内容
public final class $Proxy0 extends Proxy implements UserTpl {
    private static Method m1;
    private static Method m4;
    private static Method m2;
    private static Method m3;
    private static Method m0;

    public $Proxy0(InvocationHandler var1) throws  {
        super(var1);
    }
    public final void print() throws  {
        try {
            super.h.invoke(this, m4, (Object[])null);
        } catch (RuntimeException | Error var2) {
            throw var2;
        } catch (Throwable var3) {
            throw new UndeclaredThrowableException(var3);
        }
    }
    public final String getUserName() throws  {
        try {
            return (String)super.h.invoke(this, m3, (Object[])null);
        } catch (RuntimeException | Error var2) {
            throw var2;
        } catch (Throwable var3) {
            throw new UndeclaredThrowableException(var3);
        }
    }
    ....
}
``` 
* 输出内容 
	* invocation handler  111 tt 
*  通过源码发现 Proxy0 继承Proxy，实现了 UserTpl ，所以要基于接口实现。同时还有一点，如果在方法a中调用方法b，动态代理不会方法b进行增强

