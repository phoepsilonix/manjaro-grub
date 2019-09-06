# Based on the file created for Arch Linux by:
# Christian Hesse <mail@eworm.de>
# Tobias Powalowski <tpowa@archlinux.org>
# Ronald van Haren <ronald.archlinux.org>
# Keshav Padram <the.ridikulus.rat.gmail.com>

# Maintainer: Philip Mueller <philm|manjaro|org>
# Maintainer: Guinux <nuxgui|gmail|com>

## "1" to enable IA32-EFI build in Arch x86_64, "0" to disable
_IA32_EFI_IN_ARCH_X64="1"

## "1" to enable EMU build, "0" to disable
_GRUB_EMU_BUILD="1"

_GRUB_INT_VER="2.05"
_GRUB_COMMIT="8f6843ce60b461d630439d07e577074c64511048"
_GRUB_EXTRAS_COMMIT="136763a4cc9ca3a4f59d05b79eede2159d6f441e"
_GNULIB_COMMIT="9ce9be2ef0cb1180e35dfe9dfbbe90d774b374bd"
_UNIFONT_VER="12.1.02"

[[ "${CARCH}" == "x86_64" ]] && _EFI_ARCH="x86_64"
[[ "${CARCH}" == "i686" ]] && _EFI_ARCH="i386"

[[ "${CARCH}" == "x86_64" ]] && _EMU_ARCH="x86_64"
[[ "${CARCH}" == "i686" ]] && _EMU_ARCH="i386"

pkgname='grub'
pkgdesc='GNU GRand Unified Bootloader (2)'
_pkgver=2.04
pkgver=${_pkgver/-/}
pkgrel=3
url='https://www.gnu.org/software/grub/'
arch=('x86_64')
license=('GPL3')
backup=('etc/default/grub'
        'etc/grub.d/40_custom'
        'boot/grub/grub.cfg')
install="${pkgname}.install"
options=('!makeflags')

conflicts=('grub-common' 'grub-bios' 'grub-emu' "grub-efi-${_EFI_ARCH}" 'grub-legacy'
           'grub-fedora' 'grub-quiet-fedora' 'grub-quiet-test' 'grub-quiet')
replaces=('grub-common' 'grub-bios' 'grub-emu' "grub-efi-${_EFI_ARCH}" 'grub-quiet')
provides=('grub-common' 'grub-bios' 'grub-emu' "grub-efi-${_EFI_ARCH}"
          "grub=$pkgver-$pkgrel" "grub-quiet=$pkgver-$pkgrel")

makedepends=('git' 'rsync' 'xz' 'freetype2' 'ttf-dejavu' 'python' 'autogen'
             'texinfo' 'help2man' 'gettext' 'device-mapper' 'fuse2')
depends=('sh' 'xz' 'gettext' 'device-mapper')
optdepends=('freetype2: For grub-mkfont usage'
            'fuse2: For grub-mount usage'
            'dosfstools: For grub-mkrescue FAT FS and EFI support'
            'efibootmgr: For grub-install EFI support'
            'libisoburn: Provides xorriso for generating grub rescue iso using grub-mkrescue'
            'os-prober: To detect other OSes when generating grub.cfg in BIOS systems'
            'mtools: For grub-mkrescue FAT FS support')

if [[ "${_GRUB_EMU_BUILD}" == "1" ]]; then
    makedepends+=('libusbx' 'sdl')
    optdepends+=('libusbx: For grub-emu USB support'
                 'sdl: For grub-emu SDL support')
fi

validpgpkeys=('E53D497F3FA42AD8C9B4D1E835A93B74E82E4209'  # Vladimir 'phcoder' Serbinenko <phcoder@gmail.com>
              '95D2E9AB8740D8046387FD151A09227B1F435A33') # Paul Hardy <unifoundry@unifoundry.com>

