# Maintainer: Kuredant <kuredant[at]gmail[dot]com>
# Contributor: Loren <smallphrosty[at]gmail[dot]com>

pkgname=chocolate-castle
pkgver=1.1
pkgrel=1
pkgdesc="[Humble Bundle] A tricky sliding block puzzle game"
arch=('i686' 'x86_64')
url='http://www.lexaloffle.com/choc.php'
groups=('humblevoxatronbundle' 'humblebundle')
license=('custom: "commercial"')

[ "${CARCH}" = "i686" ]   && depends=('libgl' 'sdl')
[ "${CARCH}" = "x86_64" ] && depends=('lib32-libgl' 'lib32-sdl')

_gamepkg="${pkgname}_${pkgver}_i386.tar.gz"
source=("${_gamepkg}::https://www.humblebundle.com/login"
        "${_gamepkg}::http://www.humblebundle.com/downloads?key=${_humblevoxatronkey}"
        "${pkgname}.desktop")
md5sums=('199bcc788a063fea8015441833c8de67'
         '199bcc788a063fea8015441833c8de67'
         '7f70eb8346a93bb158055fea19dd5e5d')

_char=\'
DLAGENTS=('https::/bin/echo %o > /tmp/arch && sed -i "s/.part//" /tmp/arch &&
                 /usr/bin/curl -s --cookie-jar /tmp/cjar --output /dev/null %u && cp /tmp/cjar ./ &&
                 /usr/bin/curl -sL --cookie /tmp/cjar --cookie-jar /tmp/cjar --data "username=$_humbleemail" --data "password=$_humblepassword" %u |
                 grep -f /tmp/arch |grep -o -E "data-web=[^ ]+"| sed -e "s/data-web=\([^ ]*\)/\1/" > /tmp/url &&
                 sed -i "s/$_char//g" /tmp/url &&
                 /usr/bin/curl --cookie /tmp/cjar --cookie-jar /tmp/cjar -fLC -  --retry 3 --retry-delay 3 -o %o "$(</tmp/url)" &&
                 rm -f /tmp/{arch,url} || return 0'
          "http::/bin/echo %o > /tmp/arch && sed -i \"s/.part//\" /tmp/arch &&
                /usr/bin/curl -sL %u |grep -f /tmp/arch | grep -o -E \"data-web=[^ ]+\" | sed -e \"s/data-web='\(.*\)'/url = \1/\" > /tmp/url &&
                /usr/bin/curl -fLC -  --retry 3 --retry-delay 3 -o %o -K /tmp/url && rm /tmp/{url,arch}")

if [[ ! -f ${SRCDEST}/${source[0]%%:*} ]]; then
    if [[ -z ${_humbleemail} || -z ${_humblepassword} ]]; then
        if [[ -z ${_humblevoxatronkey} ]]; then
            msg "You need a full copy of this game in order to install it."
            echo
            msg "If you have bound your email and password to your account, "
            msg "please export the values _humbleemail and _humblepassword so"
            msg "that you can be logged in to download the game."
            echo
            msg "If you have not bound the key to an email, "
            msg "please export _humblevoxatronkey in your .bashrc"
            return 1
        fi
    fi
fi

package() {
   cd "${srcdir}"

   install -D -m 755 "${pkgname}/choc"                 "${pkgdir}/opt/${pkgname}/choc"
   install -D -m 644 "${pkgname}/choc.dat"             "${pkgdir}/opt/${pkgname}/choc.dat"
   install -D -m 644 "${pkgname}/chocolate-castle.txt" "${pkgdir}/opt/${pkgname}/chocolate-castle.txt"
   install -D -m 644 "${pkgname}/license.txt"          "${pkgdir}/opt/${pkgname}/licence.txt"

   install -D -m 644 "${pkgname}.desktop"              "${pkgdir}/usr/share/applications/${pkgname}.desktop"
   install -D -m 644 "${pkgname}/lexaloffle-choc.png"  "${pkgdir}/usr/share/pixmaps/${pkgname}.png"
   install -D -m 644 "${pkgname}/license.txt"          "${pkgdir}/usr/share/licenses/${pkgname}/LICENCE"

   install -d -m 755 "${pkgdir}/usr/bin"
   ln -s "/opt/${pkgname}/choc" "${pkgdir}/usr/bin/${pkgname}"
}

# vim:set ts=2 sw=2 et: