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

### 2018-11-01 问题记录(反复重启)
1. 问题现象：通过PVC卷上传的文件一直看不到上传成功的文件
2. 原因分析：
3. 解决方案：
