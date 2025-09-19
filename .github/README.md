### ! Go here for one click install script + preconfigured 40modules singleplayer config:

### https://github.com/duall/singlePlayerWow-android



## This repo is for raw azerothcore+playerbots:

<img width="310" height="414" alt="image" src="https://github.com/user-attachments/assets/a249da67-2bfe-4c30-b11b-0227a0f17edc" />

*yes it runs on a smartwatch ^^*



## Install Dependencies (In termux android)
You need to install the build and runtime dependancies:

`pkg install git cmake make clang mariadb boost-headers boost-static libc++`

### Install Azerothcore
Clone the project

`git clone https://github.com/duall/azerothcore-android.git`

### Enter the project's directory

`cd azerothcore-android`

### Clone playerbot module

`git clone https://github.com/liyunfan1223/mod-playerbots.git modules/mod-playerbots`

### Create the build directory

`mkdir build`

### Enter the directory

`cd build`

### Configure azerothcore for building

`cmake ../ -DCMAKE_INSTALL_PREFIX=$HOME/azeroth-server/ \
-DCMAKE_C_COMPILER=$PREFIX/bin/clang \
-DCMAKE_CXX_COMPILER=$PREFIX/bin/clang++ \
-DWITH_WARNINGS=1 -DTOOLS=0 -DSCRIPTS=static \
-DCMAKE_CXX_FLAGS="-D__ANDROID__ -DANDROID -Wno-deprecated-literal-operator" \
-DCMAKE_EXE_LINKER_FLAGS="-Wl,--allow-multiple-definition -lunwind"`

## Compile Azerothcore

`make -j$(nproc)`

### Install Azerothcore

`make install`

You will find executables in ~/azeroth-server/bin/

### Apply configs

`cp ~/azeroth-server/etc/authserver.conf.dist ~/azeroth-server/etc/authserver.conf && cp ~/azeroth-server/etc/worldserver.conf.dist ~/azeroth-server/etc/worldserver.conf`

### Download serverdata
`curl -L https://github.com/wowgaming/client-data/releases/download/v16/data.zip -o ~/data.zip && unzip ~/data.zip -d ~/azeroth-server/ && rm ~/data.zip`

### Fix mariadb link
##### CANNOT LINK EXECUTABLE "./authserver": library "libmariadb.so" not found: needed by main executable

`ln -sf $PREFIX/lib/aarch64-linux-android/libmariadb.so $PREFIX/lib/libmariadb.so`

## Servers should be runnable now

`cd ~/azeroth-server/`

`./bin/authserver`

`./bin/worldserver`

Enjoy



