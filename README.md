# NFS-server-on-Ubuntu
How to install the NFS server on Ubuntu

### Step 1:update your system
```
sudo apt update
```
### Step 2:install nfs
```
sudo apt install nfs-kernel-server
```
```
sudo systemctl status nfs-server
```
### Step 3: Create an NFS directory share
```
sudo mkdir /mnt/beluga_jr_shares
```
We will assign the following directory ownership and permissions since we want all of the files to be accessible to all clients.
```
sudo chown nobody:nogroup /mnt/beluga_jr_shares
```
```
sudo chmod -R 777 /mnt/beluga_jr_shares
```
All of the files and subdirectories that you create will have these recursive permissions applied to them.

### Step 4: Access clients to the NFS Server
```
sudo nano /etc/exports
```
```
/mnt/beluga_jr_shares 192.168.0.0/24 (rw,sync,no_subtree_check)
```
This makes the server accessible to every client in the 192.168.0.0 subnet. In this instance, we’ll provide all clients access to the NFS server as demonstrated.
/mnt/beluga_jr_shares 192.168.2.0/24(rw,sync,no_subtree_check)

Let’s quickly review the permissions and what they represent.

rw  (Read and Write )
sync  (Write changes to disk before applying them)
no_subtree_check  (Avoid subtree checking )

### Step 5: Export the shared directory

Use the following command to export the directory and make it accessible:
```
sudo exportfs -a
```
Restart NFS server

To restart the NFS server on your Ubuntu 22.04 machine, type the following command:
```
sudo systemctl restart nfs-kernel-server
```
### Step 6: Set up the NFS Server firewall rule.

If you are protected by a UFW firewall, you must use the syntax displayed to permit NFS traffic through the firewall.
```
sudo ufw allow from [client-IP] to any port nfs

sudo ufw allow from 10.0.2.15/24 to any port nfs 
```
### Step 7: Enable Firewall
```
sudo ufw reload 
```
```
sudo ufw status
```
### Step 8: Configure the Client system
```
sudo apt update
```
```
sudo apt install nfs-common
```
```
sudo mkdir -p /mnt/client_shared
```
```
sudo mount 192.168.2.103:/mnt/beluga_jr_shares /mnt/client_shared
```
### Step 9: Testing the NFS Share setup
```
cd /mnt/beluga_jr_shares
touch demoshare_file.txt
Test-NFS-Server-Ubuntu-22-04
```
```
ls /mnt/client_shared_folder/
```
