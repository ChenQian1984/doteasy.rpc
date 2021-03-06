### DotEasy.RPC

[中文介绍](https://github.com/steveleeCN87/doteasy.rpc/blob/master/README.cn.md)

![Image text](https://raw.githubusercontent.com/steveleeCN87/doteasy.rpc/master/%E5%BE%AE%E6%9C%8D%E5%8A%A1%E6%A1%86%E6%9E%B6.png)

![Image text](https://camo.githubusercontent.com/890acbdcb87868b382af9a4b1fac507b9659d9bf/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f6c6963656e73652d4d49542d626c75652e737667)

# Introduction
With the continuous development of the website system, the complexity of the architecture will change from MVC->SOA->microservices, from simple to complex, from centralized to distributed.
The introduction of the service framework is SOA->microservice process The problem that must be solved.
In the face of the increase in services, the deployment of service distribution, the mutual call between services and services, have to use the service framework to solve.
Based on NET Core 2.0 Standard 2 development, DotEasy.RPC supports transparent calls from the client to the server, just as simple as an implementation call to an interface.


# Features and dependence
1. Automate assembly and construction of related component types using Microsoft.Extensions.Dependency Injection.
2. Serialization of byte streams using [protobuf-net](https://github.com/mgravell/protobuf-net)
3. Generated by [Roslyn](https://github.com/dotnet/roslyn)'s runtime client proxy 
4. Communication pipeline and host built on [DotNetty](https://github.com/Azure/DotNetty)


# More
[http://www.cnblogs.com/SteveLee/](http://www.cnblogs.com/SteveLee/)


# How to use
for the server and add the code in you Web API Core, implement microservice middleware injection.
```
app.UseConsulServerExtensions(Configuration,
    collection =>
    {
        collection.AddSingleton<IProxyService, ProxyImpl>();
    },
    typeof(AuthorizationServerProvider)
);
```
and in the console application, you can use interface proxy the implement client code. 
```
using (var proxy = ClientProxy.Generate<IProxyService>(new Uri("http://127.0.0.1:8500")))
{
    Console.WriteLine($@"{proxy.Sync(1)}");
    Console.WriteLine($@"{proxy.Async(1).Result}");
    Console.WriteLine($@"{proxy.GetDictionaryAsync().Result["key"]}");
}
```


# Change log
## 1.0.3
1. Greatly simplify the writing of client-side calling code, read to 'How to use'.
2. Support the client to access the service node in the form of token.
3. Class instance auto disponse.

## 1.0.2
1. Added precompiled synchronous and asynchronous remote invocation methods, unforcing the use of Task as asynchronous calls and precompiled builds.

## 1.0.1
1. Added Consul registration and callback to implement the configuration of the Consul registry.
2. Added Entry lazy entry class library package to implement Asp.net middleware extension and host based on Console application.