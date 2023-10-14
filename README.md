# Pre-Assessment - The Agency Source

## Task 1. 

### Create a user on a Linux server.


Here are the steps to create a user on a Linux server:

1. **Connect to the Server**: You need to connect to the Linux server. You can do this using SSH. Open your terminal and use the following command, replacing `server_ip_address` with your server's IP address:

   ```bash
   ssh username@server_ip_address
   ```

   Replace `username` with your own username or the username with sufficient privileges, such as "root" or a user with sudo access.

2. **Switch to Root (Optional)**: If you are not already logged in as the root user and you have sudo privileges, switch to the root user:

   ```bash
   sudo su -
   ```

3. **Create a New User**: To create a new user, use the `adduser` command and provide the desired username when prompted. For example, to create a user named "newuser":

   ```bash
   adduser newuser
   ```

   You will be asked to set a password for the new user and provide additional information like the full name, room number, etc. You can leave these fields empty if you don't want to add that information.

4. **Set Password (Optional)**: If you want to set or change the user's password after the user is created, use the `passwd` command:

   ```bash
   passwd newuser
   ```

   Replace "newuser" with the actual username.

5. **Grant Sudo Privileges (Optional)**: If you want to grant the new user sudo privileges (the ability to run commands as superuser), you can add the user to the "sudo" group. On Ubuntu, the "sudo" group is typically used for this purpose:

   ```bash
   usermod -aG sudo newuser
   ```

   On some other Linux distributions, you might use the "wheel" group or a similar group for this purpose.

6. **Test the New User**: To test if the new user can log in, you can switch to that user using the `su` command:

   ```bash
   su - newuser
   ```

   You'll be prompted for the user's password. If the login is successful, you've successfully created a user on the Linux server.

7. **Exit User Session**: After testing, you can exit the user's session by typing `exit`.



## Task 2. 

### Then you need to add the SSH keys of your laptop to that server user.

Here are the steps to add your SSH keys to a user on a Linux server:

1. **Generate SSH Keys on Your Laptop** (If you haven't already):

   If you don't have SSH keys generated on your laptop, you can create them using the following command. This will create a public key (`id_rsa.pub`) and a private key (`id_rsa`) in the `~/.ssh` directory on your laptop.

   ```bash
   ssh-keygen
   ```

   Make sure to protect your private key with a strong passphrase.

2. **Copy Your Public Key to the Server**:

   You need to copy the contents of your SSH public key to the server user's `~/.ssh/authorized_keys` file. You can use the `ssh-copy-id` command to do this. Replace `username` with the username you created on the server and `server_ip_address` with the server's IP address:

   ```bash
   ssh-copy-id username@server_ip_address
   ```

   You will be prompted to enter the user's password on the server.

   Alternatively, if `ssh-copy-id` is not available, you can manually copy and append the contents of your local `~/.ssh/id_rsa.pub` file to the server's `~/.ssh/authorized_keys` file using SSH and a text editor. Here's an example using `ssh` and `cat`:

   ```bash
   cat ~/.ssh/id_rsa.pub | ssh username@server_ip_address "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
   ```

   This command will copy your public key to the server.

3. **Secure SSH Key Permissions on the Server** (Recommended):

   It's important to ensure that the `.ssh` directory and the `authorized_keys` file on the server are only accessible to the user and no one else. You can set the correct permissions by running the following commands on the server:

   ```bash
   chmod 700 ~/.ssh
   chmod 600 ~/.ssh/authorized_keys
   ```

4. **Test SSH Login**:

   You should now be able to SSH into the server without being prompted for a password:

   ```bash
   ssh username@server_ip_address
   ```

   If you've set up everything correctly, you will log in without a password.


## Task 3. 

### Then you should be able to SSH into the server from your laptop, without a password.

If you've successfully added your SSH keys to the server user as explained in the previous steps, you should be able to SSH into the server from your laptop without a password. Here's how to do it:

1. Open your terminal on your laptop.

2. Use the `ssh` command to log in to the server. Replace `username` with the server user you created and `server_ip_address` with the server's IP address:

   ```bash
   ssh username@server_ip_address
   ```

   If everything is set up correctly, you should be able to log in without being prompted for a password.

That's it! You can now securely SSH into the Linux server from your laptop without needing to enter a password each time. Your SSH key is used for authentication instead.
