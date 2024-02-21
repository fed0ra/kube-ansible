
Ubuntu22.04.3、CentOS7.9已测试适配

# 前提
* 安装包解压到/opt/src路径下
* kube-package离线包过大(671MB)，联系邮箱（990370200@qq.com）wechat(Nclass)无偿获取
* 生成秘钥: 
```
ssh-keygen -t rsa
```
* 复制主机端公钥到所有被控端
```
ssh-copy-id -i /root/.ssh/id_rsa.pub root@192.168.133.131
ssh-copy-id -i /root/.ssh/id_rsa.pub root@192.168.133.132
...
```

# 部署

## 1. 修改hosts文件,根据规划修改对应IP和名称.

## 2. 修改group_vars/all.yml文件,自定义软件包目录和证书可信任IP.

## 3. 部署
## 单master多node部署:
```
./x10d 80
```

## 扩容node节点:
```
./x10d 30
```

## 高可用架构:
```
./x10d 81
```

## 4. 查看集群状态
```
kubectl get cs
kubectl get node -o wide
kubectl get pod --all-namespaces -o wide
sh /opt/etcd/bin/etcd.sh 
```

## 5. nginx服务
运维主机上默认安装了nginx，并创建/data/k8s-yaml目录来存放yaml文件，可以统一管理yaml文件，在任意一台安装kubectl的集群上均可执行kubectl apply应用远程配置资源，IP为hosts中定义的tools
```
kubectl apply -f http://IP/xx.yaml
```
