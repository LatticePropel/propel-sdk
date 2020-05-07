#how to build openocd?
git clone https://github.com/SpinalHDL/openocd_riscv.git
cd openocd_riscv
git checkout 486df528b0e8624b4a09ec224d9dfef383e330a1
git format-patch HEAD^  //generate a patch 0001-Fixed-build-issue-under-MinGW-cross-compling.patch
git checkout 0ace94f73697b8c9970700716799a4df9bcb62b3
./bootstrap
git submodule init
git submodule update
patch -p1 < 0001-Fixed-build-issue-under-MinGW-cross-compling.patch --verbose
patch -p1 < 'PATH'/0001-lattice-driver-patch.patch --verbose
./configure --host=x86_64-w64-mingw32 PKG_CONFIG_LIBDIR="/usr/x86_64-w64-mingw32/lib/pkgconfig:/usr/x86_64-w64-mingw32/share/pkgconfig" CFLAGS="-Wno-pointer-sign -Wno-sign-compare"
make