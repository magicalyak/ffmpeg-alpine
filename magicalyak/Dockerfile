FROM alpine:3.14 as ffmpeg-deps

RUN set -eux && \
	apk upgrade --update && \
	apk add --no-cache --update \
		autoconf \
		automake \
		alpine-sdk \
		ca-certificates \
		cmake \
		coreutils \
		cunit-dev \
		curl \
		dos2unix \
		libtool \
		linux-headers \
		nasm \
		python3 \
		tzdata \
		unzip \
		wget \
		yasm && \
	\
	# cleaning
	rm -rf /tmp/* /var/tmp/*

WORKDIR /build

FROM ffmpeg-deps AS ffmpeg-build

ENV LD_LIBRARY_PATH=/opt/intel/mediasdk/lib64:/usr/local/lib64:/usr/local/lib:/usr/lib:/lib
ENV PKG_CONFIG_PATH=/opt/intel/mediasdk/lib64/pkgconfig:/usr/local/lib64/pkgconfig:/usr/local/lib/pkgconfig:/usr/lib/pkgconfig:/lib/pkgconfig
ENV SRC=/usr/local
ENV PREFIX=/usr/local

# ENV         FFMPEG_VERSION=4.4 \
#             AOM_VERSION=v1.0.0 \
#             AVISYNTHPLUS_VERSION=3.6.1 \
#             FDKAAC_VERSION=0.1.5 \
#             FONTCONFIG_VERSION=2.12.4 \
#             FREETYPE_VERSION=2.10.4 \
#             FRIBIDI_VERSION=0.19.7 \
#             KVAZAAR_VERSION=2.0.0 \
#             LAME_VERSION=3.100 \
#             LIBASS_VERSION=0.13.7 \
#             LIBPTHREAD_STUBS_VERSION=0.4 \
#             LIBVIDSTAB_VERSION=1.1.0 \
#             LIBXCB_VERSION=1.13.1 \
#             XCBPROTO_VERSION=1.13 \
#             OGG_VERSION=1.3.2 \
#             OPENCOREAMR_VERSION=0.1.5 \
#             OPUS_VERSION=1.2 \
#             OPENJPEG_VERSION=2.1.2 \
#             THEORA_VERSION=1.1.1 \
#             VORBIS_VERSION=1.3.5 \
#             VPX_VERSION=1.8.0 \
#             WEBP_VERSION=1.0.2 \
#             X264_VERSION=20170226-2245-stable \
#             X265_VERSION=3.4 \
#             XAU_VERSION=1.0.9 \
#             XORG_MACROS_VERSION=1.19.2 \
#             XPROTO_VERSION=7.0.31 \
#             XVID_VERSION=1.3.4 \
#             LIBXML2_VERSION=2.9.10 \
#             LIBBLURAY_VERSION=1.1.2 \
#             LIBBS2B_VERSION=3.1.0 \
#             LIBZMQ_VERSION=4.3.4 \
#             LIBSRT_VERSION=1.4.1 \
#             LIBARIBB24_VERSION=1.0.3 \
#             LIBPNG_VERSION=1.6.9 \
#             LIBVMAF_VERSION=2.1.1 \
#             LIBMFX_VERSION=20.1.1 \
#             LIBOPENMPT_VERSION=0.5.0 \
#             LIBMYSOFA_VERSION=1.1 \
#             TWOLAME_VERSION=0.4.0 \
#             CODEC2_VERSION=0.9.2

# ARG         FREETYPE_SHA256SUM="5eab795ebb23ac77001cfb68b7d4d50b5d6c7469247b0b01b2c953269f658dac freetype-2.10.4.tar.gz"
# ARG         FRIBIDI_SHA256SUM="3fc96fa9473bd31dcb5500bdf1aa78b337ba13eb8c301e7c28923fea982453a8 0.19.7.tar.gz"
# ARG         LIBASS_SHA256SUM="8fadf294bf701300d4605e6f1d92929304187fca4b8d8a47889315526adbafd7 0.13.7.tar.gz"
# ARG         LIBVIDSTAB_SHA256SUM="14d2a053e56edad4f397be0cb3ef8eb1ec3150404ce99a426c4eb641861dc0bb v1.1.0.tar.gz"
# ARG         OGG_SHA256SUM="e19ee34711d7af328cb26287f4137e70630e7261b17cbe3cd41011d73a654692 libogg-1.3.2.tar.gz"
# ARG         OPUS_SHA256SUM="77db45a87b51578fbc49555ef1b10926179861d854eb2613207dc79d9ec0a9a9 opus-1.2.tar.gz"
# ARG         THEORA_SHA256SUM="40952956c47811928d1e7922cda3bc1f427eb75680c3c37249c91e949054916b libtheora-1.1.1.tar.gz"
# ARG         VORBIS_SHA256SUM="6efbcecdd3e5dfbf090341b485da9d176eb250d893e3eb378c428a2db38301ce libvorbis-1.3.5.tar.gz"
# ARG         XVID_SHA256SUM="4e9fd62728885855bc5007fe1be58df42e5e274497591fec37249e1052ae316f xvidcore-1.3.4.tar.gz"
# ARG         LIBXML2_SHA256SUM="f07dab13bf42d2b8db80620cce7419b3b87827cc937c8bb20fe13b8571ee9501  libxml2-v2.9.10.tar.gz"
# ARG         LIBBLURAY_SHA256SUM="a3dd452239b100dc9da0d01b30e1692693e2a332a7d29917bf84bb10ea7c0b42 libbluray-1.1.2.tar.bz2"
# ARG         LIBZMQ_SHA256SUM="0ff5a531c9ffaf0dfdc7dc78d13d1383088f454896d252934c429b2554d10559 v4.3.4.tar.gz"
# ARG         LIBARIBB24_SHA256SUM="f61560738926e57f9173510389634d8c06cabedfa857db4b28fb7704707ff128 v1.0.3.tar.gz"
# ARG         LIBVMAF_SHA256SUM="e7fc00ae1322a7eccfcf6d4f1cdf9c67eec8058709887c8c6c3795c617326f77 v2.1.1.tar.gz"

RUN apk add --no-cache --update-cache \
	aom-dev \
	chromaprint-dev \
	cunit-dev \
	fdk-aac-dev \
	ffmpeg-libs \
	ffmpeg-dev \
	flite-dev \
	fontconfig-dev \
	freetype-dev \
	frei0r-plugins-dev \
	fribidi-dev \
	gsm-dev \
	jack-dev \
	lame-dev \
	libass-dev \
	libbluray-dev \
	libcaca-dev \
	libcdio-dev \
	libcdio-paranoia-dev \
	libdc1394-dev \
	libdrm-dev \
	libogg-dev \
	libpng-dev \
	librsvg-dev \
	libsndfile-dev \
	libssh-dev \
	libtheora-dev \
	libvorbis-dev \
	libvpx-dev \
	libwebp-dev \
	libxau-dev \
	libxcb-dev \
	libxml2-dev \
	mesa-dev \
	mpg123-dev \
	openjpeg-dev \
	openal-soft-dev \
	openssl-dev \
	opus-dev \
	pulseaudio-dev \
	sdl2-dev \
	snappy-dev \
	soxr-dev \
	speex-dev \
	util-linux-dev \
	wavpack-dev \
	x264-dev \
	x265-dev \
	xvidcore-dev \
	zeromq-dev \
	\
	libva-dev \
	libva-intel-driver \
	libvdpau-dev \
	mesa-va-gallium \
	mesa-vdpau-gallium

RUN echo http://dl-2.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories
RUN apk add --no-cache --update-cache \
	libgme-dev \
	lilv-dev \
	rubberband-dev \
	shine \
	vidstab-dev \
	\
	libva-vdpau-driver

RUN echo http://dl-2.alpinelinux.org/alpine/edge/community >> /etc/apk/repositories
RUN apk add --no-cache --update-cache \
	ladspa-dev \
#	libiec61883-dev
	\
	intel-media-driver


# AviSynth+ https://github.com/AviSynth/AviSynthPlus
WORKDIR /tmp/AviSynthPlus
RUN \
	curl -fsSL https://github.com/AviSynth/AviSynthPlus/archive/v3.6.1.tar.gz | \
		tar -xz --strip-components=1 && \
	mkdir avisynth-build && cd avisynth-build && \
	cmake -DCMAKE_BUILD_TYPE=Release ../ -DHEADERS_ONLY:bool=on && \
	make -j $(nproc) install

## bs2b http://bs2b.sourceforge.net/
WORKDIR /tmp/bs2b
RUN \
	curl -fsSL https://downloads.sourceforge.net/project/bs2b/libbs2b/3.1.0/libbs2b-3.1.0.tar.gz | \
		tar -xz --strip-components=1 && \
	cd ./build-aux && \
	curl -fsSL 'http://git.savannah.gnu.org/gitweb/?p=config.git;a=blob_plain;f=config.guess;hb=HEAD' -o config.guess && \
	curl -fsSL 'http://git.savannah.gnu.org/gitweb/?p=config.git;a=blob_plain;f=config.sub;hb=HEAD' -o config.sub && \
	cd ../ && \
	./configure --prefix="${PREFIX}" --disable-static --enable-shared && \
	make -j $(nproc) && \
	make -j $(nproc) install

## Codec 2 https://github.com/drowe67/codec2/
WORKDIR /tmp/codec2
RUN \
	curl -fsSL https://github.com/drowe67/codec2/archive/v0.9.2.tar.gz | \
		tar -xz --strip-components=1 && \
	mkdir codec2-build && cd codec2-build && \
	cmake -DCMAKE_BUILD_TYPE=Release ../ && \
	make -j $(nproc) install

## kvazaar https://github.com/ultravideo/kvazaar
WORKDIR /tmp/kvazaar
RUN \
	curl -fsSL https://github.com/ultravideo/kvazaar/archive/v2.0.0.tar.gz | \
		tar -zx --strip-components=1 && \
	./autogen.sh && \
	./configure --prefix="${PREFIX}" --disable-static --enable-shared && \
	make -j $(nproc) && \
	make -j $(nproc) install

## libaribb24 https://github.com/nkoriyama/aribb24/
WORKDIR /tmp/aribb24
RUN \
	curl -fsSL https://github.com/nkoriyama/aribb24/tarball/master | \
		tar -xz --strip-components=1 && \
	autoreconf -fiv && \
	./configure --prefix="${PREFIX}" && \
	make -j $(nproc) && \
	make -j $(nproc) install

## libmysofa https://github.com/hoene/libmysofa/
WORKDIR /tmp/libmysofa
RUN \
	curl -fsSL https://github.com/hoene/libmysofa/archive/v1.1.tar.gz | \
		tar -xz --strip-components=1 && \
	mkdir libmysofa-build && cd libmysofa-build && \
	cmake -DCMAKE_BUILD_TYPE=Release ../ && \
	make -j $(nproc) install

## libsrt https://github.com/Haivision/srt
WORKDIR /tmp/srt
RUN \
	curl -fsSL https://github.com/Haivision/srt/archive/v1.4.1.tar.gz | \
		tar -xz --strip-components=1 && \
	cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX="${PREFIX}" . && \
	make -j $(nproc) && \
	make -j $(nproc) install

## opencore-amr https://sourceforge.net/projects/opencore-amr/
WORKDIR /tmp/opencore
RUN \
	curl -fsSL https://versaweb.dl.sourceforge.net/project/opencore-amr/opencore-amr/opencore-amr-0.1.5.tar.gz | \
		tar -zx --strip-components=1 && \
	./configure --prefix="${PREFIX}" --enable-shared  && \
	make -j $(nproc) && \
	make -j $(nproc) install

## TwoLAME https://www.twolame.org/
WORKDIR /tmp/twolame
RUN \
	curl -fsSL https://downloads.sourceforge.net/twolame/twolame-0.4.0.tar.gz | \
		tar -xz --strip-components=1 && \
	./configure --prefix="${PREFIX}" --disable-static --enable-shared && \
	make -j $(nproc) && \
	make -j $(nproc) install

# libopenmpt - libportaudio http://www.portaudio.com/
WORKDIR /tmp/libportaudio
RUN \
	curl -fsSL http://www.portaudio.com/archives/pa_snapshot.tgz | \
		tar -xz --strip-components=1 && \
	./configure --prefix="${PREFIX}" --disable-static --enable-shared && \
	make -j $(nproc) && \
	make -j $(nproc) install && \
	cd ./bindings/cpp && \
	./configure --prefix="${PREFIX}" --disable-static --enable-shared && \
	make -j $(nproc) && \
	make -j $(nproc) install

# libopenmpt - libopenmpt https://lib.openmpt.org/libopenmpt/
WORKDIR /tmp/libopenmpt
RUN \
	curl -fsSL https://lib.openmpt.org/files/libopenmpt/src/libopenmpt-0.5.0+release.autotools.tar.gz | \
		tar -xz --strip-components=1 && \
	./configure --prefix="${PREFIX}" --disable-static --enable-shared && \
	make -j $(nproc) && \
	make -j $(nproc) install

# Intel-Media-SDK https://github.com/Intel-Media-SDK/MediaSDK/
WORKDIR /tmp/libmfx
RUN \
	curl -fsSL https://github.com/Intel-Media-SDK/MediaSDK/archive/intel-mediasdk-20.1.1.tar.gz | \
		tar -xz --strip-components=1 && \
	mkdir libmfx-build && cd libmfx-build && \
	cmake -DCMAKE_BUILD_TYPE=MinSizeRel ../ && \
	make -j $(nproc) && \
	make -j $(nproc) install

ENV CFLAGS="-O2 -pipe -march=x86-64 -mtune=generic"
ENV CXXFLAGS="-O2 -pipe -march=x86-64 -mtune=generic"

## ffmpeg https://ffmpeg.org/
WORKDIR /tmp/ffmpeg
RUN  \
	mkdir -p /build${PREFIX}/bin/ && \
	curl -fsSL https://ffmpeg.org/releases/ffmpeg-4.3.1.tar.bz2 | \
		tar -jx --strip-components=1 && \
	./configure \
		--disable-debug \
		--disable-doc \
		--disable-ffplay \
		--disable-filter=resample \
		--disable-stripping \
		--disable-thumb \
		--enable-avisynth \
		--enable-avresample \
		--enable-chromaprint \
		--enable-fontconfig \
		--enable-frei0r \
		--enable-gpl \
		--enable-ladspa \
		--enable-libaom \
		--enable-libaribb24 \
		--enable-libass \
		--enable-libbluray \
		--enable-libbs2b \
		--enable-libcaca \
		--enable-libcdio \
		--enable-libcodec2 \
		--enable-libdc1394 \
		--enable-libdrm \
		--enable-libfdk_aac \
		--enable-libflite \
		--enable-libfontconfig \
		--enable-libfreetype \
		--enable-libfribidi \
		--enable-libgme \
		--enable-libgsm \
#		--enable-libiec61883 \
		--enable-libjack \
		--enable-libkvazaar \
		--enable-libmp3lame \
		--enable-libmysofa \
		--enable-libopencore-amrnb \
		--enable-libopencore-amrwb \
		--enable-libopenjpeg \
		--enable-libopenmpt \
		--enable-libopus \
		--enable-libpulse \
		--enable-librsvg \
		--enable-librubberband \
		--enable-libshine \
		--enable-libsnappy \
		--enable-libsoxr \
		--enable-libspeex \
		--enable-libsrt \
		--enable-libssh \
		--enable-libtheora \
		--enable-libtwolame \
		--enable-libvidstab \
		--enable-libvorbis \
		--enable-libvpx \
		--enable-libwavpack \
		--enable-libwebp \
		--enable-libx264 \
		--enable-libx265 \
		--enable-libxcb \
		--enable-libxml2 \
		--enable-libxvid \
		--enable-libzmq \
#		--enable-libzvbi \
		--enable-lv2 \
		--enable-nonfree \
		--enable-openal \
		--enable-opengl \
		--enable-openssl \
		--enable-postproc \
		--enable-sdl2 \
		--enable-shared \
		--enable-version3 \
		--extra-cflags="-I${PREFIX}/include ${CFLAGS}" \
		--extra-cxxflags="-I${PREFIX}/include ${CXXFLAGS}" \
		--extra-ldflags="-L${PREFIX}/lib" \
		--extra-libs="-lpthread -lm" \
		--prefix="${PREFIX}" \
		\
		--enable-libmfx \
		--enable-vaapi \
		--enable-vdpau && \
	make -j $(nproc) && \
	make -j $(nproc) install && \
	make tools/zmqsend && \
	cp tools/zmqsend /build${PREFIX}/bin/ && \
	make distclean && \
	hash -r && \
	cd tools && \
	make qt-faststart && \
	cp qt-faststart /build${PREFIX}/bin/


WORKDIR /tmp/build
COPY ./extractlibrary cp.sh
RUN chmod +x ./cp.sh
RUN echo /usr/local/bin/ffmpeg >> cplist
RUN echo /usr/local/bin/ffprobe >> cplist
RUN ./cp.sh cplist /build

RUN cp --archive --parents --no-dereference /opt/intel /build

RUN rm -rf /tmp/* /var/cache/apk/*


# final image
FROM alpine:3.13.5 AS release
LABEL maintainer "collelog <collelog.cavamin@gmail.com>"

ENV LD_LIBRARY_PATH=/opt/intel/mediasdk/lib64:/usr/local/lib64:/usr/local/lib:/usr/lib:/lib

COPY --from=ffmpeg-build /build /
COPY --from=ffmpeg-build /build /build

RUN set -eux && \
	apk upgrade --no-cache --update-cache && \
	apk add --no-cache --update-cache \
		libva-intel-driver \
		mesa-va-gallium \
		mesa-vdpau-gallium && \
	echo http://dl-2.alpinelinux.org/alpine/edge/community >> /etc/apk/repositories && \
	apk add --no-cache --update-cache \
		intel-media-driver && \
	echo http://dl-2.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories && \
	apk add --no-cache --update-cache \
		libva-vdpau-driver && \
	\
	# cleaning
	rm -rf /tmp/* /var/cache/apk/*

ENTRYPOINT  ["ffmpeg"]
CMD  ["--help"]