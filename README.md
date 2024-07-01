# ubuntu-virtual-swap-memory

'free -h'  - get details<br>

# checking swap

' cat /proc/meminfo ' to see total swap, and free swap (all linux)  <br>
'cat /proc/swaps' to see which swap devices are being used (all linux) <br>
'swapon -s' to see swap devices and sizes (where swapon is installed) <br>
'vmstat' for current virtual memory statistics <br>
'swapon --show' <br>

# debug
sudo swapon --all --verbose

//
# for **
dd if=/dev/zero of=/media/fasthdd/swapfile.img bs=1024 count=1M


# Resize Swap to 8GB
#Turn swap off <br>
#This moves stuff in swap to the main memory and might take several minutes <br>
sudo swapoff -a

#Create an empty swapfile <br>
#Note that "1G" is basically just the unit and count is an integer.<br>
#Together, they define the size. In this case 8GB. <br>
sudo dd if=/dev/zero of=/swapfile bs=1G count=8

#Set the correct permissions <br>
sudo chmod 0600 /swapfile <br>
(if not work sudo chmod 0644 /swapfile) <br>


#Set up a Linux swap area <br>
sudo mkswap /swapfile <br>
#Turn the swap on <br>
sudo swapon /swapfile  <br>


# Check if it worked
grep Swap /proc/meminfo

# Make it permanent (persist on restarts)
#Add this line to the end of your /etc/fstab: <br>
/swapfile swap swap sw 0 0

# swappiness Details
cat /proc/sys/vm/swappiness  <br>
sudo sysctl vm.swappiness=10  <br>
#Edit and add line <br>
sudo nano /etc/sysctl.conf  <br>
vm.swappiness=60 <br>
#Apply changes  <br>
sudo sysctl -p


# Restart required if not host is server

# Note swappiness
Swappiness can have a value between 0 and 100(200 according to chatgpt). A value of 0 instructs the kernel to aggressively avoid swapping out for as long as possible. A value of 100 will aggressively be swapping processes out of physical memory.
A lower value will make the kernel to try to avoid swapping whenever possible while a higher value means the kernel will try to use the swap space more aggressively.
Accessing swap memory is much slower than accessing physical memory directly. A lower value for the swappiness parameter will most likely improve overall system performance. For regular desktop installation, a value of 10 is recommended. A swappiness value of 0 or 1 is recommended for most database servers.
The optimal swappiness value depends on your system workload and the size of the RAM memory . You should adjust this parameter in small increments to find an optimal value.
