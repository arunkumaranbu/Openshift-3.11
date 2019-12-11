Create 3 VM's with Centos-7.x

In all 3 Nodes,

cat /etc/hosts
172.x.x.185    master.example.com master
172.x.x.186    node1.example.com node1
172.x.x.187    node2.example.com node2

In Master node,
ssh-keygen
ssh-copy-id root@node1
ssh-copy-id root@node2
ssh-copy-id root@master

In all 3 Nodes,
yum update -y

yum install -y wget git net-tools docker-1.13.1 bind-utils iptables-services bridge-utils bash-completion kexec-tools sos psacct openssl-devel httpd-tools NetworkManager python-cryptography python2-pip python-devel  python-passlib java-1.8.0-openjdk-headless

yum -y install epel-release
sed -i -e "s/^enabled=1/enabled=0/" /etc/yum.repos.d/epel.repo
yum -y --enablerepo=epel install pyOpenSSL
yum -y --enablerepo=epel install https://releases.ansible.com/ansible/rpm/release/epel-7-x86_64/ansible-2.6.5-1.el7.ans.noarch.rpm

In Master Node,

git clone https://github.com/arunkumaranbu/Openshift-3.11.git
cd Openshift-3.11

vim inventory file & change the Ipaddress of all Nodes / domain Name

ansible-playbook -i inventory openshift-ansible/playbooks/prerequisites.yml
ansible-playbook -i inventory openshift-ansible/playbooks/deploy_cluster.yml
