# i9300_lineage

This repository contains modified and cleaned up versions of the scripts and patches I used to build my updated experimental roms for i9300, found in the later pages of [this XDA forum thread](https://forum.xda-developers.com/galaxy-s3/orig-development/experimental-lineageos-14-1-i9300-t3696500). I've since stopped making those builds due to a lack of time and because I switched phones, so using these scripts and patches someone else might be able to continue making them.

# Dependencies
Building LineageOS has a set of dependencies that are required for building to succeed. Those dependencies are listed on [the LineageOS wiki here](https://wiki.lineageos.org/devices/i9300/build#build-lineageos-and-lineageos-recovery), but how you install them depends on your specific distro.

To use these scripts and patches download all the files in the `android` directory and place them in `$HOME/android`. Then, assuming you've already installed and set-up all required dependencies for building LineageOS, follow these steps:

# 1. Build the custom toolchains
Following [this guide](https://github.com/GalaxyMaster2/i9300_ubertc) build your custom toolchains that you intend to use (if you want to use the stock toolchain then you can skip this step). Then, copy them to `$HOME/android/lineage_customstuff/ubertc`. The path to a given toolchain should look like this: `$HOME/android/lineage_customstuff/ubertc/arm-cortex_a9-linux-androideabi-7.x`.

If you try to build with a toolchain which is not present in the aforementioned directory, the scripts will most likely fail in unexpected ways.

# 2. Set the USE_CCACHE setting inside the scripts
If you have a ccache set up and want to use it with the builds, you can leave the scripts as they are. If not, please comment out the `export USE_CCACHE=1` line in the relevant scripts before you run them to avoid problems.

# 3. Execute your desired script
There are 3 main scripts of interest, with the others being subscripts used by the main scripts. They are:

* `./build_lineage`
* `./build_lineage_uber_hwc`
* `./uber_hwc_build_all`

`./build_lineage` is an interactive script that receives input for various options. It then automatically syncs the LineageOS sources to the latest available and cleans out any relevant directories. After that it executes the build using the options you set, and when it's done copies and renames the flashable .zip file to `$HOME/android/builds`.

`./build_lineage_uber_hwc` is a modified version of `./build_lineage` that has preset options for building with UBER toolchains optimized for Cortex A9 for both the kernel and the rom, and using the HWC experimental patches. It also takes the GCC version to be used as a command line argument (defaulting to 4). Valid GCC versions are: `4, 5, 6, 7, 8`.

`./uber_hwc_build_all` is a script that asks for input on which GCC versions to build for, and then executes `./build_lineage_uber_hwc` for each given version.

# Notes:
It's been more than a year since I've last used these scripts and patches to build roms. It's possible that they won't work right away and may require modifications or additional patches. If you need assistance on getting these scripts to work please don't hestitate to contact me.

I have also never been able to get a build with GCC version 8 to work due to a build error that I was unable to solve. Thus, it is highly likely that it won't work for you either. It will likely require additional patches that are not included in this repository. If you have managed to get it to work feel free to create a pull request.

Although support for Linaro toolchains exists within the scripts, I have never successfully used them to build roms. As such, I have currently commented out Linaro options in the scripts. You are free to try making Linaro builds, but don't expect it to work right away. It will likely require a lot of effort to get working, and as such you are on your own with that.
