# ubuntu-virtual-swap-memory

'free -h'  - get details<br>
cd /proc/sys/vm/swappiness


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
vm.swappiness=10 <br>
#Apply changes  <br>
sudo sysctl -p
