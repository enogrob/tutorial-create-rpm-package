```
Roberto Nogueira  
BSd EE, MSd CE
Solution Integrator Experienced - Certified by Ericsson
```
# Tutorial 

![tutorial image](images/tutorial.png)

**About**

This article shows you how to package a script into an RPM file for easy installation, updating, and removal from your Linux systems. Before I jump into the details, I'll explain what an RPM package is, and how you can install, query, remove, and, most importantly, create one yourself.

This article covers:

* What an RPM package is.
* How to create an RPM package.
* How to install, query, and remove an RPM package.

**Refs:**
* [How to create a Linux RPM package](https://www.redhat.com/sysadmin/create-rpm-package)
* [How To Add and Delete Users on a CentOS 7 Server](https://www.digitalocean.com/community/tutorials/how-to-add-and-delete-users-on-a-centos-7-server)

## Topics

1. Installing the required software:
```
centos7
yum install -y rpmdevtools rpmlint
```

2. After installing rpmdevtools, we can run the following as a user called `sai.local`:
**Note:** Do not build RPM packages as the root user. This is highly discouraged.
```
adduser sai.local
yum install tree vim -y

su - sai.local
rpmdev-setuptree
tree rpmbuild
```

3. Place the script `rm-ssh-offendingkey` in the designated directory
```
mkdir -p ~/rpmbuild/SOURCES/sshscripts-1/rm-ssh-offendingkey-1/
```

4. Subsequently, I .tar.gz the source as follows:
```
cd ~/rpmbuild/SOURCES/ && tar zcvf sshscripts-1.tar.gz sshscripts-1/
```

5. Create the .spec file
```
cd ~/rpmbuild/SPECS/
rpmdev-newspec rm-ssh-offendingkey
vim rm-ssh-offendingkey
```

6. Check macros
```
rpm --eval '%{_bindir}'
rpm --eval '%{_datadir}'
rpm --eval '%{_sysconfdir}'
```

7. Checking the .spec file on error (rpmlint)
```
rpmlint ~/rpmbuild/SPECS/rm-ssh-ffendingkey.spec
```

8. Building the package (rpmbuild)
```
rpmbuild -bs ~/rpmbuild/SPECS/rm-ssh-offendingkey.spec
```

9. To create the binary .rpm package, use:
```
rpmbuild -bb ~/rpmbuild/SPECS/rm-ssh-offendingkey.spec
```

10. Installing the RPM package
```
rpm -ivh /home/sai.local/rpmbuild/RPMS/noarch/sshscripts-1-0.noarch.rpm
```

11. Verifying the package has been installed
```
rpm -qi sshscripts-1
```