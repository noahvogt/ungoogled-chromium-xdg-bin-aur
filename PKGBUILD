# Maintainer: Noah Vogt (noahvogt) <noah@noahvogt.com>

pkgname=ungoogled-chromium-xdg-bin
pkgver=123.0.6312.86
pkgrel=1
pkgdesc="A lightweight approach to removing Google web service dependency - without creating a useless ~/.pki directory (using pre-releases), (binary version)"
arch=('x86_64')
url="https://github.com/Eloston/ungoogled-chromium"
license=('BSD')
depends=('gtk3' 'nss' 'alsa-lib' 'xdg-utils' 'libxss' 'libcups' 'libgcrypt'
         'ttf-liberation' 'systemd' 'dbus' 'libpulse' 'pciutils' 'libva'
         'wayland' 'desktop-file-utils' 'hicolor-icon-theme')
makedepends=()
optdepends=('pipewire: WebRTC desktop sharing under Wayland'
            'kdialog: support for native dialogs in Plasma'
            'qt5-base: enable Qt5 with --enable-features=AllowQt'
            'org.freedesktop.secrets: password storage backend on GNOME / Xfce'
            'kwallet: support for storing passwords in KWallet on Plasma')
source=(https://github.com/noahvogt/${pkgname%-*}-aur/releases/download/$pkgver-$pkgrel/${pkgname%-*}-$pkgver-$pkgrel-x86_64.pkg.tar.zst
        index.html)
sha256sums=('72d29a5b9664e7d7e60ad8a100cf1eaff84e001b74ed3ae1cc012c792c610b07'
            'a4cdd2b86f32d5302c2792be841ff40d982b19bb58a4e63df9d77f4c706b8665')
provides=('chromium')
conflicts=('chromium')

# Possible replacements are listed in build/linux/unbundle/replace_gn_files.py
# Keys are the names in the above script; values are the dependencies in Arch
declare -gA _system_libs=(
    #[brotli]=brotli
    [dav1d]=dav1d
    [ffmpeg]=ffmpeg
    [flac]=flac
    [fontconfig]=fontconfig
    [freetype]=freetype2
    [harfbuzz-ng]=harfbuzz
    [icu]=icu
    [jsoncpp]=jsoncpp
    #[libaom]=aom
    #[libavif]=libavif
    [libdrm]=
    [libjpeg]=libjpeg
    [libpng]=libpng
    #[libvpx]=libvpx
    [libwebp]=libwebp
    [libxml]=libxml2
    [libxslt]=libxslt
    [opus]=opus
    [re2]=re2
    [snappy]=snappy
    [woff2]=woff2
    [zlib]=minizip
)
_unwanted_bundled_libs=(
    $(printf "%s\n" ${!_system_libs[@]} | sed 's/^libjpeg$/&_turbo/')
)
depends+=(${_system_libs[@]})

package() {
    cp -R "${srcdir}/usr/" "${pkgdir}/usr"

    chown root "$pkgdir/usr/lib/chromium/chrome-sandbox"
    chmod 4755 "$pkgdir/usr/lib/chromium/chrome-sandbox"
}
