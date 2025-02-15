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
)
makedepends=(
    "gcc"
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
        "slstatus_wayland"
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
        "wayidle" "waylock"
        # menu
        "wmenu-git"
        # wallpaper manager
        "wbg"
        # screen shot
        "slurp" "grim"
        # Day/night gamma adjustments
        "wlsunset"
        # clipboard support
        "wl-clipboard"
        # screen share
        "xdg-desktop-portal-gtk" "xdg-desktop-portal-wlr"
    )
    optdepends=(
        "wlr-randr: outputs configure"
        "swayimg: image viewer"
        "mpv: video player"
        "wf-recorder: screen recorder"
        "mako: notification daemon"
    )

    cd ${srcdir}/..
    make DESTDIR="${pkgdir}" PREFIX="/usr" MANPREFIX="/usr/local/man" install
    install -Dm644 dwl-portals.conf ${pkgdir}/usr/share/xdg-desktop-portal/dwl-portals.conf
}
