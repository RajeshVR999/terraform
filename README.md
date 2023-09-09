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


#terraform Outputs 
output "instance_ip_addr" {
    value = aws_instance.server.private_ip
}

output "sample" {
    value ="hello world"
}

output prints a message on the screen.
output blocks helps in printing the created resource attributes & arguments on the screen
outputs with modules work as data transmitter
You can define mutiple output blocks.


terraform registry (all HCL blocks available here)




sudo yum install python3-pip -y
pip3 install awscli --upgrade --user

aws configure # to configure IAM setup 

to get aws access key and security access key , goto IAM and select any user inside that goto securty 


Access key 
Secret access key: 
eu-north-1

export AWS_ACCESS_KEY_ID=your-access-key-id
export AWS_SECRET_ACCESS_KEY=your-secret-access-key
export AWS_DEFAULT_REGION=your-preferred-region

aws iam list-access-keys




terraform type of variable supports 
    1. Strings
    2. Numbers
    3. Booleans

output variable is most importance 

#Default variable type 
variable "sample" {
    default = "hello"
}

#List variable type
variable "sample" {
    default = [
        "hello"
        1000'
        true
        "world"
    ]

    }
}

#Map variable type 
variable "sample" {
    default = {
        string = "hello"
        number = 100,
        boolean = true
    }
}



default vars
input vars 
.tfvars
terraform CLI
shell enviroments variable is least variables 


variable "city" {
    value = "name of the city is $(var.city)"
}

variable "state" {
    value = "name of the state is $(var.state)"
}


terraform apply -auto-approve -var state=karnataka
terraform apply -auto-approve -var-file=sample.tfvars


auto pick the variable is

terraform.tfvars  auto pick 
terraform.auto.tfvars auto pick

dev.tfvars  manual 
prod.tfvars manual 

Variable "sample" {}

High prority to low priority 

-var
-var-file
*.auto.tfvars
low priority shell env vars like "export"
-----------------------------------------------------------------


terraform {
    required_providers {
        prod = {
            source = "hashicorp/aws"
            version = "1.0"
        }
        dev = {
            source = "hashicorp/aws"
            version = "2.0"
              
        }
    }
}

provider "aws" {}
provider "azurerm" {}

--------------------

terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
      version = "5.16.1"
    }
  }
}

provider "aws" {
  # Configuration options
}


terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
      version = "5.12.0"
    }
  }
}


Arguments and Attributes in terraform

Arguments are the build blocks of the resources that you wish to create, which are like the properties to be used to create instance.

EX: ``` AMI to use , Security Group To Use, Network To Use``` 

Attributes are the properties which can only be see once the resource is provisioned.

Ex: ``` Instance ID, Private IP, Public IP```
Depends on the type of changes, terraform change can be either --> Concurrent --> Disruptive --> Destroy and recreate



examples : 

Manually if we change the type t3.micro to t2,micro so manually require to stop instance and do so that only it enables.

in terraform , if change the t3 to t2.micro , it will stop the current instance and it will action it and start the  instance with updated t2.micro


if suppose if changes resoruce  tag names 

it will destroy current resources (instance) and it will re-create the new instance with which are updated t2.micro.


* You created the infra with terraform and updated that manually and you run terraform, what will happen ?
 We will lose all the manual changes and will the changes as per the code.

 * what excatly is happening ?
  when you terraform plan, first your statefile will be validated against the current real-infra and with the terrform code and then will do the necessary changes


  Mutiple people can provising infa at a same time what will be happen ?

Only one person can allow it to provising the infra

if require mutiple persons can deploy to allow means
Terraform locking machism has to do 
or else terraform paid version can allow for multiple persons to run

terraform with aws extends its supports to having a locking mechanism with dynamoDB db integreated with s2 state file


output direct could not send from one module to another module 
output goes to root first than we can fetch output from root module to another module.


--------------
Topics 
output 
variables 
modules 
modules with output 
data resources (exiting resourse)
Provisioners 

Provisioners are used to execute certain tasks after the resources creation,
For example : 
connect to instance and perform some commands , copy somefiles to the instance that got created 

provisioner is a sub-block in resource 

types of provisioners 
local-exec 
remote-exec

if provisioner is fails means terraform output show ec2 instance also shows fails in terraform output.

so choose remote-exec 

connect {
  typer = "ssh"
  user = "centos"
  password = "****"
  host = self.private_ip
}

Provisioner "remote=-exec"  {
  inline = [anisible cmds]
}

*terraform complies the alphbetic order to  load it with logical order to execute 

