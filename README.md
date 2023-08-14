# free_cloud_ssd

# Installation
## The source way (building from source with manually installing dependencies)

=== *Please note: building from source takes **a lot of CPU and RAM** usage.* ===\
You need to have installed:
- [Rust](https://www.rust-lang.org/tools/install) 
- [opencv](https://github.com/twistedfall/opencv-rust)

If having any issues also try installing:
- [ffmpeg](https://ffmpeg.org/)
- [clang](https://clang.llvm.org/)
- [qt](https://github.com/qt)

If you want to or already have went through the hassle of installing Rust, you can ```git clone``` this repository, then ```cargo build --release```.
Cd to `/target/release` directory and run the program `./isg_4real`.

## The easiest way (Docker)

Trying to make anything work on other people's computers is a nightmare so I'll use docker from now on \
[Trend Oceans](https://trendoceans.com/isg-lets-you-use-youtube-as-cloud-storage-for-any-files-not-just-video/) wrote a neat article on how to use this method as well.

1. Install [Docker](https://docs.docker.com/get-docker/) if you haven't already.
2. Clone this repository
3. Change into the repository `cd Infinite-Storage-Glitch`
4. Run `docker build -t isg .` to build the docker image.
5. Run `docker run -it --rm -v ${PWD}:/home/Infinite-Storage-Glitch isg cargo build --release` to build the project.

```

**Note:** If you are using `cmd` on Windows, you will need to use `%cd%` instead of `${PWD}`.

How to use
-------------
1. Archive to zip all the files you will be uploading
2. Run the executable
3. Use the embed option on the archive (**THE VIDEO WILL BE SEVERAL TIMES LARGER THAN THE FILE**, 4x in case of optimal compression resistance preset)
4. Upload the video to your YouTube channel. You probably want to keep it up as unlisted
5. Use the download option to get the video back
6. Use the dislodge option to get your files back from the downloaded video
7. PROFIT

***No it's not just a rick roll.***

Explanation 4 nerds
-------------
The principle behind this is pretty simple. All files are made of bytes and bytes can be interpreted as numbers ranging from 0-255. This number can be represented with pixels using one of two modes: RGB or binary.

**RGB**:
The cooler mode. Every byte perfectly fits inside one of the colors of an rgb pixel. One rgb pixel can contain 3 bytes at a time. You just keep adding pixels like this until you run out of data. It is leagues more efficient and quick than binary.

**Binary**:
Born from YouTube compression being absolutely brutal. RGB mode is very sensitive to compression as a change in even one point of one of the colors of one of the pixels dooms the file to corruption. Black and white pixels are a lot harder to mess up. Every pixel is either bright representing a 1 or dark representing a 0. We string these bits together to get bytes and continue until we run out of data. 

Both of these modes can be corrupted by compression, so we need to increase the size of the pixels to make it less compressable. 2x2 blocks of pixels seem to be good enough in binary mode.

To make it easier on the user, we also include all the relevant settings used to create the video on the first frame of the video. This allows the program to know what mode the video is in and what size to use in order to avoid making the user remember.

# Final comments
I appreciate any and all roasting of the code so I can improve.

Do what you want with the code, but credit would be much appreciated and if you have any trouble with ISG, please contact me over discord.
