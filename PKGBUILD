# Maintainer: Paraworker <paraworker@gmail.com>

pkgname=mutter-artifact
pkgver=41.0
pkgrel=1
pkgdesc="A window manager for GNOME (with MR1441)"
url="https://gitlab.gnome.org/GNOME/mutter"
arch=(x86_64)
license=(GPL)
depends=(dconf gobject-introspection-runtime gsettings-desktop-schemas
         libcanberra startup-notification zenity libsm gnome-desktop upower
         libxkbcommon-x11 gnome-settings-daemon libgudev libinput pipewire
         xorg-xwayland graphene libxkbfile)
makedepends=(gobject-introspection git egl-wayland meson xorg-server
             wayland-protocols)
checkdepends=(xorg-server-xvfb wireplumber python-dbusmock)
provides=(mutter)
conflicts=(mutter)
groups=(gnome)
source=("$pkgname::git+https://gitlab.gnome.org/GNOME/mutter.git"
        "https://gitlab.gnome.org/GNOME/mutter/-/merge_requests/1441.patch")

sha256sums=('SKIP'
            'SKIP')

pkgver() {
  cd $pkgname
  git describe --tags | sed 's/-/+/g'
}

prepare() {
  cd "$srcdir/$pkgname"
  patch -p1 < "$srcdir/1441.patch"
}

build() {
  arch-meson $pkgname build \
    -D egl_device=true \
    -D wayland_eglstream=true \
    -D installed_tests=false \
    -D profiler=false
  meson compile -C build
}

package() {
  meson install -C build --destdir "$pkgdir"
}
