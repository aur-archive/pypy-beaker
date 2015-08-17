pkgbase='pypy-beaker'
pkgname='pypy-beaker'
pkgname=('pypy3-beaker' 'pypy-beaker')
pkgver=1.6.4
pkgrel=3
arch=('any')
license=('custom')
pkgdesc="Caching and sessions WSGI middleware for use with web applications and stand-alone Python scripts and applications, pypy version."
url="http://beaker.groovie.org/"
makedepends=('pypy-setuptools' 'pypy3-setuptools' 'sqlite')
source=("http://cheeseshop.python.org/packages/source/B/Beaker/Beaker-${pkgver}.tar.gz")
md5sums=('c2e102870ed4c53104dec48ceadf8e9d')

build() {
    cp -r Beaker-${pkgver} python2-Beaker-${pkgver}

    cd "${srcdir}/Beaker-${pkgver}"
    sed -i "s#/usr/bin/python#/usr/bin/pypy3#" beaker/crypto/pbkdf2.py
    pypy3 setup.py build

    cd "${srcdir}/python2-Beaker-${pkgver}"
    sed -i "s#/usr/bin/python#/usr/bin/pypy#" beaker/crypto/pbkdf2.py
    pypy setup.py build
}

package_pypy3-beaker() {
    depends=("pypy3>=2.3" "pypy3<=2.4")

    cd "${srcdir}/Beaker-${pkgver}"
    # pypy3 setup.py install --root="${pkgdir}" --optimize=1 \
    #   --install-lib=/opt/pypy3/lib/python3.2/site-packages
    pypy3 setup.py install --root="${pkgdir}" --optimize=1
    install -D -m644 LICENSE "${pkgdir}/usr/share/licenses/pypy3-beaker/LICENSE"
}

package_pypy-beaker() {
    depends=("pypy>=2.3" "pypy<=2.4")

    cd "${srcdir}/python2-Beaker-${pkgver}"
    pypy setup.py install --root="${pkgdir}" --optimize=1
    install -D -m644 LICENSE "${pkgdir}/usr/share/licenses/pypy-beaker/LICENSE"
}
