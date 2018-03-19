# hadoop
基本配置（通用版）
版本：2.6.4
节点：master 192.168.1.2 
     slave1 192.168.1.3
     slave2 192.168.1.4
总结步骤如下：
1、下载hadoop-2.6.4放于/usr/local下，下载Java1.7放于/usr/lib/jvm下
2、root下创建hadoop用户:useradd hadoop
   给hadoop用户sudo权限:sudo vi /etc/sudoers 加入hadoop (ALL:ALL) ALL
3、修改环境变量:sudo vi /etc/profile
   export JAVA_HOME=/usr/lib/jvm/Java1.7
   export HADOOP_HOME=/usr/local/hadoop-2.6.4
   export CLASSPATH=".:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$CALSSPATH"
   export PATH=$JAVA_HOME/bin:$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$PATH
4、使环境变量生效:source /etc/profile（若未生效重启终端）
5、配置远程免密码登陆
   在hadoop用户目录下创建.ssh文件:cd /home/hadoop      mkdir .ssh
   创建私钥和公钥：ssh-keygen -t rsa -p '' -f /home/hadoop/.ssh/id_rsa
   将公钥生成authorized_keys：cat /home/hadoop/.ssh/id_rsa.pub >> /home/hadoop/.ssh/authorized_keys（权限600）
   将生成的authorized_keys复制到所有节点上
6、进入hadoop-2.6.4的etc文件中的hadoop-env.sh
   修改JAVA的路径：export JAVA_HOME=/usr/lib/jvm/Java1.7
7、修改/etc/hosts:
   127.0.0.1 localhost
   192.168.1.2 master
   192.168.1.3 slave1
   192.168.1.4 slave2
8、修改/etc/hostname:
   视主机而定，master节点写master，slave1节点写slave1，slave2节点写slave2
9、修改hadoop-2.6.4中etc的masters文件和salves文件
   masters文件加入master
   slaves文件加入salve1，slave2
10、配置
   
