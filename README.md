# Kubernetes-Setup

###Remove kubernetes created directory
```rm -r ~/.kube```

### Set vars associated with eks cluster
```export region_code="<aws_region>"```

```export cluster-name="<aws_eks_cluster_name>"```

```export account_id="<aws_account_id>"```

```cluster_endpoint=$(aws eks describe-cluster --region $region_code --name $cluster_name --query "cluster.endpoint" --output text)```

```certificate_data=$(aws eks describe-cluster --region $region_code --name $cluster_name --query "cluster.certificateAuthority.data" --output text)```


### Place cluster cert into eks.crt
```aws eks describe-cluster --name test-cluster --query "cluster.certificateAuthority.data" --output text| base64 --decode > eks.crt```

### Read eks.crt
```openssl x509 -in eks.crt -text -noout```

### Manually create .kube directory
```mkdir -p ~/.kube```

### Make sure create-kubenetes file is executeable
```chmod +x create-kubernetes.sh```

### Run script to create ~/.kube/config file
```./create-kubernetes.sh```


--------------------------------------------------
# General Kubernetes commands
### Get eksctl version
```eksctl version```

### Delete nodegroup
```eksctl delete nodegroup   --cluster <cluster_name>   --region <aws_region>   --name <name_of_nodegroup>```

### List the node groups associated with cluster name
```aws eks list-nodegroups --cluster-name <cluster_name>```