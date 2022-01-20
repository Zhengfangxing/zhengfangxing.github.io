## SpringCloud

#### 1.什么是SpringCloud?

Spring Cloud为开发人员提供了工具，以快速构建分布式系统中的一些常见模式（例如，配置管理，服务发现，断路器，智能路由，微代理，控制总线，一次性令牌，全局锁，领导选举，分布式会话，群集状态）。它们可以在任何分布式环境中正常工作，包括开发人员自己的笔记本电脑，裸机数据中心以及Cloud Foundry等托管平台。

#### 2.什么是微服务？

所谓的微服务是SOA架构下的最终产物，该架构的设计目标是为了肢解业务，使得服务能够独立运行。微服务设计原则：

1、各司其职 。

2、服务高可用和可扩展性。

#### 3.SpringCloud有哪些特征?

Spring Cloud专注于为典型的用例和可扩展性机制（包括其他用例）提供良好的开箱即用体验。

- 分布式/版本化配置
- 服务注册和发现
- 路由
- 服务到服务的调用
- 负载均衡
- 断路器
- 全局锁
- 领导选举和集群状态
- 分布式消息传递

#### 4.SpringCloud核心组件?

Eureka : 注册中心

Ribbon ：客服端负载均衡

Hystrix :  服务容错处理

Feign: 声明式REST客户端

Zuul : 服务网关

Config : 分布式配置

#### 5.SpringCloud基于什么协议？

HTTP

#### 6.SpringCloud和Dubbo区别?

![image-20200429230443620](https://gitee.com/yizhibuerdai/Imagetools/raw/master/images/image-20200429230443620.png)

#### 7.Eureka是什么？

云端服务发现，一个基于 REST 的服务，用于定位服务，以实现云端中间层服务发现和故障转移。

#### 8.服务治理的基础角色？

服务注册中心：提供服务注册与发现的能力。

服务提供者：提供服务的应用，会把自己提供的服务注册到注册中心。

服务消费者：服务的消费者，从注册中心获取服务列表。

#### 9.什么是服务续约？

在注册完服务以后，服务提供者会维护一个心跳来向注册中心证明自己还活着，以此防止被“剔除服务”。

#### 10.什么是服务下线？

当服务实例进行正常关闭时，会发送一个REST请求（我要下线了）给注册中心，收到请求后，将该服务状态设置下线（DOWN），并把这事件传播出去。

#### 11.什么是失效剔除？

当服务非正常下线时，可能服务注册中心没有收到下线请求，注册中心会创建一个定时任务（默认60s)将没有在固定时间(默认90s)内续约的服务剔除掉。

#### 12.什么是自我保护机制？

在运行期间，注册中心会统计心跳失败比例在15分钟之内是否低于85%,如果低于的情况，注册中心会将当前注册实例信息保护起来，不再删除这些实例信息，当网络恢复后，退出自我保护机制。

自我保护机制让服务集群更稳定、健壮。

#### 13.Ribbon是什么?

提供云端负载均衡，有多种负载均衡策略可供选择，可配合服务发现和断路器使用。

#### 14.Ribbon负载均衡的注解是?

@LoadBalanced

#### 15.Ribbon负载均衡策略有哪些？

RandomRule :  随机。

RoundRobinRule : 轮询。

RetryRule : 重试。

WeightedResponseTimeRule : 权重。

ClientConfigEnabledRoundRobinRule : 一般不用，通过继承该策略，默认的choose就实现了线性轮询机制。可以基于它来做扩展。

BestAvailableRule : 通过便利负载均衡器中维护的所有服务实例，会过滤到故障的，并选择并发请求最小的一个。

PredicateBasedRule : 先过滤清单，再轮询。

AvailabilityFilteringRule ：继承了父类的先过滤清单，再轮询。调整了算法。

ZoneAvoidanceRule : 该类也是PredicateBasedRule的子类，它可以组合过滤条件。以ZoneAvoidancePredicate为主过滤条件，以AvailabilityPredicate为次过滤条件。

#### 16.什么是服务熔断？

服务熔断的作用类似于我们家用的保险丝，当某服务出现不可用或响应超时的情况时，为了防止整个系统出现雪崩，暂时停止对该服务的调用。

#### 17.什么是服务降级？

服务降级是当服务器压力剧增的情况下，根据当前业务情况及流量对一些服务和页面有策略的降级，以此释放服务器资源以保证核心任务的正常运行。

