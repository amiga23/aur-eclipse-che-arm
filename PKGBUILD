# Maintainer: Thomas Scheller <t.scheller@email.de>
#
# Repository: https://github.com/amiga23/aur-eclipse-che-arm

pkgname=eclipse-che-arm
pkgver=4.2.0
pkgrel=4
epoch=
pkgdesc="Open Source Platform for Cloud Based Development"
arch=('armv7h')
url="http://www.eclipse.org/che"
license=('EPL')
groups=()
depends=(java-runtime docker)
makedepends=()
checkdepends=()
optdepends=()
provides=(eclipse-che)
conflicts=()
replaces=()
backup=('/etc/conf.d/eclipse-che')
options=()
install=install
changelog=changelog
source=('https://install.codenvycorp.com/che/eclipse-che-latest.zip'
        'sysuser.conf'
	'eclipse-che.conf'
	'eclipse-che.service')
noextract=()
sha256sums=('d8128797320c3a288916f54da3f85d058974199ff87213fdeb2e4e56913009a9'
            '519d891d5ff5abe85c9fedffa6af75571ed1b0e382b0b6a8b8d1b2de79b95e0e'
	    'c45e83a67c662479f54d40dcd1b16990073eab7e4e0da048b742429a8789c04c'
	    'e35b626413385856a33f59da6d65e0ce22c1d207e193fdc7fc79f98ce10d99d7')
package() {
  #modify repository for arm docker images
  cd eclipse-che*
  sed -i 's/codenvy\/ubuntu_jdk8/kartben\/armhf-che-jdk8/g' stacks/predefined-stacks.json
  sed -i 's/codenvy\/node/kartben\/armhf-che-node/g' stacks/predefined-stacks.json
  # Increase timeout
  sed -i 's/machine.ws_agent.max_start_time_ms=60000/machine.ws_agent.max_start_time_ms=240000/g' conf/che.properties
  # Change directories
  sed -i 's+che.user.workspaces.storage=${che.home}/workspaces+che.user.workspaces.storage=/var/lib/eclipse-che/workspaces+g' conf/che.properties
  sed -i 's+che.conf.storage=${catalina.base}/temp/local-storage+che.conf.storage=/var/lib/eclipse-che/temp/local-storage+g' conf/che.properties
  #install
  mkdir -p $pkgdir/usr/share
  mv $srcdir/eclipse-che-4.2.0 $pkgdir/usr/share/eclipse-che

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
