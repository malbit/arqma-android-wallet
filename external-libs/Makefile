all: arqma

arqma: toolchain libsodium openssl boost arqma_dl openssl_sysroot
	script/arqma-build.sh

arqma_dl:
	script/arqma-fetch.sh

toolchain:
	script/toolchain-build.sh

openssl: toolchain openssl_dl
	script/openssl-build.sh

openssl_sysroot:
	script/openssl-install.sh

openssl_dl:
	script/openssl-fetch.sh
	script/openssl-patch.sh

boost: toolchain boost_dl
	script/boost-build.sh

boost_dl:
	script/boost-fetch.sh

libsodium: toolchain libsodium_dl
	script/libsodium-build.sh

libsodium_dl:
	script/libsodium-fetch.sh

install: all
	script/install.sh

clean:
	script/clean.sh

distclean: clean
	find arqma     -type f -a ! -name ".gitignore" -a ! -name "wallet2_api.h" -exec rm {} \;
	find boost     -type f -a ! -name ".gitignore" -exec rm {} \;
	find libsodium -type f -a ! -name ".gitignore" -exec rm {} \;
	find openssl   -type f -a ! -name ".gitignore" -exec rm {} \;

archive: libsodium openssl boost arqma
	echo "Packing external-libs"
	tar czfv libsodium openssl boost arqma external-libs.tgz
