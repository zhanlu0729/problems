# problems
### 2018-10-16 问题记录(反复重启)
1. 问题现象：![问题现象](https://github.com/zhanlu0729/problems/blob/master/images/20181016-jvm-args-error.png)
2. 原因分析：怀疑可能是JVM的Heap参数配置过小导致的,辅助截图：![排查截图](https://github.com/zhanlu0729/problems/blob/master/images/20181016-jvm-args-error-analyse.png)
3. 解决方案：给JVM的Heap参数加上单位即可

### 2018-10-31 问题记录1(反复重启)
1. 问题现象：![问题现象](https://github.com/zhanlu0729/problems/blob/master/images/20181031-unable-to-mount-volumns.png)
2. 原因分析：初步怀疑是PVC卷的配置有问题，经查是PV对象的mount路径有问题导致的,辅助截图：![排查截图](https://github.com/zhanlu0729/problems/blob/master/images/20181031-volumns-mount-path-error.png)
3. 解决方案：将PV对象mount的路修改正确

### 2018-10-31 问题记录2(启动失败)
1. 问题现象：发布k8s应用时Pod报node命中失败的错误
2. 原因分析：a.初步判断可能是Node资源紧张导致Node命中失败，经查各Node资源很正常；b.Pod有添加nodeSelector属性，而Node没有打上对应的标签导致的ror.png)
3. 解决方案：给Node打上和Pod中nodeSelector属性对应的标签即可：`kubectl label no/nodeName key=value`

### 2018-12-03 问题记录(日志乱码)
1. 问题现象：在Kibana上查出的日志是乱码![问题现象](https://github.com/zhanlu0729/problems/blob/master/images/20181203-app-log-messy-code.png)
2. 排查思路：a.怀疑是logstash环境的语言、应用容器环境的语言、机器语言设置问题，经排查语言设置正常；b.怀疑是应用本身编码问题问题，经排查应用部分日志输出又是正常的；c.发现乱码日志都是部分dubbo接口产生的，经查dubbo官方资料，dubbo默认对有效载荷的限制8M,而出现乱码日志的这个dubbo接口传输的数据量又非常大
3. 解决方案：调大有效载荷的限制为16M：``<dubbo:protocol name="dubbo" payload="16777216" />``问题得到解决
