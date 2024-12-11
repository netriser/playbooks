# Kubernetes Install Role

Playbook's repository for installing a stack with:
- Elasticsearch cluster
- Kibana
- Metricbeat and Filebeat
- Kubernetes Cluster with masters and workers

## Requirements
- Ansible 2.9 or higher.
- Supported platforms:
  - **Debian-based systems:** Ubuntu, Debian.
- Tested on aws cloud, using terraform provisionning(https://github.com/netriser/k8s_aws_instances), EC2 are tagged refering to there roles
- Be sure you already have AWS CLI, and the inventory aws_ec2.yml

### Step 1: Install aws collection
Install the required Ansible aws collection using:
```bash
ansible-galaxy collection install amazon.aws
```
### Step 2: Install Ansible Roles
Install the required Ansible roles using:
```bash
ansible-galaxy install -r roles/requirements.yml
```

### Step 3: Configure Kubernetes Nodes
Use Ansible to configure the Kubernetes nodes with the following command:
```bash
ansible-playbook -i aws_ec2.yml k8s_install_playbook.yml
```
Same with 
- elastic_install_playbook.yml
- kibana_install_playbook.yml

#### Example Play Recap
```plaintext
PLAY RECAP *********************************************************************************************************************
ec2-52-21-52-238.compute-1.amazonaws.com : ok=37   changed=19   unreachable=0    failed=0    skipped=2    rescued=0    ignored=0
ec2-52-3-159-177.compute-1.amazonaws.com : ok=35   changed=18   unreachable=0    failed=0    skipped=3    rescued=0    ignored=0
ec2-52-70-97-58.compute-1.amazonaws.com : ok=35   changed=18   unreachable=0    failed=0    skipped=3    rescued=0    ignored=0
ec2-54-145-88-170.compute-1.amazonaws.com : ok=35   changed=18   unreachable=0    failed=0    skipped=3    rescued=0    ignored=0

```
### Step 5: Verify Kubernetes Cluster
SSH into the master node and run:
```bash
kubectl get nodes
```

#### Example Output
```plaintext
NAME           STATUS   ROLES           AGE     VERSION
k8s-master-1   Ready    control-plane   11m     v1.30.3
k8s-master-2   Ready    control-plane   8m9s    v1.30.3
k8s-worker-1   Ready    <none>          8m46s   v1.30.3
k8s-worker-2   Ready    <none>          8m46s   v1.30.3
```

## Dependencies
None.

## License
MIT

## Author Information
This role was created by Chakib. Contributions and feedback are welcome!
