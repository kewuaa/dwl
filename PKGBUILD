pkgname=dwl
pkgver="0.1.0"
pkgrel=1
arch=("x86_64")
depends=(
    "libinput"
    "wayland"
    "wlroots0.18"
    "libxkbcommon"
    # X11 support
    "libxcb"
    "xorg-xwayland"

    "fcft"
)
makedepends=(
    "gcc"
    "pkgconf"
    "wayland-protocols"
    "tllist"
    "meson"
    "ninja"
)


build() {
    # provide status bar content
    cd ${srcdir}
    [ ! -d slstatus ] && git clone -b dwl https://github.com/kewuaa/slstatus.git
    cd slstatus
    make

    # personal fork for wmenu
    cd ${srcdir}
    [ ! -d wmenu ] && git clone https://github.com/kewuaa/wmenu.git
    cd wmenu
    meson setup build --buildtype=release
    meson compile -C build

    cd ${srcdir}/..
    make
}

package() {
    depends+=(
        # font
        "ttf-firacode-nerd"
        # adjust light
        "brightnessctl"
        # adjust volume
        "wireplumber"
        # default terminal
        "foot"
        # power manager
        "wlopm"
        # screen lock
        "swayidle" "waylock"
        # wallpaper manager
        "swaybg"
        # screen shot
        "slurp" "grim"
        # Day/night gamma adjustments
        "gammastep"
        # clipboard support
        "wl-clipboard"
        # screen share
        "xdg-desktop-portal-gtk" "xdg-desktop-portal-wlr"
        "wob"
    )
    optdepends=(
        "wlr-randr: simple output configuration tool"
        "swayimg: image viewer"
        "mpv: video player"
        "wf-recorder: screen recorder"
        "mako: notification daemon"
        "lf: terminal file manager"
    )
    prefix="/usr"
    man_prefix="/usr/local/man"

    cd ${srcdir}/slstatus
    make DESTDIR="${pkgdir}" PREFIX="${prefix}" MANPREFIX="${man_prefix}" install

    cd ${srcdir}/wmenu
    meson install -C build --destdir="${pkgdir}"

    cd ${srcdir}/..
    make DESTDIR="${pkgdir}" PREFIX="${prefix}" MANPREFIX="${man_prefix}" install
}
