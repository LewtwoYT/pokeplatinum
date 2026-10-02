# Pokémon Platinum PC Port
## Info
_Feel free to join us on [Discord](https://discord.gg/ZgtPszuBeN) for discussion or support._

**pokeplatinum** is an experimental PC port of Pokémon Platinum based on the [pret](https://github.com/pret/pokeplatinum) decompilation project and powered by the [libntr](https://github.com/cybervisi0n/libntr) suite; a collection of libraries that replace the NitroSDK to allow for easy porting of Nintendo DS titles.

* The port should be possible to play from start to finish, albeit with crashes and minor graphical bugs. **[If you spot any issues, please report them here to be fixed!](https://github.com/cybervisi0n/pokeplatinum/issues)**
* Generative AI/LLM shortcuts were **not** used in the creation of this project. **Pull requests or code suggestions using AI will be rejected.**

## Project Goals:
* Create a native port of pokeplatinum for 64-bit PC platforms
* * Long term: Create native ports for homebrew on various game consoles
* Facilitate modding by allowing both a PC port and DS ROM to be compiled and debugged from the same source tree
* Support for all Wi-Fi and multiplayer features

## Setup Guide
### Pre-Built Binaries (running via .exe)
To run the [pre-built binaries found in the releases tab,](https://github.com/cybervisi0n/pokeplatinum/releases) **you MUST dump and extract your own US ROM of Pokémon Platinum.** Extraction of the ROM is automatic, but you still must provide your own.

* On the first launch of **main.exe** you'll be prompted to select your own **.nds** file, as seen below.

![ROM extraction dialog 1](images/BinarySetup.png)

* Now you're done! Click **main.exe** to launch your game at any point. **To access in-game debug tools, press Tab.**

### Building on Linux
#### Dockerized build (Recommended)
This only requires Docker to be installed and setup on your system. The drun.sh script is used to build the docker image and run build commands in it. Build with:
* ./drun.sh make linux

The container image will automatically be built the first time this script is run.

#### Non-container build
Required Packages (arch linux):
* nasm
* enet
* arm-none-eabi-gcc (required by the base pret project)
* ninja
* flex
* bison

To build: 
* make linux

Alternatively:
* meson setup build
* cd build
* meson configure -Dbuild_target=linux
* meson compile

You can also build a ROM from the same source tree, just run:
* make

### Building on Windows
From a freshly cloned repo, run the "Install_MSys2.ps1" script in powershell. This will create a portable MSys2 build environment with all dependencies installed in the repo. This only has to be done once per repo.

To build, run "Launch_MSys2.ps1" and it will launch a MSys2 bash shell. From here, run "make win64" to build.

## NX Build Target (working, but poor performance)
This build target requires DevKitA64, this is already installed in the build container.
* ./drun.sh make nx

## Notes
Target executable will be in ./build_(platform)/pokeplatinum directory.
ROM will be built in /build directory

firmware.bin does not contain any real DS firmware, it only contains an offset address and enough space to keep the WiFi config.

You can update your SDKs using "meson subprojects update"

### Tracy Profiling
To enable, run ./meson.sh configure -Dtracy_enable=true {build_folder} from the repo root. This works on Win64, Linux, and NX build targets.

