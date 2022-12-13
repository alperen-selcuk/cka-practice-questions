# cka-practice-questions

this questions help you to achive cka exam.

1.
Create a namespace cka. All resources should be created in this namespace.
***

2. 
Create a new Secret named mysql-password that has the following key=value pair:

mysql_root_password = Mysql5.6Password
***
3. 
Create a new PersistentVolume named pv-mysql.

Set capacity to 1Gi.

Set accessMode to ReadWriteOnce.

Set hostPath to /data_mysql.

Set persistentVolumeReclaimPolicy to Recycle.

The volume should have no storageClassName defined.

***
4. 

Create a new PersistentVolumeClaim named pvc-mysql. 
It should request 1Gi storage, accessMode ReadWriteOnce and should not define a storageClassName. 
The PVC should bound to the PV correctly.

***
5. 
Create a new StatefulSet named mysql.

Use container image mysql:5.6.

The container in the pod should runAsUser=65534 and runAsGroup=65534.

Mount the persistent volume pv-mysql at /var/lib/mysql.

There should be only 1 replica running.

Define initContainer named fix-permissions that uses image busybox:1.35.

The init container should runAsUser=0.

The init container should mount the persistent volume pv-mysql and run the following command: ["sh", "-c", "chown -R 65534:65534 /var/lib/mysql"].

***
6. 

Configure the stateful set mysql deployment so that the underlying container has the following environment variables set:
MYSQL_ROOT_PASSWORD from secret mysql-password key mysql_root_password.
***
7. 

Create a new ClusterIP Service named mysql which exposes mysql pods from the stateful set on port 3306.
***
8. 

Create a new Deployment named wordpress.

Use container image wordpress:4.8-apache.

Use deployment strategy Recreate.

There should be 3 replicas created.

The pods should request 10m cpu and 64Mi memory.

The livenessProbe should perform an HTTP GET request to the path /readme.html and port 80 every 5 seconds.

Configure PodAntiAffinity to ensure that the scheduler does not co-locate replicas on a single node.

Pods of this deployment should be able to run on master nodes as well, create the proper toleration.

***
9. 

Configure wordpress deployment so that the underlying container has the following environment variables set:

WORDPRESS_DB_PASSWORD from secret mysql-password key mysql_root_password.

WORDPRESS_DB_HOST set to the following value: mysql.

***
10.

Create a NodePort Service named wordpress which exposes wordpress deployment on port 80 and connects to the containers on port 80. 
The port on the node should be set to 31234.

***
11. 

Create a new NetworkPolicy named netpol-mysql. Use the app label of pods in your policy. 
The policy should allow the mysql-* pods to:

Connect to IP block 10.0.0.0/8.

Accept ingress traffic on port 3306 from wordpres-* pods only.

***
12. 
Navigate your web browser to http://${NODE_IP_ADDRESS}:31234/ and take a moment to enjoy a brand new instance of WordPress on Kubernetes.

***
13. 

Take a backup of etcd running on the control plane and save it on the control plane to /tmp/etcd-backup.db.
***
14. 

Delete wordpress deployment configuration from the cluster. Verify that the application is no longer accessible.
***
15. 
Restore etcd configuration from the backup file /tmp/etcd-backup.db. Confirm that the cluster is working and that all wordpress pods are back.
***
