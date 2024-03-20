pkgdesc="ROS - A simple viewer for ROS image topics."
url='https://wiki.ros.org/image_view'

pkgname='ros-noetic-image-view'
pkgver='1.17.0'
arch=('i686' 'x86_64' 'aarch64' 'armv7h' 'armv6h')
pkgrel=1
license=('BSD')

ros_makedepends=(
	ros-noetic-std-srvs
	ros-noetic-nodelet
	ros-noetic-dynamic-reconfigure
	ros-noetic-stereo-msgs
	ros-noetic-catkin
	ros-noetic-cv-bridge
	ros-noetic-camera-calibration-parsers
	ros-noetic-message-generation
	ros-noetic-rosconsole
	ros-noetic-roscpp
	ros-noetic-message-filters
	ros-noetic-sensor-msgs
	ros-noetic-image-transport
)

makedepends=(
	'cmake'
	'ros-build-tools'
	${ros_makedepends[@]}
	gtk2
       qt5-base
)

ros_depends=(
	ros-noetic-std-srvs
	ros-noetic-nodelet
	ros-noetic-dynamic-reconfigure
	ros-noetic-cv-bridge
	ros-noetic-camera-calibration-parsers
	ros-noetic-rosconsole
	ros-noetic-roscpp
	ros-noetic-message-filters
	ros-noetic-image-transport
)

depends=(
	${ros_depends[@]}
	gtk2
	gtk3
       qt5-base
)

_commit="69488e6e455d97c2deaf924234aa5f87b83cfda8"
_dir="image_pipeline-${_commit}/image_view"
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros-perception/image_pipeline/archive/${_commit}.tar.gz")
sha256sums=('f833d69491a2b4988bafa1e4d74b539486853ddd9f184506d7e2c61e1b03fa85')

build() {
	# Use ROS environment variables.
	source /usr/share/ros-build-tools/clear-ros-env.sh
	[ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

	# Create the build directory.
	[ -d ${srcdir}/build ] || mkdir ${srcdir}/build
	cd ${srcdir}/build

	# Build the project.
	cmake ${srcdir}/${_dir} \
		-DCATKIN_BUILD_BINARY_PACKAGE=ON \
		-DCMAKE_INSTALL_PREFIX=/opt/ros/noetic \
		-DPYTHON_EXECUTABLE=/usr/bin/python \
		-DSETUPTOOLS_DEB_LAYOUT=OFF
	make
}

package() {
	cd "${srcdir}/build"
	make DESTDIR="${pkgdir}/" install
}
