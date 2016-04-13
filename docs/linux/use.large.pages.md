# use large pages

## References
* http://www.oracle.com/technetwork/java/javase/tech/largememory-jsp-137182.html
* http://jose-manuel.me/2012/11/how-to-enable-the-jvm-option-uselargepages-in-redhat/

[Large page support is included in 2.6 kernel. Some vendors have backported the code to their 2.4 based releases.](http://www.oracle.com/technetwork/java/javase/tech/largememory-jsp-137182.html)

##### Check if your system can support large page memory
```
cat /proc/meminfo | grep Huge 
```
[If the output shows the three "Huge" variables then your system can support large page memory, but it needs to be configured. If the command doesn't print out anything, then large page support is not available.](http://www.oracle.com/technetwork/java/javase/tech/largememory-jsp-137182.html)
```
HugePages_Total: 0 
HugePages_Free: 0 
Hugepagesize: 2048 kB 
```

##### What is shared memory?
* *Shared memory allows processes to access common structures and data by placing them in shared memory segments. It is the fastest form of inter-process communication available since no kernel involvement occurs when data is passed between the processes. In fact, data does not need to be copied between the processes.* (https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/5/html/Tuning_and_Optimizing_Red_Hat_Enterprise_Linux_for_Oracle_9i_and_10g_Databases/chap-Oracle_9i_and_10g_Tuning_Guide-Setting_Shared_Memory.html)

##### Increase SHMMAX value
*It must be larger than the Java heap size. On a system with 4 GB of physical RAM (or less) the following will make all the memory sharable:*
```
sudo echo 4294967295 > /proc/sys/kernel/shmmax 
```

##### Reload the changes into the running kernel
```
sysctl -p
```

##### Specify the number of large pages 
*In the following example 3 GB of a 4 GB system are reserved for large pages (assuming a large page size of 2048k, then 3g = 3 x 1024m = 3072m = 3072 * 1024k = 3145728k, and 3145728k / 2048k = 1536):*
```
echo 1536 > /proc/sys/vm/nr_hugepages 
```

##### Reload the changes into the running kernel
```
sysctl -p
```
*Note the /proc values will reset after reboot so you may want to set them in an init script (e.g. rc.local or sysctl.conf).*