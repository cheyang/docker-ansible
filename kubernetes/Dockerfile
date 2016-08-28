FROM williamyeh/ansible:centos7

MAINTAINER cheyang@163.com

RUN yum install -y git && \
    cd / && \
    git clone https://github.com/kubernetes/contrib.git && \
    mv /contrib/ansible /k8s-ansible && \
    rm -rf /contrib

ADD ansible.cfg /k8s-ansible

RUN chmod 644 /k8s-ansible/ansible.cfg

ENV ANSIBLE_HOST_KEY_CHECKING=False

ENV INVENTORY=/etc/ansible/hosts

WORKDIR /k8s-ansible/scripts

CMD [./deploy-cluster.sh]