## Lost in Time
**Title:** Lost in Time  
**Author:** Suraj 
**Points:** 300  

**Description:**

During an investigation into potential misconduct at WindShine Pvt Ltd, an employee stumbles upon a mysterious disk image rumored to hold important secrets. However, the password to unlock it remains unknown. Can you help uncover the hidden secrets?

---

## Writeup

**Step 1: Mount the Disk Image**

   We've been provided with a `.img` file, which is a disk image—a complete copy of a storage device or a portion of it. Disk images are often used for backup or distribution purposes, as they contain the exact contents and structure of the original disk, allowing     users to access and manipulate the files contained within.

   To access the contents of the provided `.img` file, we need to mount it. Mounting is the process of making the filesystem on the disk image accessible to the operating system. Follow these steps:

1. **Open Terminal** on your system.
2. Create a mount point (a directory where the image will be accessible):
```bash
sudo mkdir /mnt/disk_image
```
3. Mount the disk image using the following command (replace image.img with the actual name of your image file):
```bash
sudo mount -o loop image.img /mnt/disk_image
```

4. Now, we can navigate to the mounted directory:
```bash
cd /mnt/disk_image
```

After mounting the image, we will see a Linux-like environment resembling a directory structure similar to a typical Linux filesystem. You'll notice directories like **/home**, **/root**, and **/usr**. The **/home** directory is commonly where user files are stored, providing a personal space for each user to manage their documents, downloads, and configurations.

**Step 2: View All Files**

As you search through the directories, you may need to list all files, including those that may not be immediately visible. To view all files in the current directory, including those that may be hidden, use the following command:

```bash
ls -a
```

**Step 3: Explore the Directory Structure**

Navigate through the directories to gather information. Start by examining the /home/windshine directory:

```bash
cd home/windshine
```
As you explore the Documents directory, you will find a suspicious file named .secret.txt.enc

![secret_file](img/term1.png)

**Step 4: Identify the Encrypted File**

Upon locating the .secret.txt.enc file, you will discover that it is encrypted, indicated by the .enc extension. This suggests that the file requires a password to access its contents.

**Step 5: Check the Bash History**

The bash_history file records the commands previously executed by the user. We can check this file to find any commands that might help us in our investigation, especially those related to file encryption. Use the following command:

```bash
cat .bash_history
```
in the home directory of the image (not your bash_history file)

Look for commands that suggest any recent file operations or encryption activities. This may lead you to discover useful information, including the password used for encrypting the secret file.

![history](img/term2.png)

You might see a command in the bash_history file like: `openssl enc -aes-256-cbc -salt -in secret.txt -out secret.txt.enc -k "grepHistoryForFun" `

This command indicates that the file was encrypted using the AES-256-CBC algorithm, a widely used symmetric encryption standard. The -salt option helps to protect against dictionary attacks, while -k specifies the password used for encryption. So the password used here is `grepHistoryForFun`

**Step 6: Decrypting the Encrypted File**

Once you've identified the password from the bash_history, you can use it to decrypt the file. Use the following command, replacing YOURPASSWORD with the actual password obtained:

```bash
openssl enc -aes-256-cbc -d -in .secret.txt.enc -out secret.txt -pass pass:YOURPASSWORD
```

![decrypt](img/decrypt.png)

**Step 7: Access the Decrypted File**

After running the decryption command, you will find the decrypted file in the same directory. You can view its contents using:

```bash
cat secret.txt
```

which gives us the flag

![flag](img/flag.png)

**Flag:** cyberarc{C0mm4nd_H1st0ry_3xp0s3s_M4l1c10us_Act1v1ty}
