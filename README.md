# ubuntu-virtual-swap-memory

# checking swap

' cat /proc/meminfo ' to see total swap, and free swap (all linux)
'cat /proc/swaps' to see which swap devices are being used (all linux)
'swapon -s' to see swap devices and sizes (where swapon is installed)
'vmstat' for current virtual memory statistics
'swapon --show'

# debug
sudo swapon --all --verbose

//
# for **
dd if=/dev/zero of=/media/fasthdd/swapfile.img bs=1024 count=1M


# Resize Swap to 8GB
#Turn swap off <br>
#This moves stuff in swap to the main memory and might take several minutes <br>
sudo swapoff -a

# Create an empty swapfile
#Note that "1G" is basically just the unit and count is an integer.
#Together, they define the size. In this case 8GB.
sudo dd if=/dev/zero of=/swapfile bs=1G count=8

# Set the correct permissions
sudo chmod 0600 /swapfile (if not work sudo chmod 0644 /swapfile)


# Set up a Linux swap area
sudo mkswap /swapfile
 # Turn the swap on
sudo swapon /swapfile 


# Check if it worked
grep Swap /proc/meminfo

# Make it permanent (persist on restarts)
#Add this line to the end of your /etc/fstab:
/swapfile swap swap sw 0 0
