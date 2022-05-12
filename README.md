

# Building patched flussonic packages

1. Build docker image with `docker build --pull . -f Dockerfile -t builder-22.02.1`
2. Run `docker run --rm -it -v $(pwd)/repack-flussonic:/build/repack builder-22.02.1 ./build.sh` to repack and build flussonic packages into local `repack-flussonic` directory

# Installing

1. Full installation with watcher `dpkg -i *.deb`
2. Flussonic only installation `dpkg -i flussonic_22.02.1_all.deb flussonic-deprecated_22.02.1_all.deb flussonic-erlang_24.0.6.3_all.deb flussonic-qsv_21.07.1_all.deb flussonic-transcoder_21.11.1_all.deb flussonic-transcoder-base_21.11.1_all.deb`


# Old Ubuntu or arm64 architectures
## Building crossplatform erlang packages for ALL available distros/arch

Installing on older Ubuntu versions or on arm64 architecture needs appropriate erlang package.

1. Build docker image with `docker build --pull . -f Dockerfile.esl-erlang -t builder-esl`
2. Run `docker run --rm -it -v $(pwd)/repack-erlang:/repack builder-esl` to copy all erlang packages from builder image to local `repack-erlang` directory
3. Install appopriate package
4. Run `apt-get install -f --no-install-recommends` to fix missing dependencies

# Build single erlang package for required architecture/distro

1. Adjust DISTRO, RELEASE, ARCH arguments inside `Dockerfile.esl-erlang-single` as per Erlang Solutions repository https://www.erlang-solutions.com/downloads/
2. Build docker image with `docker build --pull . -f Dockerfile.esl-erlang-single -t builder-esl-single`
3. Run `docker run --rm -it -v $(pwd)/repack-erlang:/repack builder-esl-single` to copy all erlang packages from builder image to local `repack-erlang` directory
4. Install appopriate package
5. Run `apt-get install -f --no-install-recommends` to fix missing dependencies