source=(#"git+https://git.savannah.gnu.org/git/grub.git#tag=grub-${_pkgver}?signed"
        "git+https://git.savannah.gnu.org/git/grub.git#commit=${_GRUB_COMMIT}"
        "git+https://git.savannah.gnu.org/git/grub-extras.git#commit=${_GRUB_EXTRAS_COMMIT}"
        "git+https://git.savannah.gnu.org/git/gnulib.git#commit=${_GNULIB_COMMIT}"
        "https://ftp.gnu.org/gnu/unifont/unifont-${_UNIFONT_VER}/unifont-${_UNIFONT_VER}.bdf.gz"{,.sig}
        'background.png'
        'grub.default'
        'grub.cfg'
        'update-grub'
        "${pkgname}.hook"
        # Arch patches
        '0001-grub-add-GRUB_COLOR_variables.patch'
        # Manjaro patches
        '0001-grub-manjaro-modifications.patch'
        '0002-grub-export-path.patch'
        '0003-grub-use-efivarfs.patch'
        # Fedora patches
        '0021-Add-support-for-UEFI-operating-systems-returned-by-o.patch'
        #'0123-EFI-console-Do-not-set-text-mode-until-we-actually-n.patch'
        '0124-EFI-console-Add-grub_console_read_key_stroke-helper-.patch'
        '0125-EFI-console-Implement-getkeystatus-support.patch'
        '0126-Make-grub_getkeystatus-helper-funtion-available-ever.patch'
        '0127-Accept-ESC-F8-and-holding-SHIFT-as-user-interrupt-ke.patch'
        '0128-grub-editenv-Add-incr-command-to-increment-integer-v.patch'
        '0129-Add-auto-hide-menu-support.patch'
        '0131-Add-grub-set-bootflag-utility.patch'
        '0132-docs-Add-grub-boot-indeterminate.service-example.patch'
        '0173-Don-t-assume-that-boot-commands-will-only-return-on-.patch'
        # Ubuntu patches
        '0001-grub-maybe_quiet.patch'
        '0002-grub-gettext_quiet.patch')

sha256sums=('SKIP'
            'SKIP'
            'SKIP'
            '04d652be1e28a6d464965c75c71ac84633085cd0960c2687466651c34c94bd89'
            'SKIP'
            '01264c247283b7bbdef65d7646541c022440ddaf54f8eaf5aeb3a02eb98b4dd8'
            '8eaecef8f417de916b5612cb66942bd826c9f84295e561d81f5220fe436ac69c'
            '7fc95d49c0febe98a76e56b606a280565cb736580adecf163bc6b5aca8e7cbd8'
            '467b0101154076fee99d9574a5fb6b772a3923cc200a1f4ca08fe17be8d68111'
            '1488d7f3924bd7385a222e3e9685cdb1ecb39f3d6f882da6b5907b898f5b8f08'
            'a5198267ceb04dceb6d2ea7800281a42b3f91fd02da55d2cc9ea20d47273ca29'
            'cf00c96aee37e0a73c1ab6ed6ccfe74fa2b2859f55cd315a4caa6c880ce7aeba'
            '63c611189a60d68c6ae094f2ced91ac576b3921b7fd2e75a551c2dc6baefc35e'
            '20b2b6e7f501596b5cce6ffa05906980427f760c03d308d0e045cf2ecf47bb0e'
            '9ed7986ed7c8681f5e83e5d37ad9ef557369d786270c3440d7e1809f9f0f8c14'
            'd49236776e53a7ffdc5845205c94b3276b116d1f476bbccadcea1aa0a3f57b38'
            'b218ade00670bad6095e0284b17d85f6f92900d5ebd156a2ec1cbc5ccad92fcb'
            '3803a487dce21f29bff829c391651705a9253431af5b20ca4ed9fe8f7ea7db6d'
            '8e00b55925e5d9ba67b4949c75c0c33ae1c7ea9644780a79bf1e0f4dbaac06ff'
            'ff95c6866476b0bc574cf89f57acc22a6e277d0f0e55d9654dbfe27798622576'
            '46ee7f04e14cf6a311258f34b937697d9fe75c5cee6d9d354911a989153a4498'
            '00e04c665072d0b03c3b9ab15bac274edff9c2f1113e70cd60258f328ab961ea'
            'd858707ce7912ba479a3fb0de9a1cc858b92c787500073cc7af90186562a8731'
            '09b247abfbbeef8299fc9ddefd7e8913e77c2179c4507c08800ce067169da430'
            '9a0ef2efe572f3e206d8f145cb9a00098f44d41eaf396110810f6f79885bd5de'
            '39d7843dfe1e10ead912a81be370813b8621794a7967b3cc5e4d4188b5bf7264')

_backports=(      
)

