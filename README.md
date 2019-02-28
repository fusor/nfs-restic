# nfs-restic

## Purpose
To simplify the set up for testing restic with NFS in EC2 after using origin3-dev to set up a cluster.

## Use
* Set up an Origin 3.11 cluster on EC2 using [origin3-dev](https://github.com/fusor/origin3-dev)

On your EC2 VM:
* Clone [nfs-restic](https://github.com/fusor/nfs-restic)
* `ansible-playbook setup.yml` to set up nfs and velero/restic.
* `ansible-playbook test.yml` to test restic with nfs
* `ansible-playbook clean.yml` to clean resources so you can test again
