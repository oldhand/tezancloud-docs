# tezancloud
<h1 align="center">
  <br>
  <a href="https://github.com/oldhand/tezancloud"><img src="https://github.com/oldhand/images/raw/master/logo/tezan.jpg" width="200"></a>
  <br>
  tezancloud(特赞平台)
  <br>
</h1>

<h4 align="center">
  一套基于erlang语言开发的，大型分布式云平台，同时，也是一个简单，稳定，高效，跨平台的开发框架。<br>
  致力于零后台开发人员，零成本地帮您解决后台开发问题。
  <br><br>
  Based in erlang.
  Support By <a href="https://github.com/oldhand" target="_blank">oldhand</a>.
</h4>
<p align="center">    
    <b>如果对您有帮助，您可以点右上角 "Star" 支持一下 谢谢！</b>
</p>

## 欢迎


### 介绍
**tezancloud，是基于 [erlang](https://erlang.org) 开发的、面向后端的一整套框架解决方案。**

平台主要集成了任务调度，报表引擎、数据库、标签缓存、REST、消息队列，图片CDN等模块。

> 简单来说，在tezancloud提供的强大支持下，您的项目不需要配专职的后台开发人员，数据库的建表，增删改查，高效缓存，消息队列，接口等，都已经标准化，同时支持大部分开发语言的接口，部分需求只需要使用脚本语言lua进行简单配置。

<br>

### 选择了 tezancloud 可以得到什么？
- **大型分布式架构**<br>
  平台支持负载均衡，多节点冗余布署方案。
  
- **最小开发成本**<br>
  项目开发最大的成本，就是后台开发人员的人员成本。:smile::smile::smile:
  
- **高效的开发速度**<br>
  拿来即用的后台，免除了项目的开发与试错时间。
  
- **NoSQL**<br>
  平台所有的数据都存储在关系型数据库(PostreSQL)中, 但平台使用都是以NoSQL的方式进行的。<br>
  开发过程中，不需要写一条SQL语句，也无需进行字段管理，每一条记录的字端数，都是灵活多变的，字段还可以以数组的方式进行存储。<br>
  PostreSQL关系型数据库，可以很好的利用成熟稳定的备份还原，容错，集群等机制。<br>
  数据增长较庞大后，进行特定组合索引，分表分库，可以大大提高数据检索速度。

- **数据库分表分库**<br>
  平台数据支持按年，按月，按天存储，保障系统运营过程中，不会有数据膨胀的问题。

- **SaaS模式**<br>
  平台天然支持SaaS模式,也支持不同业务场景同时运行。
  
- **无需程序员干预的缓存机制**<br>
  缓存是平台健康高效有效保障，建立缓存相对容易，什么时候清除，关联的缓存是否清理干净，往往是程序员最为棘手的工作。平台引入缓存标签机制，程序员无需增加一行代码，就可以有效保障缓存机制正常运转。<br>
  缓存标签机制，大大降低了数据库的负载压力。

- **消息队列服务**<br>
  消息队列的重要性，在订单系统，交易系统，库存管理等场景中，必须使用队列的方法，才能保障数据的正确性。<br>
  平台同时支持并发性队列与单一队列。

- **lua配置服务端脚本**<br>
  lua 是一个小巧的，执行速度最快的，同时也是学习成本最低的脚本语言。<br>
  所有消息队列的响应端，全部为服务端lua脚本。

- **REST服务**<br>
  [基于IBM标准的REST服务](https://www.ibm.com/developerworks/cn/webservices/ws-restful/)，具体实现方法，请参阅文档。<br>
  java的微服务，需要后台开发人员设计并实现所有的接口，占用了大量的人力与工期。<br>
  相比我们的REST服务，所有的接口与服务，都已经标准化，即使业务需要新增功能，也无需增加接口。<br>
  >架构设计,我们已经走在了最前面,将来的趋势,也肯定是标准化,省时省力的架构才能得到市场的认可。

- **接口安全保障**<br>
  接口使用token认证，以及RSA公钥与私钥的方式进行加密处理。
  >同时提供各种主流开发语言的接口。
  
- **图片转换CDN服务**<br>
  平台提供图片转换与缓存服务。
  
  >在图片链接后增加参数，即可获得指定尺寸与格式的图片文件。
  
- **高效的运行速度，充分利用服务器的多核资源**<br>
  得益于 `erlang`的多核，高并发特性，绝对不会出现一个CPU核心在努力工作，其他的CPU核心都在边上看着的情况。
  >实测，当tezancloud服务于WEB端时，所有的页面都可以做到500ms内返回数据，让用户体验达到了极致！
  
- **稳定**<br>
  得益于 `erlang`的监控树机制，更是让我们的服务，天生就具备了高可靠的基因。<br>
  得益于 `erlang`的设计机制，具备“9个9的可靠性”。<br>
  
  > “9个9的可靠性”意识是什么了?意思就是说在一百万秒钟，只有一秒出现故障时间，或者说在一百万分钟，只出现一分钟的故障时间。然而，一百万秒大约就是30年。一百万分钟大约是2000年。

- **获得开源的成熟项目**<br>
  可以获得大量开源代码。<br>
  见开源项目列表。<br>

 

- - -

## 使用须知
1.未经授权的所有代码与资源，仅允许用于个人学习、毕业设计、教学案例、公益事业;<br>
2.如果已经经过授权，所有的代码与资源可以随意修改并出售;<br>
3.禁止将本项目的所有资源，在未经授权的情况下，进行任何形式的出售，产生的一切任何后果责任由侵权者自负。<br>

## 版权信息
<p align="center">    
版权所有Copyright © 2017-2019 by <a href="www.tezan.cn" target="_blank">tezan</a><br>
All rights reserved。<br>
湖南赛明威科技有限公司<br>
</p>