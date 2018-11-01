# problems
### 2018-10-16问题记录
1. 问题现象：![问题现象](https://github.com/zhanlu0729/problems/blob/master/images/20181016-jvm-args-error.png "问题现象")
2. 原因分析：怀疑可能是JVM的Heap参数配置过小导致的
3. 排查截图：![排查截图](https://github.com/zhanlu0729/problems/blob/master/images/20181016-jvm-args-error-analyse.png "排查截图")
4. 解决方案：给JVM的Heap参数加上单位即可

### 2018-10-31问题记录
1.问题现象：![问题现象](https://github.com/zhanlu0729/problems/blob/master/images/20181031-unable-to-mount-volumns.png)
2. 原因分析：初步怀疑是PVC卷的配置有问题，经查是PV对象的mount路径有问题导致的,辅助截图：
