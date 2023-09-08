# terraform Notes 

WHy Terraform ?
Lower Operation cost 
versioned infra

Terraform works on a languague called 

Json 
HCL  preffered 
K8s
Python 

Two versions 
Latest : 1:3:2

Many cloud providers by terraformodule 

All the files of terraform end with .tf or .tf.json as an extension 

We can keep multiple files, Terrform loads them in an alphabetical order but compiles as per the its logic as per the dependencies

if you want to control that simply use depends_ondata



#How HCL will have the code 
*code is in blocks, THe example you see here in a resource block.
* A resource belongs to a providers
* Terraform has alot of provider AWS is one of them

* Everthing is a block in terraform HCL.
* EX: resources, Variables, outputs, data, provider, locals

Terrraform init
terraform plan
terraform apply
terraform destroy 


HCL code is converted into pstyon lang so that many provider can the code.

ssh -i /path/to/your-key.pem ec2-user@51.20.31.33

#EPEL packages for centos 8 below commands 
# sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
# sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*

sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/RHEL/hashicorp.repo
sudo yum -y install terraform


# terraform --version
Terraform v1.5.7
on linux_arm64
[root@ip-172-31-11-223 ~]#

sudo yum install git

git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"


RajeshVR999
git config --global user.name "RajeshVR999"
git config --global user.email "rajeshpadma99@gmail.com"

ssh-keygen -t rsa -b 4096 -C "rajeshpadma99@gmail.com"

eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
