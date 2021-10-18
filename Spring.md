springboot

+ 快速开发脚手架
+ 约定大于配置
+ 基于springboot开发单个微服务

spring cloud

+ 基于springboot实现

学习springboot需要学习spring和springmvc作为前提

弊端：

违背原来的理念，配置十分繁琐，人称“配置地狱”

### IOC：控制反转

1. UserDao接口
2. UserDaoImpl实现类
3. UserService接口
4. UserServiceImpl实现类

降低程序的耦合度，在维护或需求变更时可以更快速迭代。对于代码量大的程序就付出很少的维护成本

将程序创建的对象的控制权从程序员，交给调用者

程序员不需要再去管理对象创建，大大降低耦合度，更加专注业务逻辑和实现

IOC是一种思想，DI是一种具体的IOC实现