
# How to view completed Job's log and get file from the container where the Job ran
A completed Job's log will get deleted from OKD console because the pod got deleted once the Job is completed.
Here is how you can view the Job's log and how to copy file from the container that ran the Job. 
(In this example it try to look at TWAS set trace Job):

1. Login to your OKD console and navigate to    
   ClusterConsole ===> Workloads ===> Jobs ===> and copy the Job's name   
   e.g: **kappnav-622bcc42-7ba1-4d37-b4a0-dc4cdfbd67fc**
   
2. Then ssh to your OKD VM to find out the container name that Job was running on and do the following:         
   sudo docker ps -a | grep kappnav-622bcc42-7ba1-4d37-b4a0-dc4cdfbd67fc         
   e.g: output is below:          
   1f11743d9fbb        docker.io/juniarti/app-nav-cmds@sha256:972cd06c896b2127dc66680f8385f0c6b70d70f2c298e62824f039a42456652b                       "sh set-tWAS-App-t..."   17 hours ago        Exited (0) 17 hours ago                         **k8s_kappnav-94923f40-bf7e-467e-bfab-fcba49650739_kappnav-622bcc42-7ba1-4d37-b4a0-dc4cdfbd67fc-72mjw_juniarti_8e5b29a2-e9fe-11e9-bd66-005056a0368e_0**   
   
   e6361de689be        docker.io/openshift/origin-pod:v3.11.0                                                                                        "/usr/bin/pod"           17 hours ago        Exited (0) 17 hours ago                         k8s_POD_kappnav-622bcc42-7ba1-4d37-b4a0-dc4cdfbd67fc-72mjw_juniarti_8e5b29a2-e9fe-11e9-bd66-005056a0368e_0
   
3. Using the container name from step 2 above, you can view the log as below:         
   sudo docker logs --details **k8s_kappnav-94923f40-bf7e-467e-bfab-fcba49650739_kappnav-622bcc42-7ba1-4d37-b4a0-dc4cdfbd67fc-72mjw_juniarti_8e5b29a2-e9fe-11e9-bd66-005056a0368e_0**
   
4. You can also copy files from docker container to your VM.       
   In this example, it is getting wsadmin.traceout file:           
   sudo docker cp **k8s_kappnav-94923f40-bf7e-467e-bfab-fcba49650739_kappnav-622bcc42-7ba1-4d37-b4a0-dc4cdfbd67fc-72mjw_juniarti_8e5b29a2-e9fe-11e9-bd66-005056a0368e_0**:/wsadmin/logs/wsadmin.traceout /home/ibmadmin/
