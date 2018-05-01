
### AWS

##### install aws cli
```sh
pip3 install awscli
```


##### configure aws
```sh
aws configure
```

##### check aws
```sh
aws iam list-users
```

##### check configures dns
```sh
dig NS k8s.kuznetsov.site
```

##### create bucket
```sh
aws s3 mb s3://cluster1.k8s.kuznetsov.site
```

##### check route53
```sh
aws route53 list-hosted-zones

{
    "HostedZones": [
        {
            "CallerReference": "58E48BF5-676F-A07F-8701-27C0867DA971",
            "ResourceRecordSetCount": 6,
            "Config": {
                "PrivateZone": false
            },
            "Id": "/hostedzone/Z3DV2NYLOXN7ZX",
            "Name": "k8s.kuznetsov.site."
        }
    ]
}

```

### KOPS (Kubernetes OPS)

##### install
```sh
wget https://github.com/kubernetes/kops/releases/download/1.8.0/kops-linux-amd64
chmod +x kops-linux-amd64
mv kops-linux-amd64 /usr/local/bin/
```

##### export KOPS
```sh
export KOPS_STATE_STORE=s3://cluster1.k8s.kuznetsov.site
```

##### cluster creation
```sh
kops create cluster \
--cloud=aws --zones=eu-west-1b \
--dns-zone=k8s.kuznetsov.site \
--name=cluster1.k8s.kuznetsov.site --yes
```

##### cluster validation
```sh
kops validate cluster


Using cluster from kubectl context: cluster1.k8s.kuznetsov.site

Validating cluster cluster1.k8s.kuznetsov.site

INSTANCE GROUPS
NAME			ROLE	MACHINETYPE	MIN	MAX	SUBNETS
master-eu-west-1b	Master	m3.medium	1	1	eu-west-1b
nodes			Node	t2.medium	2	2	eu-west-1b

NODE STATUS
NAME						ROLE	READY
ip-172-20-39-234.eu-west-1.compute.internal	master	True
ip-172-20-40-87.eu-west-1.compute.internal	node	True
ip-172-20-54-147.eu-west-1.compute.internal	node	True

Your cluster cluster1.k8s.kuznetsov.site is ready

```
or using kubectl
```sh
kubectl get nodes

NAME                                          STATUS    ROLES     AGE       VERSION
ip-172-20-39-234.eu-west-1.compute.internal   Ready     master    6m        v1.9.3
ip-172-20-40-87.eu-west-1.compute.internal    Ready     node      4m        v1.9.3
ip-172-20-54-147.eu-west-1.compute.internal   Ready     node      4m        v1.9.3

```

##### get clusters
```sh
kops get cluster

NAME				CLOUD	ZONES
cluster1.k8s.kuznetsov.site	aws	eu-west-1b
```

##### edit this cluster with: 
```sh
kops edit cluster cluster1.k8s.kuznetsov.site
```

##### edit node
```sh
kops edit ig --name=cluster1.k8s.kuznetsov.site nodes
```

##### update cluster
```sh
kops update cluster cluster1.k8s.kuznetsov.site --yes
```

##### delete cluster
```sh
        kops delete cluster \
        --name=cluster1.k8s.kuznetsov.site --yes

...
Deleted cluster: "cluster1.k8s.kuznetsov.site"

```


