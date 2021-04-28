##eureka集群部署

#####eureka版本 
     <groupId>org.springframework.cloud</groupId> 
     <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>   
     <version>2.2.1.RELEASE</version>  
 
#### 机器1： ip: 81.140.12.51 yml配置文件
    server:
      port: 7001
    
    eureka:
      instance:
        #hostname: localhost  #eureka服务端实例名称
        hostname: 81.140.12.51 #eureka服务端的实例名称
    #    instance-id: eureka1
    #    prefer-ip-address: true  #访问路径可以显示IP地址
      client:
        register-with-eureka: true  #false表示不向注册中心注册自己
        fetch-registry: true   #false表示自己就是注册中心，我的职责就是维护服务实例，并不需要去检索服务
        service-url:
          defaultZone: http://107.14.137.231:7001/eureka/,http://122.4.81.175:7001/eureka/
          #defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/   #设置与Eureka Server交互的地址查询服务和注册服务都需要依赖这个地址（单机）
    #    server:
    #      #关闭自我保护机制，保证不可用服务被及时剔除
    #      enable-self-preservation: false
    #      eviction-interval-timer-in-ms: 2000
 
#### 机器2： ip: 122.4.81.175 yml配置文件
    server:
      port: 7001
    
    eureka:
      instance:
        #hostname: localhost  #eureka服务端实例名称
        hostname: 122.4.81.175 #eureka服务端的实例名称
    #    instance-id: eureka2
    #    prefer-ip-address: true  #访问路径可以显示IP地址
      client:
        register-with-eureka: true  #false表示不向注册中心注册自己
        fetch-registry: true   #false表示自己就是注册中心，我的职责就是维护服务实例，并不需要去检索服务
        service-url:
          defaultZone: http://81.140.12.51:7001/eureka/,http://107.14.137.231:7001/eureka/
          #defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/   #设置与Eureka Server交互的地址查询服务和注册服务都需要依赖这个地址（单机）
    #    server:
    #      #关闭自我保护机制，保证不可用服务被及时剔除
    #      enable-self-preservation: false
    #      eviction-interval-timer-in-ms: 2000
#### 机器3： ip: 107.14.137.231 yml配置文件
    server:
      port: 7001
    
    eureka:
      instance:
        #hostname: localhost  #eureka服务端实例名称
        hostname: 107.14.137.231 #eureka服务端的实例名称
    #    instance-id: eureka3
    #    prefer-ip-address: true  #访问路径可以显示IP地址
      client:
        register-with-eureka: true  #false表示不向注册中心注册自己
        fetch-registry: true   #false表示自己就是注册中心，我的职责就是维护服务实例，并不需要去检索服务
        service-url:
          defaultZone: http://122.4.81.175:7001/eureka/,http://81.140.12.51:7001/eureka/
          #defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/   #设置与Eureka Server交互的地址查询服务和注册服务都需要依赖这个地址（单机）
    #    server:
    #      #关闭自我保护机制，保证不可用服务被及时剔除
    #      enable-self-preservation: false
    #      eviction-interval-timer-in-ms: 2000

 

 
#### 检查集群是否启动成功 
##### 注意：Centeral Info 下 unavailable-replicas 不能有值：否则集群启动失败！！
 
    访问：81.140.12.51:7001
    访问: 122.4.81.175:7001
    访问: 107.14.137.231:7001

#####DS Replicas
    122.4.81.175
    81.140.12.51
   
#####Instances currently registered with Eureka

    Application	AMIs	Availability Zones	Status
    UNKNOWN	n/a (3)	(3)	UP (3) - 81.140.12.51:7001 , 122.4.81.175:7001 , 107.14.137.231:7001

#####General Info

    Name	Value
    total-avail-memory	56mb
    environment	test
    num-of-cpus	1
    current-memory-usage	30mb (53%)
    server-uptime	02:18
    registered-replicas	http://122.4.81.175:7001/eureka/, http://81.140.12.51:7001/eureka/
    unavailable-replicas	
    available-replicas	http://122.4.81.175:7001/eureka/,http://81.140.12.51:7001/eureka/,