_configure_options=(
	FREETYPE="pkg-config freetype2"
	BUILD_FREETYPE="pkg-config freetype2"
	--enable-mm-debug
	--enable-nls
	--enable-device-mapper
	--enable-cache-stats
	--enable-grub-mkfont
	--enable-grub-mount
	--prefix="/usr"
	--bindir="/usr/bin"
	--sbindir="/usr/bin"
	--mandir="/usr/share/man"
	--infodir="/usr/share/info"
	--datarootdir="/usr/share"
	--sysconfdir="/etc"
	--program-prefix=""
	--with-bootdir="/boot"
	--with-grubdir="grub"
	--enable-quiet-boot \
	--enable-quick-boot \
	--disable-silent-rules
	--disable-werror
)

prepare() {
	cd "${srcdir}/grub/"

	echo "Apply backports..."
	local _c
	for _c in "${_backports[@]}"; do
		git log --oneline -1 "${_c}"
		git cherry-pick -n "${_c}"
	done

	msg "Patch to enable GRUB_COLOR_* variables in grub-mkconfig"
	## Based on http://lists.gnu.org/archive/html/grub-devel/2012-02/msg00021.html
	patch -Np1 -i "${srcdir}/0001-grub-add-GRUB_COLOR_variables.patch"
	echo

	msg "Patch to include Manjaro Linux Modifications"
	patch -Np1 -i "${srcdir}/0001-grub-manjaro-modifications.patch"
	echo

	msg "Patch to export $PATH"
        ## https://github.com/manjaro/manjaro-settings-manager/issues/130
	patch -Np1 -i "${srcdir}/0002-grub-export-path.patch"
	echo

	msg "Use efivarfs modules"
        ## https://github.com/calamares/calamares/issues/918
	patch -Np1 -i "${srcdir}/0003-grub-use-efivarfs.patch"
	echo


	msg "Add Fedora patches"
        #patch -Np1 -i "${srcdir}/0021-Add-support-for-UEFI-operating-systems-returned-by-o.patch"
	# Disable this patch for now. Creates black screens on some Lenovo laptops   
        #patch -Np1 -i "${srcdir}/0123-EFI-console-Do-not-set-text-mode-until-we-actually-n.patch"
	patch -Np1 -i "${srcdir}/0124-EFI-console-Add-grub_console_read_key_stroke-helper-.patch"
	patch -Np1 -i "${srcdir}/0125-EFI-console-Implement-getkeystatus-support.patch"
	patch -Np1 -i "${srcdir}/0126-Make-grub_getkeystatus-helper-funtion-available-ever.patch"
	patch -Np1 -i "${srcdir}/0127-Accept-ESC-F8-and-holding-SHIFT-as-user-interrupt-ke.patch"
	patch -Np1 -i "${srcdir}/0128-grub-editenv-Add-incr-command-to-increment-integer-v.patch"
	#patch -Np1 -i "${srcdir}/0129-Add-auto-hide-menu-support.patch"
	#patch -Np1 -i "${srcdir}/0131-Add-grub-set-bootflag-utility.patch"
	patch -Np1 -i "${srcdir}/0132-docs-Add-grub-boot-indeterminate.service-example.patch"
	patch -Np1 -i "${srcdir}/0173-Don-t-assume-that-boot-commands-will-only-return-on-.patch"

	msg "Add Ubuntu patches"
	patch -Np1 -i "${srcdir}/0001-grub-maybe_quiet.patch"
	patch -Np1 -i "${srcdir}/0002-grub-gettext_quiet.patch"

        # delete line due man h2m
        sed -i -e '1369d' "Makefile.util.def"
	echo

	echo "Fix DejaVuSans.ttf location so that grub-mkfont can create *.pf2 files for starfield theme..."
	sed 's|/usr/share/fonts/dejavu|/usr/share/fonts/dejavu /usr/share/fonts/TTF|g' -i "configure.ac"

	echo "Fix mkinitcpio 'rw' FS#36275..."
	sed 's| ro | rw |g' -i "util/grub.d/10_linux.in"

	echo "Fix OS naming FS#33393..."
	sed 's|GNU/Linux|Linux|' -i "util/grub.d/10_linux.in"

	msg "Bump Version to ${pkgver}~manjaro"
	sed -i -e "s|${_GRUB_INT_VER}|${pkgver}~manjaro|g" "configure.ac"

	echo "Pull in latest language files..."
	./linguas.sh

	echo "Remove not working langs which need LC_ALL=C.UTF-8..."
	sed -e 's#en@cyrillic en@greek##g' -i "po/LINGUAS"

	echo "Avoid problem with unifont during compile of grub..."
	# http://savannah.gnu.org/bugs/?40330 and https://bugs.archlinux.org/task/37847
	gzip -cd "${srcdir}/unifont-${_UNIFONT_VER}.bdf.gz" > "unifont.bdf"

	echo "Run bootstrap..."
	./bootstrap \
		--gnulib-srcdir="${srcdir}/gnulib/" \
		--no-git
}

