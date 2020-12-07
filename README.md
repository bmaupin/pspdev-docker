Docker images with the [pspdev toolchain](https://github.com/pspdev/psptoolchain) prebuilt.

## Usage

Change to the directory containing the PSP source code you'd like to build and use this command to build it:

```
docker run --rm -v "$PWD:/build" bmaupin/pspdev make
```

TempGBA4PSP requires an older version of gcc. You can use this command instead:

```
docker run --rm -v "$PWD:/build" bmaupin/pspdev:gcc-4.6.4 make
```


## Building these images

To build these images locally:

```
docker build -f gcc-4.6.4/Dockerfile -t pspdev-docker:gcc-4.6.4
docker build -f latest/Dockerfile -t pspdev-docker:latest
gcc_version=$(docker run -it --rm pspdev-docker:latest gcc --version | head -n 1 | cut -d " " -f 4 | tr -d '\r\n')
docker tag pspdev-docker:latest pspdev-docker:gcc-${gcc_version}
```
