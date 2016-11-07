# Maintainer: Thomas Scheller <t.scheller@email.de>
#
# Repository: https://github.com/amiga23/aur-eclipse-che-arm

pkgname=eclipse-che-arm
pkgver=4.7.2
pkgrel=1
epoch=
pkgdesc="Open Source Platform for Cloud Based Development"
#arch=('armv7h' 'aarch64')
arch=('armv7h')
url="http://www.eclipse.org/che"
license=('EPL')
groups=()
depends=(java-runtime docker)
#makedepends=(go)
checkdepends=()
optdepends=()
provides=(eclipse-che)
conflicts=()
replaces=()
backup=('etc/conf.d/eclipse-che')
options=()
install=install
changelog=changelog
source=("http://mirror.switch.ch/eclipse/che/eclipse-che-$pkgver.tar.gz"
        'sysuser.conf'
	'eclipse-che.conf'
	'eclipse-che.service')
noextract=()
sha256sums=('2f85571929ebede0525fea15bcb8ebf4b1dcfd01cbccf86a81bd00d2668df91b'
            '519d891d5ff5abe85c9fedffa6af75571ed1b0e382b0b6a8b8d1b2de79b95e0e'
	    'c45e83a67c662479f54d40dcd1b16990073eab7e4e0da048b742429a8789c04c'
	    '1b189f593f10bb4961536d08dfd6b48598e4ff708214b36a9213f1709bd36a66')
package() {
#  mkdir codenvy
#  cd codenvy
#  export GOPATH=$srcdir/codenvy
#  go get github.com/gorilla/websocket
#  go get github.com/codenvy/pty
#  git clone https://github.com/codenvy/websocket-terminal.git
#  cd websocket-terminal
#  go build

  #modify repository for arm docker images
  cd $srcdir/eclipse-che*
  sed -i 's/codenvy\/ubuntu_jdk8/kartben\/armhf-che-jdk8/g' stacks/stacks.json
  sed -i 's/codenvy\/node/kartben\/armhf-che-node/g' stacks/stacks.json
  # Increase timeout
  sed -i 's/machine.ws_agent.max_start_time_ms=60000/machine.ws_agent.max_start_time_ms=240000/g' conf/che.properties
  # Change directories
  sed -i 's+che.user.workspaces.storage=${che.home}/workspaces+che.user.workspaces.storage=/var/lib/eclipse-che/workspaces+g' conf/che.properties
  sed -i 's+che.conf.storage=${catalina.base}/temp/local-storage+che.conf.storage=/var/lib/eclipse-che/temp/local-storage+g' conf/che.properties
  #install
  mkdir -p $pkgdir/usr/share
  mv $srcdir/eclipse-che-$pkgver $pkgdir/usr/share/eclipse-che

  # setup eclipse-che home
  install -m 755 -d $pkgdir/var/lib/eclipse-che
  install -m 755 -d $pkgdir/var/lib/eclipse-che/workspaces
  install -m 755 -d $pkgdir/var/lib/eclipse-che/temp/local-storage

  # create user (creation itself is done with install script)
  install -D -m 644 $srcdir/sysuser.conf "$pkgdir"/usr/lib/sysusers.d/eclipse-che.conf

  # install service
  install -Dm0644 $srcdir/eclipse-che.service $pkgdir/usr/lib/systemd/system/eclipse-che.service
  install -Dm0644 $srcdir/eclipse-che.conf $pkgdir/etc/conf.d/eclipse-che
}
