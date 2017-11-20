# Cloud scripts

These scripts configure Ubuntu on EC2 graphics instances to support running OpenGL applications in TurboVNC via VirtualGL.

Hint: use a spot instance and attach an external volume where you can save your work - this will result in major cost savings!

# How to use

ip=239.239.239.239
private_key=~/.ssh/private_key.pem

ssh -p 22 -i ${private_key} ubuntu@${ip}

git clone https://github.com/agisoft-llc/cloud-scripts
cd cloud-scripts
chmod +x configure.sh
./configure.sh

# Wait a while when instance will be rebooted, then reconnect to start vnc server:
ssh -p 22 -i ${private_key} ubuntu@${ip}

cd cloud-scripts
chmod +x start_vnc_server.sh
./start_vnc_server.sh
# You will be asked to enter Password twice.
# You will be also asked:
#  Would you like to enter a view-only password (y/n)? n

# Press Ctrl+D to disconnect

# Connect with TurboVNC:
/opt/TurboVNC/bin/vncviewer ${ip}:5901
# Enter password you configured above

# Download PhotoScan from http://www.agisoft.com/downloads/installer/
wget http://download.agisoft.com/photoscan-pro_1_3_4_amd64.tar.gz
# Extract it:
tar -zxf photoscan-pro_1_3_4_amd64.tar.gz
# Now you can run any OpenGL application with vglrun:
vglrun photoscan-pro/photoscan.sh

# References

https://github.com/yrahal/ec2-setup/

https://virtualgl.org/Documentation/HeadlessNV
