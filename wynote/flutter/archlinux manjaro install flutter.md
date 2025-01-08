需要先安装jdk 看我的system/manjaro quicksetup
yay -Ss android-sdk
yay -Sy android-sdk
yay -S android-tools
yay -S android-sdk-platform-tools
yay -S android-sdk-cmdline-tools-latest
yay -S android-sdk-build-tools
yay -S android-platform
yay -Ss fvm 
yay -Sy fvm
fvm releases
fvm install x.x.x 
fvm use x.x.x
fvm flutter

配置Android SDK 的路径
fvm flutter config --android-sdk /opt/android-sdk

更改文件夹权限 <username> 替换为你的用户名
sudo chown -R <username>:<username> /opt/flutter
sudo chown -R <username>:<username> /opt/android-sdk
sudo chown -R <username>:<username> /opt/dart-sdk

fvm flutter doctor --android-licenses
sudo ln -s /usr/bin/google-chrome-stable /usr/bin/google-chrome



sudo pacman -S clang

sudo pacman -S ninja

yay -Sy cmake

安装插件
