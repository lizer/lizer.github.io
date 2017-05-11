---
published: true
---
1. microservice是SOA的一个变种.microservice构架追求轻量和低依赖性(功能和数据的独立性).
2. microservice已经有很多现成的开源框架了.
3. microservice并不能解决你的所有问题.你的项目并不一定适合用microservice结构.
4. mricroservice的优点
	- 功能模块之间相互独立,不同模块可以使用不同技术
    - 功能模块的独立可以让开发组的职责划分更明确
    - 拓展性!!
    - 容错性!!
    - 跟现在的流行cloud和container很搭配   
5. mricroservice的缺点
	- 结构相对复杂,如果产品要求快速上线,开发的时间成本较高
    - 不同功能模块可能是不同技术实现的,这增加了维护的难度
    - 缺乏好的IDE支持.~~虽然用IDE有点初级,但是有些时候用IDE还挺方便.~~
    - 测试和部署环境可能会难以管理,again,不同功能模块可能是不同技术.
6. 由于数据的隔离,做一些查询的时候可能有有点麻烦.CRQS好像是目前的最好的解决方案.但是我的感觉这让软件变的不清爽了.不像一个proper solution,更像是一个workaround.
7. 功能模块(service)的切分看构架师经验也看运气.就像寿司师傅片鱼片.
