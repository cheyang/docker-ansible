FROM williamyeh/ansible:centos7

MAINTAINER cheyang@163.com

RUN yum install -y git python-netaddr && \
    cd / && \
    git clone https://github.com/kubernetes/contrib.git && \
    mv /contrib/ansible /k8s-ansible && \
    rm -rf /contrib

ADD ansible.cfg /k8s-ansible/scripts

# Add Options
ADD ansible/roles/node/templates/kubelet.j2 /k8s-ansible/roles/node/templates/kubelet.j2
# Create local copies of easy-rsa
ADD ansible/roles/kubernetes/files/make-ca-cert.sh /k8s-ansible/roles/kubernetes/files/make-ca-cert.sh
COPY ansible/roles/kubernetes/files/easy-rsa.tar.gz /k8s-ansible/roles/kubernetes/files/easy-rsa.tar.gz
ADD ansible/roles/kubernetes/tasks/gen_certs.yml /k8s-ansible/roles/kubernetes/tasks/gen_certs.yml
# replace gcr.io with local docker registry
ADD ansible/roles/kubernetes-addons/tasks/main.yml /k8s-ansible/roles/kubernetes-addons/tasks/main.yml

RUN chmod 644 /k8s-ansible/scripts/ansible.cfg

#ENV ANSIBLE_HOST_KEY_CHECKING=False

ENV INVENTORY=/etc/ansible/hosts

WORKDIR /k8s-ansible/scripts

CMD [./deploy-cluster.sh]