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

### 2018-12-04 问题记录(应用反复重启)
1. 问题现象：应用反复重启并报拉取镜像失败的错误
2. 排查思路：a.查看harbor镜像是有的，到应用所在Node手工拉取镜像报错：![](https://github.com/zhanlu0729/problems/blob/master/images/20181204-failed-register-layer-link-too-many.png) b.报这个错误的原因是tag=none的镜像太多，导致inodes资源耗尽
3. 解决方案：比较好的解决办法还是在每个node上跑一个定时任务进行定时清理
```
df -i
sudo find . -xdev -type f | cut -d "/" -f 2 | sort | uniq -c | sort -n
curl -s https://raw.githubusercontent.com/ZZROTDesign/docker-clean/v2.0.4/docker-clean |
sudo tee /usr/local/bin/docker-clean > /dev/null && \
sudo chmod +x /usr/local/bin/docker-clean
docker-clean
```

### 2018-12-05 问题记录(应用发布失败)
1. 问题现象：应用发布失败，拿不到Pod信息
2. 排查思路：a.Pod存在但一直是Pending状态，通过describe查看Pod详细信息：![](https://github.com/zhanlu0729/problems/blob/master/images/20181205-failed-fit-any-node-Insufficient-cpu.png)
3. 解决方案：增加集群资源问题得到解决

### 2018-12-28 问题记录(Dubbo调用失败)
1. 问题现象：Dubbo服务Consumer调用Provider端出现RemotingException异常
2. 排查思路：a.查看日志：![](https://github.com/zhanlu0729/problems/blob/master/images/20181228-dubbo-data-too-large-8m.png)
3. 解决方案：调大有效载荷的限制比实际大：``<dubbo:protocol name="dubbo" payload="16777216" />``问题得到解决

### 2019-01-04 问题记录(隆众机房部分应用日志丢失)
1. 问题现象：隆众机房部分应用日志丢失(mysteel-oilchem-callcenter-timedtask)
2. 排查思路：a.查看日志：![](https://github.com/zhanlu0729/problems/blob/master/images/20190104-es-400-LogLevel-too-lang.png)
3. 解决方案：

### 2019-02-25 问题记录(Dubbo服务报java.io.IOException: invalid constant type: 18)
1. 问题现象：Dubbo服务在启动一直报依赖的Provider的一个bean注册失败，启动异常日志：![](https://github.com/zhanlu0729/problems/blob/master/images/20190225-invalid-constant-type-18.png)
2. 排查思路：a.检查provider的接口是否注册成功：成功；b.查网上资料`javassist3.18.1以下版本在jdk8版本下不工作和asm5以下的版本在jdk8下也不工作`
3. 解决方案：a.更改本地jdk版本为`jdk7`；b.升级项目的`javassist`版本为`>=3.18.1`并且`删除cglib, asm升级到5.0.4`
