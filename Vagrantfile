$script = <<-SCRIPT
apt-get update -y
apt-get upgrade -y
apt-get install -y ack antlr3 asciidoc autoconf automake autopoint binutils bison build-essential \
bzip2 ccache cmake cpio curl device-tree-compiler fastjar flex gawk gettext gcc-multilib g++-multilib \
git gperf haveged help2man intltool libc6-dev-i386 libelf-dev libglib2.0-dev libgmp3-dev libltdl-dev \
libmpc-dev libmpfr-dev libncurses5-dev libncursesw5-dev libreadline-dev libssl-dev libtool lrzsz \
mkisofs msmtp nano ninja-build p7zip p7zip-full patch pkgconf python2.7 python3 python3-pyelftools \
libpython3-dev qemu-utils rsync scons squashfs-tools subversion swig texinfo uglifyjs upx-ucl unzip \
vim wget xmlto xxd zlib1g-dev
cd /home/vagrant
git clone https://github.com/bernylinville/lede.git
cd /home/vagrant/lede
./scripts/feeds update -a
./scripts/feeds install -a
make download -j8
make V=s -j$(nproc)
SCRIPT

Vagrant.configure("2") do |config|
    config.vm.box = "debian/bullseye64"
    config.vm.provider :libvirt do |l|
        l.memory = 8192
        l.cpus = 8
        l.storage_pool_name = "images"
    end
    config.vm.provision "shell", inline: $script
end
