# AWS-EBS:
===============================
Part-1: Attach and Mount Extra EBS Volume to Linux EC2
===============================

Step 5: Verify and Format the Attached Volume

1. Switch to root user:
sudo -i

2. List all block devices:
lsblk

3. Check if a filesystem exists on the new volume:
file -s /dev/xvdf

4. Format the volume with XFS:
mkfs -t xfs /dev/xvdf

5. Verify that the filesystem is now XFS:
file -s /dev/xvdf


Step 6: Mount the Volume to the EC2 Instance

1. Create a new directory:
mkdir /mnt/extra_ebs

2. Mount the volume:
mount /dev/xvdf /mnt/extra_ebs

3. Check the mounted file systems:
df -h

4. Navigate to the mount directory:
cd /mnt/extra_ebs

5. Create a file:
touch 1.txt

6. Open the file in vi editor:
vi 1.txt
# Inside vi:
# Press 'i' to insert
# Type your Roll No
# Press 'Esc', then type ':wq' and hit Enter to save and exit

7. Confirm the size of the attached volume:
df -h


===============================
Part-2: Creating Files in EBS, Taking Snapshot & Attaching in Another Region
===============================

Step 1: Creating Files in EBS

1. Navigate to the mounted directory:
cd /mnt/extra_ebs

2. Verify the current directory:
pwd

3. Create a Python file:
vi 2.py
# Inside vi:
# Press 'i' to insert
# Type the following:
# a = 10
# b = 5
# print("Sum =", a + b)
# Press 'Esc', then type ':wq' to save and exit

4. Create a Java file:
vi 3.java
# Inside vi:
# Press 'i' to insert
# Type the following:
# public class Hello {
#     public static void main(String[] args) {
#         System.out.println("Welcome RollNo");
#     }
# }
# Press 'Esc', then type ':wq' to save and exit

5. Check that the files are created:
ls -l


Step 2: Generate Public Key from PEM File

ssh-keygen -y -f my-key.pem > my-key.pub


Step 3: Connect to New EC2 Instance in Different Region

1. Connect via SSH:
ssh -i my-key.pem ec2-user@<new-instance-public-ip>

2. Check current disk info:
sudo fdisk -l


Step 6: Mount Snapshot Volume on New EC2 Instance

1. Switch to root:
sudo -i

2. List block devices:
lsblk

3. Create mount directory:
mkdir /mnt/snap_volume

4. Mount the volume:
mount /dev/xvdf /mnt/snap_volume

5. Go to the mount directory:
cd /mnt/snap_volume

6. Check for presence of files:
ls -l
# You should see:
# 1.txt
# 2.py
# 3.java