_build_grub-common_and_bios() {
	echo "Set ARCH dependent variables for bios build..."
	if [[ "${CARCH}" == 'x86_64' ]]; then
		_EFIEMU="--enable-efiemu"
	else
		_EFIEMU="--disable-efiemu"
	fi

	echo "Copy the source for building the bios part..."
	cp -r "${srcdir}/grub/" "${srcdir}/grub-bios/"
	cd "${srcdir}/grub-bios/"

	echo "Add the grub-extra sources for bios build..."
	install -d "${srcdir}/grub-bios/grub-extras"
	cp -r "${srcdir}/grub-extras/915resolution" \
		"${srcdir}/grub-bios/grub-extras/915resolution"
	export GRUB_CONTRIB="${srcdir}/grub-bios/grub-extras/"

	echo "Unset all compiler FLAGS for bios build..."
	unset CFLAGS
	unset CPPFLAGS
	unset CXXFLAGS
	unset LDFLAGS
	unset MAKEFLAGS

	echo "Run ./configure for bios build..."
	./configure \
		--with-platform="pc" \
		--target="i386" \
		"${_EFIEMU}" \
		--enable-boot-time \
		"${_configure_options[@]}"

	echo "Run make for bios build..."
	make
}

_build_grub-efi() {
	echo "Copy the source for building the ${_EFI_ARCH} efi part..."
	cp -r "${srcdir}/grub/" "${srcdir}/grub-efi-${_EFI_ARCH}/"
	cd "${srcdir}/grub-efi-${_EFI_ARCH}/"

	echo "Unset all compiler FLAGS for ${_EFI_ARCH} efi build..."
	unset CFLAGS
	unset CPPFLAGS
	unset CXXFLAGS
	unset LDFLAGS
	unset MAKEFLAGS

	echo "Run ./configure for ${_EFI_ARCH} efi build..."
	./configure \
		--with-platform="efi" \
		--target="${_EFI_ARCH}" \
		--disable-efiemu \
		--enable-boot-time \
		"${_configure_options[@]}"

	echo "Run make for ${_EFI_ARCH} efi build..."
	make
}

_build_grub-emu() {
	echo "Copy the source for building the emu part..."
	cp -r "${srcdir}/grub/" "${srcdir}/grub-emu/"
	cd "${srcdir}/grub-emu/"

	echo "Unset all compiler FLAGS for emu build..."
	unset CFLAGS
	unset CPPFLAGS
	unset CXXFLAGS
	unset LDFLAGS
	unset MAKEFLAGS

	echo "Run ./configure for emu build..."
	./configure \
		--with-platform="emu" \
		--target="${_EMU_ARCH}" \
		--enable-grub-emu-usb=no \
		--enable-grub-emu-sdl=no \
		--disable-grub-emu-pci \
		"${_configure_options[@]}"

	echo "Run make for emu build..."
	make
}

build() {
	cd "${srcdir}/grub/"

	echo "Build grub bios stuff..."
	_build_grub-common_and_bios

	echo "Build grub ${_EFI_ARCH} efi stuff..."
	_build_grub-efi

	if [[ "${CARCH}" == "x86_64" ]] && [[ "${_IA32_EFI_IN_ARCH_X64}" == "1" ]]; then
		echo "Build grub i386 efi stuff..."
		_EFI_ARCH="i386" _build_grub-efi
	fi

	if [[ "${_GRUB_EMU_BUILD}" == "1" ]]; then
		echo "Build grub emu stuff..."
		_build_grub-emu
	fi
}

