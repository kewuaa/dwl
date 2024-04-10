pkgname=dwl
pkgver="0.1.0"
pkgrel=1
arch=("x86_64")
depends=(
    "libinput"
    "wayland"
    "wlroots"
    "libxkbcommon"
    # X11 support
    "libxcb"
    "xorg-xwayland"

    "fcft"
    "libpng"
    "libjpeg"
)
makedepends=(
    "gcc"
    "meson"
    "ninja"
    "pkgconf"
    "wayland-protocols"
    "tllist"
)


build() {
    cd ${srcdir}/..
    make
}

package() {
    depends+=(
        # provide status bar content
        "slstatus"
        # font
        "ttf-firacode-nerd"
        # adjust light
        "brightnessctl"
        # adjust volume
        "pamixer"
        # default terminal
        "foot"
        # screen lock
        "swayidle"
        "swaylock-effects"
        # menu
        "bemenu-wayland"
        # wallpaper manager
        "wbg"
        # Day/night gamma adjustments
        "wlsunset"
    )

    cd ${srcdir}/..
    make DESTDIR="${pkgdir}" PREFIX="/usr" MANPREFIX="/usr/local/man" install
}