#### 18.什么是Hystrix?

熔断器，容错管理工具，旨在通过熔断机制控制服务和第三方库的节点,从而对延迟和故障提供更强大的容错能力。

#### 19.断路器Hystrix的有哪些功能？

- 通过第三方客户端访问依赖服务出现高延迟或者失败时,为系统提供保护和控制 。
- 在复杂的分布式系统中防止级联失败(服务雪崩效应) 。
- 快速失败 (Failfast) 同时能快速恢复。
- 提供失败回滚 (Fallback) 和优雅的服务降级机制。
- 提供近实时的监控、 报警和运维控制手段。

#### 20.Hystrix将远程调用封装到？

HystrixCommand 或者 HystrixObservableCommand对象中。

#### 21.启动熔断降级服务的注解？

@EnableHystrix

#### 22.什么是Feign?

Feign是一种声明式、模板化的HTTP客户端。

#### 23.Feign优点？

1.feign采用的是基于接口的注解。 2.feign整合了ribbon，具有负载均衡的能力。 3.整合了Hystrix，具有熔断的能力。

#### 24.什么是Config?

配置管理工具包，让你可以把配置放到远程服务器，集中化管理集群配置，目前支持本地存储、Git以及Subversion。

#### 25.Config组件中的两个角色?

Config Server : 配置中心服务端。

Config Client : 配置中心客户端。

#### 26.什么是Zuul?

Zuul 是在云平台上提供动态路由,监控,弹性,安全等边缘服务的框架。Zuul 相当于是设备和 Netflix 流应用的 Web 网站后端所有请求的前门。

#### 27.使用Zuul的优点?

- 方便监控。可以在微服务网管手机监控数据并将其推送到外部系统进行分析。
- 方便认证。可在网关进行统一认证，然后在讲请求转发到后端服务。
- 隐藏架构实现细节，提供统一的入口给客户端请求，减少了客户端和每个微服务的交互次数。
- 可以统一处理切面任务，避免每个微服务自己开发，提升效率。
- 高可用高伸缩性的服务，避免单点失效。

#### 28.Zuul的核心是？

过滤器。

#### 29.Zuul有几种过滤器类型？分别是？

4种。

pre : 可以在请求被路由之前调用。

适用于身份认证的场景，认证通过后再继续执行下面的流程。

route : 在路由请求时被调用。

适用于灰度发布场景，在将要路由的时候可以做一些自定义的逻辑。

post :在 route 和 error 过滤器之后被调用。

这种过滤器将请求路由到达具体的服务之后执行。适用于需要添加响应头，记录响应日志等应用场景。

error : 处理请求时发生错误时被调用。

在执行过程中发送错误时会进入 error 过滤器，可以用来统一记录错误信息。

#### 30.什么是Sleuth?

日志收集工具包，封装了Dapper和log-based追踪以及Zipkin和HTrace操作，为SpringCloud应用实现了一种分布式追踪解决方案。

#### 31.Sleuth帮助我们做了哪些工作？

- 可以方便的了解到每个采样的请求耗时，分析出哪些服务调用比较耗时。
- 对于程序未捕捉的异常，可以在集成Zipkin服务页面上看到。
- 识别调用比较频繁的服务，从而进行优化。

#### 32.什么是Bus?

事件、消息总线，用于在集群（例如，配置变化事件）中传播状态变化，可与Spring Cloud Config联合实现热部署。

#### 33.eureka比zookeeper的优势在？

A:高可用 C:一致性，P:分区容错性

Zookeeper保证了CP，Eureka保证了AP。

Eureka可以很好的应对因网络故障导致部分节点失去联系的情况，而不会像Zookeeper那样使整个微服务瘫痪。

#### 34.什么是Stream?

数据流操作开发包，封装了与Redis,Rabbit、Kafka等发送接收消息。

#### 35.更多知识？

SpringCloud这个体系东西还是挺大的，小编会不断的丰富内容以及优化。欢迎大家关注我的公众号获得最新动态《Java小咖秀》。

参考：

- 《Spring Cloud微服务实战》

- 《Spring Cloud微服务全栈技术与案例解析》

- 《Spring Cloud微服务架构开发实战》

- ​	https://spring.io/projects/spring-cloud

- ​	https://www.springcloud.cc/

- ​    百度百科

  