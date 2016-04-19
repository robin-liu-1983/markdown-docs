# CentOS6是目前最为高效和易用的服务器版本之一
## Fedora和EL使用rpmfusion镜像使用帮助
su -c 'yum localinstall --nogpgcheck [http://mirrors.163.com/rpmfusion/free/fedora/rpmfusion-free-release-stable.noarch.rpm](http://mirrors.163.com/rpmfusion/free/fedora/rpmfusion-free-release-stable.noarch.rpm) [http://mirrors.163.com/rpmfusion/nonfree/fedora/rpmfusion-nonfree-release-stable.noarch.rpm](http://mirrors.163.com/rpmfusion/nonfree/fedora/rpmfusion-nonfree-release-stable.noarch.rpm)'

su -c 'yum localinstall --nogpgcheck [http://mirrors.163.com/rpmfusion/free/fedora/rpmfusion-free-release-rawhide.noarch.rpm](http://mirrors.163.com/rpmfusion/free/fedora/rpmfusion-free-release-rawhide.noarch.rpm) [http://mirrors.163.com/rpmfusion/nonfree/fedora/rpmfusion-nonfree-release-rawhide.noarch.rpm](http://mirrors.163.com/rpmfusion/nonfree/fedora/rpmfusion-nonfree-release-rawhide.noarch.rpm)'

## rpmforge使用帮助（适用于RHEL，CentOS，Scientific Linux）
Servers (eg. monitoring, troubleshooting, management) Desktops (eg. office, leisure, multi-media) Development (eg. perl, python, ruby libraries)

[http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.i686.rpm](http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.i686.rpm) [http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm](http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm)

Hints:

Use cat /etc/redhat-release to find which release of EL you are using Use uname -a to find your processor architecture Use rpm -ivh package-filename to install the rpmforge-release package (also works with URLs) You can use wget or curl to download the package using one of the above links if needed (for example on a server with no X Window) Then you can use yum to install the available packages from the RepoForge repo Afterward, you can disable accidental updates from the repo by setting enabled = 0 in the repo definition file in /etc/yum.repos.d/
