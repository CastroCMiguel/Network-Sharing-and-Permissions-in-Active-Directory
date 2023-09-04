<p align="center">
<img src="https://i.imgur.com/tC2leBg.jpg" alt="1"/>
</p>

<h1>Understanding File Permissions</h1>

This lab delves into the realm of file permissions and shares within the framework of an Active Directory domain. In a business environment, file permissions and shares are crucial to ensuring that users have the necessary access and permissions to files relevant to their roles. This lab builds upon a previous one where a client was successfully joined to the <a href="https://github.com/CastroCMiguel/Configuring-On-premises-Active-Directory-within-Azure-VMs">"mydomain.com"</a> domain. For this exercise, I am logged in as Jane Doe, who possesses an admin account on the domain controller VM, and as a regular user on the client VM.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10

<h2>Video Demonstration</h2>

### [Network File Shares and Permissions](https://www.youtube.com/watch?v=d--RznSX9NU)

<h2>File Permissions Configuration Steps</h2>

<p align="center">
<img src="https://i.imgur.com/vVfG9DX.png" alt="1"/>
</p>

To establish permissions for folders and files, it is essential to create the folders for sharing. While logged in to the domain controller VM as an administrator, I have created four folders with appropriate names on the C:\ drive. To share a folder and allocate permissions, the following steps were taken:

1. Open the folder's Properties.
2. Under the Sharing tab, click on "Share."
3. Specify the network users with whom you want to share the folder and assign the relevant permissions.

<p align="center">
<img src="https://i.imgur.com/rBGRxWs.png" alt="1"/>
</p>

For the folders in this setup, the permissions were configured as follows:

- Domain Users were granted "Read" permissions for the "read-access" folder, and they were given "Read/Write" permissions for the "write-access" folder.
- Domain Admins were granted "Read/Write" access to the "no-access" folder.

(Note: The permissions for the "accounting" folder are planned to be adjusted later.)

<p align="center">
<img src="https://i.imgur.com/IfksOXX.png" alt="1"/>
</p>

On the client VM, I accessed the shared folders using the following path in File Explorer: \dc-1. I observed that some folders only allowed viewing files without the ability to add new ones, while one folder didn't grant access at all. This behavior is a result of how permissions are configured for the folders, considering the user's membership in the respective Security Group and the folder's specific permissions for users within that Security Group.

<p align="center">
<img src="https://i.imgur.com/eVAVPGs.png" alt="1"/>
</p>

The next step involves creating a new Security Group and granting appropriate permissions to the "accounting" folder. Here are the steps taken:

1. On the domain controller, the Active Directory Users and Computers panel was opened.
2. A new Group named "ACCOUNTANTS" was created.
3. After creating the new Group, permissions were assigned to the "accounting" folder to ensure that the "ACCOUNTANTS" Group has "Read/Write" permissions for the folder.

<p align="center">
<img src="https://i.imgur.com/0Uk26pv.png" alt="1"/>
</p>

To grant access to the "accounting" folder, the following steps were taken:

1. The user, bel.hof, was logged off the client to ensure that permissions take effect when logged in again.
2. On the domain controller, the "ACCOUNTANTS" Properties were opened in Active Directory Users and Computers.
3. In the Members tab, the respective user, bel.hof, was added to the "ACCOUNTANTS" Security Group.

<p align="center">
<img src="https://i.imgur.com/T4pYK73.png" alt="1"/>
</p>

4. Upon logging back into the client, bon.rovej was able to access the "accounting" folder because they were now a member of the "ACCOUNTANTS" group, which had the necessary permissions for that folder.

<p align="center">
<img src="https://i.imgur.com/6AoXBXz.png" alt="1"/>
</p>

<h2>Summary</h2>

This lab provided valuable insights into how file permissions function within the Windows/Active Directory environment. It highlighted the importance of carefully configuring permissions to ensure that individuals have access only to the resources they require to perform their tasks. Granting minimal necessary permissions is crucial to maintaining security and data integrity in a real-world setting.
