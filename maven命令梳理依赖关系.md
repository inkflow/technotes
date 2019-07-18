
列出依赖清单
```
mvn dependency:list
```
给出依赖树
```
mvn dependency:tree
```
分析依赖关系
```
mvn dependency:analyze
```
该命令执行结果的两个重要部分：

Used undeclared dependencies: 表示项目中使用到的，但是没有显示声明的依赖

Unused declared dependencies: 表示项目中未使用的，但显示声明的依赖

PS：dependency : analyze只会分析编译主代码和测试代码需要用到的依赖，一些执行测试和运行时需要的依赖它无法发现。
