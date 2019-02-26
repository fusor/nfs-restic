# nfs-restic

## Purpose
To simplify the set up for testing restic with NFS

## Use
* Get a cluster using origin3-dev (probably a better idea to do this on an EC2 VM)
* SSH into the VM
* `yum install -y ansible git python-openshift`
* `setenforce 0`
* `git clone https://github.com/fusor/ocp-velero-ansible`
* `cd ocp-velero-ansible`
* `mkdir auth`
* `cp /tmp/openshift.local.clusterup/openshift-apiserver/admin.kubeconfig auth/kubeconfig`
* Comment out `- login_ocp` in launch-ark.yml
* `ansible-playbook launch-ark.yml`
* `oc edit ds -n heptio-ark restic` and change the hostPath mount from `/var/lib/kubelet/pods/` to `/tmp/openshift.local.clusterup/openshift.local.volumes/pods/`
* `cd ..`
* `git clone https://github.com/fusor/nfs-restic`
* `cd nfs-restic`
* `ansible-playbook setup.yml` to set up nfs, delete hostPath pv's, and create some NFS pv's
* `oc new-project nfs-test`
* `oc create -f mariadb.yml` - prod mariadb apb instance to back up
* manually fix and run the command in annotate.yml with the correct pod to annotate it for backup. Very not yaml at the moment
* `oc create -f backup.yml` to backup the pod
* Delete the namespace to test further
* `oc create -f restore.yml to restore it`

## TODO
Make this happen in less than 57 steps


## Known Issues
* Lots of manual steps and work arounds Working on it.
