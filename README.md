# k8s
k8s deployment with sdulger/k8s base box

Cluster slave count can be provisioned with WORKER_COUNT variable(default to 1)
Slave memory and cpu size can be provisioned in Vagrantfile:

```
  (1..WORKER_COUNT).each do |i|
    config.vm.define "slave#{i}" do |node|
      node.vm.box = "sdulger/k8s"
      
      ...
      
      node.vm.provider "virtualbox" do |vb|
        ###vb.memory = "2048"
        ###vb.cpus = 2
      end
    end
```

run below to setup cluster:
```
vagrant up
```
run below to login master
```
vagrant ssh master
```
run below to login slave#{i}:
```
vagrant ssh slave1
```

fission is installed to master if you are interested to serverless programming.

See setup logs from /root/fission.log
Test hello world fission function:
```
fission function test --name hello
```

Fission pods:
```
kubectl get pod --namespace=fission
```
