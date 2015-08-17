
pkgdesc="ROS - Playstation 3 SIXAXIS or DUAL SHOCK 3 joystick driver."
url='http://www.ros.org/'

pkgname='ros-hydro-ps3joy'
pkgver='1.9.10'
_pkgver_patch=0
arch=('i686' 'x86_64')
pkgrel=2
license=('BSD')

ros_makedepends=(ros-hydro-rospy
  ros-hydro-catkin
  ros-hydro-sensor-msgs
  ros-hydro-diagnostic-msgs
  ros-hydro-rosgraph)
makedepends=('cmake' 'git' 'ros-build-tools'
  ${ros_makedepends[@]}
  linuxconsole
  bluez
  libusb-compat
  python2-pybluez)

ros_depends=(ros-hydro-rospy
  ros-hydro-sensor-msgs
  ros-hydro-diagnostic-msgs
  ros-hydro-rosgraph)
depends=(${ros_depends[@]}
  linuxconsole
  bluez
  libusb-compat
  python2-pybluez)

_tag=release/hydro/ps3joy/${pkgver}-${_pkgver_patch}
_dir=ps3joy
source=("${_dir}"::"git+https://github.com/ros-gbp/joystick_drivers-release.git"#tag=${_tag})
md5sums=('SKIP')

build() {
  # Use ROS environment variables
  /usr/share/ros-build-tools/clear-ros-env.sh
  [ -f /opt/ros/hydro/setup.bash ] && source /opt/ros/hydro/setup.bash

  # Create build directory
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build

  # Fix Python2/Python3 conflicts
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/${_dir}

  # Build project
  cmake ${srcdir}/${_dir} \
        -DCMAKE_BUILD_TYPE=Release \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/hydro \
        -DPYTHON_EXECUTABLE=/usr/bin/python2 \
        -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 \
        -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