_package_grub-common_and_bios() {
	cd "${srcdir}/grub-bios/"

	echo "Run make install for bios build..."
	make DESTDIR="${pkgdir}/" bashcompletiondir="/usr/share/bash-completion/completions" install

	echo "Remove gdb debugging related files for bios build..."
	rm -f "${pkgdir}/usr/lib/grub/i386-pc"/*.module || true
	rm -f "${pkgdir}/usr/lib/grub/i386-pc"/*.image || true
	rm -f "${pkgdir}/usr/lib/grub/i386-pc"/{kernel.exec,gdb_grub,gmodule.pl} || true

	echo "Install /etc/default/grub (used by grub-mkconfig)..."
	install -D -m0644 "${srcdir}/grub.default" "${pkgdir}/etc/default/grub"

	msg "Install grub.cfg for backup array"
	install -D -m0644 "${srcdir}/grub.cfg" "${pkgdir}/boot/grub/grub.cfg"

	msg "Install update-grub"
	install -Dm755 "${srcdir}/update-grub" "${pkgdir}/usr/bin/update-grub"

	msg "Install grub background"
	install -Dm644 "${srcdir}/background.png" "${pkgdir}/usr/share/grub/background.png"	
}

_package_grub-efi() {
	cd "${srcdir}/grub-efi-${_EFI_ARCH}/"

	echo "Run make install for ${_EFI_ARCH} efi build..."
	make DESTDIR="${pkgdir}/" bashcompletiondir="/usr/share/bash-completion/completions" install

	echo "Remove gdb debugging related files for ${_EFI_ARCH} efi build..."
	rm -f "${pkgdir}/usr/lib/grub/${_EFI_ARCH}-efi"/*.module || true
	rm -f "${pkgdir}/usr/lib/grub/${_EFI_ARCH}-efi"/*.image || true
	rm -f "${pkgdir}/usr/lib/grub/${_EFI_ARCH}-efi"/{kernel.exec,gdb_grub,gmodule.pl} || true
}

_package_grub-emu() {
	cd "${srcdir}/grub-emu/"

	echo "Run make install for emu build..."
	make DESTDIR="${pkgdir}/" bashcompletiondir="/usr/share/bash-completion/completions" install

	echo "Remove gdb debugging related files for emu build..."
	rm -f "${pkgdir}/usr/lib/grub/${_EMU_ARCH}-emu"/*.module || true
	rm -f "${pkgdir}/usr/lib/grub/${_EMU_ARCH}-emu"/*.image || true
	rm -f "${pkgdir}/usr/lib/grub/${_EMU_ARCH}-emu"/{kernel.exec,gdb_grub,gmodule.pl} || true
}

package() {
	cd "${srcdir}/grub/"

	echo "Package grub ${_EFI_ARCH} efi stuff..."
	_package_grub-efi

	if [[ "${CARCH}" == "x86_64" ]] && [[ "${_IA32_EFI_IN_ARCH_X64}" == "1" ]]; then
		echo "Package grub i386 efi stuff..."
		_EFI_ARCH="i386" _package_grub-efi
	fi

	if [[ "${_GRUB_EMU_BUILD}" == "1" ]]; then
		echo "Package grub emu stuff..."
		_package_grub-emu
	fi

	echo "Package grub bios stuff..."
	_package_grub-common_and_bios

	install -D -m644 "${srcdir}/${pkgname}.hook" "${pkgdir}/usr/share/libalpm/hooks/99-${pkgname}.hook"

	# install example files
#	mkdir -p "${pkgdir}/usr/lib/systemd/user/timers.target.wants"
#	install -D -m644 "${srcdir}/grub/docs/grub-boot-success.timer" "${pkgdir}/usr/lib/systemd/user/grub-boot-success.timer"
#	install -D -m644 "${srcdir}/grub/docs/grub-boot-success.service" "${pkgdir}/usr/lib/systemd/user/grub-boot-success.service"
#	ln -sfv '../grub-boot-success.timer' "${pkgdir}/usr/lib/systemd/user/timers.target.wants/grub-boot-success.timer"
#	chmod +s "${pkgdir}/usr/bin/grub-set-bootflag"

#	mkdir -p "${pkgdir}/usr/lib/systemd/system/sysinit.target.wants/"
#	install -D -m644 "${srcdir}/grub/docs/grub-boot-indeterminate.service" "${pkgdir}/usr/lib/systemd/system/grub-boot-indeterminate.service"
#	ln -sfv '../grub-boot-indeterminate.service' "${pkgdir}/usr/lib/systemd/system/sysinit.target.wants/grub-boot-indeterminate.service"
}
