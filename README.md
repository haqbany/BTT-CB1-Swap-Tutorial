How to Create and Configure a Swap File on a BTT-CB1

This tutorial will guide you through the process of creating and configuring a swap file on a BTT-CB1. Increasing swap space can help manage memory usage and improve system stability for memory-intensive tasks.

Prerequisites

	•	A BTT-CB1 running a Debian-based distribution.
	•	Basic knowledge of using the terminal.

Step-by-Step Guide

Step 1: Turn Off Existing Swap

If there’s an existing swap file, turn it off to avoid conflicts.

sudo swapoff -a

Step 2: Remove Existing Swap File

Remove the existing swap file if it exists.

sudo rm /var/swap

Step 3: Create a New Swap File

Create a new swap file with the desired size. Here, we’ll create a 4GB swap file.

sudo fallocate -l 4G /var/swap

If fallocate is not available, use dd:

sudo dd if=/dev/zero of=/var/swap bs=1M count=4096 status=progress

Step 4: Set Correct Permissions

Set the correct permissions for the swap file.

sudo chmod 600 /var/swap

Step 5: Set Up the Swap Area

Initialize the swap file.

sudo mkswap /var/swap

Step 6: Turn On the Swap

Activate the swap file.

sudo swapon /var/swap

Step 7: Verify the Swap Size

Check to ensure the swap space is active and verify its size.

free -h

You should see the swap size listed as 4.0GiB.

Step 8: Make the Swap File Permanent

To make sure the swap file is used after a reboot, add it to the /etc/fstab file.

sudo nano /etc/fstab

Add the following line to the end of the file:

/var/swap none swap sw 0 0

Save the file by pressing Ctrl + O, then Enter, and exit by pressing Ctrl + X.

Step 9: Reboot the System

Reboot your BTT-CB1 to apply the changes.

sudo reboot

Step 10: Verify Swap Space After Reboot

After the system has rebooted, log back in and run:

free -h

This command will confirm that the swap space is still active and correctly set up.

Example Output

After completing these steps, you should see output similar to this:

total        used        free      shared  buff/cache   available
Mem:           986Mi        90Mi       69Mi       0.0Ki       827Mi       815Mi
Swap:          4.0Gi          0B       4.0Gi

Caution
Backup before anything !!
