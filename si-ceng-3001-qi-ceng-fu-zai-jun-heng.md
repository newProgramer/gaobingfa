# 简介

### OSI模型

![](https://upload-images.jianshu.io/upload_images/1156719-afc57efbe98be4f6.png?imageMogr2/auto-orient/strip|imageView2/2/w/557)

二层：基于MAC地址的负载均衡

三层：基于IP地址的负载均衡

四层：基于IP+端口的负载均衡

七层：基于URL等应用层信息的负载均衡

所谓四层到七层负载均衡，就是对后台的服务器进行负载均衡时，依据四层的信息或七层的信息来决定怎样转发流量。

# 区别

四层的负载均衡就是通过发布三层的IP地址，然后加四层的端口号，来决定那些流量需要负载均衡，对需要的流量进行NAT处理，转发至后台服务器，并记录这个TCP或UDP的流量是由哪台服务器处理的，后续这个连接的所有流量都转发到同一台服务器处理。

七层的负载均衡就是在四层的基础上，再考虑应用层的特征（例如：URL、浏览器类别、语言），然后选择对应的服务器进行负载均衡处理。

负载均衡分为L4 switch（四层交换），即在OSI第4层工作，就是TCP层啦。此种Load Balance不理解应用协议（如HTTP/FTP/MySQL等等）。例子：LVS，F5。

另一种叫做L7 switch（七层交换），OSI的最高层，应用层。此时，该Load Balancer能理解应用协议。例子： haproxy，MySQL Proxy。

# Nginx、LVS及HAProxy负载均衡软件的优缺点

负载均衡 （Load Balancing） 建立在现有网络结构之上，它提供了一种廉价有效透明的方法扩展网络设备和服务器的带宽、增加吞吐量、加强网络数据处理能力，同时能够提高网络的灵活性和可用性。

一般对负载均衡的使用是随着网站规模的提升根据不同的阶段来使用不同的技术。具体的应用需求还得具体分析，如果是中小型的Web应用，比如日PV小于1000万，用Nginx就完全可以了；如果机器不少，可以用DNS轮询，LVS所耗费的机器还是比较多的；大型网站或重要的服务，且服务器比较多时，可以考虑用LVS。

目前关于网站架构一般比较合理流行的架构方案：Web前端采用Nginx/HAProxy+ Keepalived作负载均衡器；后端采用 MySQL数据库一主多从和读写分离，采用LVS+Keepalived的架构。当然要根据项目具体需求制定方案。

更多信息请查看：

[https://www.jianshu.com/p/fa937b8e6712](https://www.jianshu.com/p/fa937b8e6712)

