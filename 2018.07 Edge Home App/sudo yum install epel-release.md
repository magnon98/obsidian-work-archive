sudo yum install epel-release
 
cat \<\<EOF | sudo tee /etc/yum.repos.d/vscode.repo  
[code]  
name=Visual Studio Code  
baseurl=https://packages.microsoft.com/yumrepos/vscode  
enabled=1  
gpgcheck=1  
gpgkey=https://packages.microsoft.com/keys/microsoft.asc  
EOF
 
sudo yum install golang golang-godoc glide git code
   

mkdir ~/go
 
echo \>\> ~/.bashrc  
echo "export LC_COLLATE=\"C\"" \>\> ~/.bashrc  
echo "alias ls='/usr/bin/ls --color=auto --group-directories-first'" \>\> ~/.bashrc  
echo "alias ll='ls -al'" \>\> ~/.bashrc
 
echo \>\> ~/.bashrc  
echo export GOROOT=`go env GOROOT` \>\> ~/.bashrc  
echo export GOPATH=$PWD/go \>\> ~/.bashrc  
echo export PATH=\$PATH:\$GOROOT/bin \>\> ~/.bashrc
          
git clone [http://192.168.100.35/bliex/home-app-container.git](http://192.168.100.35/bliex/home-app-container.git)  
cd home-app-container  
git checkout golang
 
./init.sh