For  storing data in AWS cloud

Create S3 bucket in specific region

Create S3 user for bucket that user should have S3 bucket full permission.

Create Access key & secret key for that user.

Change value of <Access_key> & <secret_key> in file 30-secret.yaml.

Change bucket name & aws region in file 00-ark-config.yaml.

Change AWSaccount number & username as your aws account no. & username in file 10-deployment-kube2iam.yaml.

For installing in kubernetes follow the steps:- 

1. #kubectl apply -f common/00-prereqs.yaml

2. #kubectl apply -f  aws/

It will create crd & deployment for ark tool.


Install nginx application on cluster using 

#kubectl apply -f nginx-app/base.yaml

For taking backup use

#alias ark='docker run --rm -u $(id -u) -v $(dirname $KUBECONFIG):/kubeconfig -e KUBECONFIG=/kubeconfig/$(basename $KUBECONFIG) gcr.io/heptio-images/ark:latest'

#ark backup create nginx-backup --selector app=nginx

Delete app & try 
#kubectl delete -f nginx-app/base.yaml

For restoring 

#ark restore create nginx-backup --from-backup nginx-backup

For Volume snapshot 
#kubectl apply -f nginx-app/with-pv.yaml

Create backup using 
#ark backup create nginx-backup01 --selector app=nginx --snapshot-volumes

For restoring 

ark restore create nginx-backup01 --from-backup nginx-backup01

That's all.







