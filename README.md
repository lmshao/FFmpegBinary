# FFmpeg Compilation Guide for Linux

## Third-party Software Complilation

### nasm

```sh
wget https://www.nasm.us/pub/nasm/releasebuilds/2.15.05/nasm-2.15.05.tar.xz
tar Jxvf nasm-2.15.05.tar.xz
pushd nasm-2.15.05
./configure
make && make install
popd
```

### libx264

```sh
wget https://code.videolan.org/videolan/x264/-/archive/master/x264-master.tar.bz2
tar jxvf x264-master.tar.bz2
pushd x264-master
./configure --enable-shared
make && make install
popd
```

### libx265

```sh
hg clone http://hg.videolan.org/x265
pushd x265/build/linux/
./make-Makefiles.bash
make && make install
popd
```

### libfdk-aac

```sh
wget -O fdk-aac-2.0.1.tar.gz https://sourceforge.net/projects/opencore-amr/files/fdk-aac/fdk-aac-2.0.1.tar.gz/download
tar zxvf fdk-aac-2.0.1.tar.gz
pushd fdk-aac-2.0.1
./configure
make && make install
popd
```

### libmp3lame

```sh
wget -O lame-3.100.tar.gz https://sourceforge.net/projects/lame/files/lame/3.100/lame-3.100.tar.gz/download
pushd lame-3.100
./configure
make && make install
popd
```

### libvpx

```sh
wget https://github.com/webmproject/libvpx/archive/v1.10.0/libvpx-1.10.0.tar.gz
tar zxvf libvpx-1.10.0.tar.gz 
pushd libvpx-1.10.0
sed -i 's/cp -p/cp/' build/make/Makefile
mkdir libvpx-build && cd libvpx-build
../configure --enable-shared --disable-static
make && make install
popd
```

### libopus

```sh
wget https://archive.mozilla.org/pub/opus/opus-1.3.1.tar.gz
tar zxvf opus-1.3.1.tar.gz
pushd opus-1.3.1
./configure --enable-shared --disable-static
make && make install
popd
```

## FFmpeg Complilation

```sh
wget https://www.ffmpeg.org/releases/ffmpeg-4.4.tar.bz2
tar jxvf ffmpeg-4.4.tar.bz2
pushd ffmpeg-4.4
export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig/
./configure --prefix=./ffmpeg-4.4-$(date +%Y%m%d) --enable-shared --disable-static --enable-gpl --enable-nonfree --enable-libx264 --enable-libx265 --enable-libfdk-aac --enable-libmp3lame --enable-libvpx --enable-libopus
make && make install
popd
```
