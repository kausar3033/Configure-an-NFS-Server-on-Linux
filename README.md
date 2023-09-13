## Step 1: Update system packages

	sudo apt update

## Step 2: Install NFS server

	sudo apt install nfs-kernel-server

## Step 3: Make shared NFS directory

	sudo mkdir -p /mnt/nfs_share
	
## Step 4: Set directory permissions

	sudo chown -R nobody:nogroup /mnt/nfs_share/
	
# Step 5: Set file permissions

	sudo chmod 777 /mnt/nfs_share/
	
# Step 6: Grant NFS access

	sudo vim /etc/exports
	
### Now, it is up to you whether you want to grant access to the entire subnet, single or multiple clients. For instance, we will permit an entire subnet “10.0.2.15/24” to access the NFS share:

Example:

/mnt/nfs_share 10.0.2.15/24(rw,sync,no_subtree_check)


## Step 7: Exporting NFS directory

	sudo exportfs -a
	
## Step 8: Restart NFS server

	sudo systemctl restart nfs-kernel-server
	
## Step 9: Grant Firewall access

	sudo ufw allow from 10.0.2.15/24 to any port nfs
	
## Step 10: Enable Firewall

	sudo ufw enable
	
## Step 11: Check Firewall status

	sudo ufw status
	
# Step 1:Installing NFS client on Ubuntu 22.04

	sudo apt install nfs-common

## Step 2: Make shared NFS directory

	sudo mkdir -p /mnt/nfs_clientshare

## Then, mount the NSF share on the other Client system:

	sudo mount 10.0.2.15:/mnt/nfs_share /mnt/nfs_clientshare
	
	cd /mnt/nfs_share/
	
### Now check NFS create file .

## Then, switch to the client system and view the list of files present in the “nfs_clientshare” directory:
	
	ls -l /mnt/nfs_clientshare/
	
## Uninstalling NFS server on Ubuntu 22.04

	sudo apt remove nfs-kernel-server
	sudo apt remove nfs-common

