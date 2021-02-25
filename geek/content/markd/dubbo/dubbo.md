## dubbo

## 1. 服务消费方发起请求   
 当服务的消费方引用了某远程服务，服务的应用方在spring的配置实例如下：
```
<dubbo:referenceid="demoService"interface="com.alibaba.dubbo.demo.DemoService" />
```
 demoService实例其实是代理工厂生产的代理对象（大家可以参考代理那部分生成的伪代码），在代码中调用demoService.sayHello(“world!”)时，

> 1.1 将方法名方法参数传入InvokerInvocationHandler的invoke方
>> 对于Object中的方法toString, hashCode, equals直接调用invoker的对应方法,
这里对于Object的方法需要被远程调用吗？调用了是不是报错比默认处理更好呢？？
远程调用层是以Invocation, Result为中心， 这里根据要调用的方法以及传入的参数构建RpcInvocation对象，作为Invoker的入参  
 
> 1.2 MockClusterInvoker根据参数提供了三种调用策略   
















