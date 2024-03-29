How to Mount S3 Bucket on CentOS/RHEL and Ubuntu using S3FS
Step 1: Remove Existing Packages

First check if you have any existing s3fs or fuse package installed on your system. If installed it already remove it to avoid any file conflicts.

CentOS/RHEL Users:
 # yum remove fuse fuse-s3fs

Ubuntu Users:
 $ sudo apt-get remove fuse
 
 Step 2: Install Required Packages

After removing above packages. First we will install all dependencies for fuse and s3cmd. Install the required packages to system use following command.

CentOS/RHEL Users:
 # yum install gcc libstdc++-devel gcc-c++ curl-devel libxml2-devel openssl-devel mailcap

Ubuntu Users:
 $ sudo apt-get install build-essential libcurl4-openssl-dev libxml2-dev mime-support
 
 
 Step 3: Download and Compile Latest Fuse

Download and compile latest version of fuse source code. For this article we are using fuse version 2.9.3. Following set of command will compile fuse and add fuse module in kernel.

# cd /usr/src/
# wget http://downloads.sourceforge.net/project/fuse/fuse-2.X/2.9.3/fuse-2.9.3.tar.gz
# tar xzf fuse-2.9.3.tar.gz
# cd fuse-2.9.3
# ./configure --prefix=/usr/local
# make && make install
# export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig
# ldconfig
# modprobe fuse


Step 4: Download and Compile Latest S3FS

Download and compile latest version of s3fs source code. For this article we are using s3fs version 1.74. After downloading extract the archive and compile source code in system.

# cd /usr/src/
# wget https://s3fs.googlecode.com/files/s3fs-1.74.tar.gz
# tar xzf s3fs-1.74.tar.gz
# cd s3fs-1.74
# ./configure --prefix=/usr/local
# make && make install


Step 5: Setup Access Key

Also In order to configure s3fs we would required Access Key and Secret Key of your S3 Amazon account. Get these security keys from Here.

# echo AWS_ACCESS_KEY_ID:AWS_SECRET_ACCESS_KEY > ~/.passwd-s3fs
# chmod 600 ~/.passwd-s3fs
Note: Change AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY with your actual key values.

Step 6: Mount S3 Bucket

Finally mount your s3 bucket using following set of commands. For this example, we are using s3 bucket name as mydbbackup and mount point as /s3mnt.
