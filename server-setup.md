Step 1 — Logging in as root

ssh root@your_server_ip

Step 2 — Creating a New User

adduser sammy

Step 3 — Granting Administrative Privileges

usermod -aG sudo sammy
You can now type sudo before commands to run them with superuser privileges when logged in as your regular user.

Step 4 — Setting Up a Firewall
You can examine the list of installed UFW profiles by typing:

ufw app list

ufw allow OpenSSH
Now enable the firewall by typing:

ufw enable
Type y and press ENTER to proceed. You can see that SSH connections are still allowed by typing:

ufw status
Output
Status: active

Step 5 — Enabling External Access for Your Regular User

ssh sammy@your_server_ip
After entering your regular user’s password, you will be logged in. Remember, if you need to run a command with administrative privileges, type sudo before it like this:

sudo command_to_run
You will receive a prompt for your regular user’s password when using sudo for the first time each session (and periodically afterward).

To enhance your server’s security, we strongly recommend setting up SSH keys instead of using password authentication. Follow our guide on setting up SSH keys on Ubuntu 22.04 to learn how to configure key-based authentication.

If the root Account Uses SSH Key Authentication
If you logged in to your root account using SSH keys, then password authentication is disabled for SSH. To log in as your regular user with an SSH key, you must add a copy of your local public key to your new user’s ~/.ssh/authorized_keys file.

Since your public key is already in the root account’s ~/.ssh/authorized_keys file on the server, you can copy that file and directory structure to your new user account using your current session.

The simplest way to copy the files with the correct ownership and permissions is with the rsync command. This command will copy the root user’s .ssh directory, preserve the permissions, and modify the file owners, all in a single command. Make sure to change the highlighted portions of the command below to match your regular user’s name:

Note: The rsync command treats sources and destinations that end with a trailing slash differently than those without a trailing slash. When using rsync below, ensure that the source directory (~/.ssh) does not include a trailing slash (check to make sure you are not using ~/.ssh/).

If you accidentally add a trailing slash to the command, rsync will copy the contents of the root account’s ~/.ssh directory to the sudo user’s home directory instead of copying the entire ~/.ssh directory structure. The files will be in the wrong location and SSH will not be able to find and use them.

rsync --archive --chown=sammy:sammy ~/.ssh /home/sammy
Now, open up a new terminal session on your local machine, and use SSH with your new username:

ssh sammy@your_server_ip
You should be connected to your server with the new user account without using a password. Remember, if you need to run a command with administrative privileges, type sudo before the command like this:

sudo command_to_run
You will be prompted for your regular user’s password when using sudo for the first time each session (and periodically afterward).
