<img width="706" height="732" alt="image" src="https://github.com/user-attachments/assets/d3b48f90-d5a2-41c4-b95b-56fdb88d26df" />


## Install Dependencies (In termux android)
You need to install the build and runtime dependancies:

`pkg install git cmake make clang mariadb boost-headers boost-static`

### Install Azerothcore
Clone the project

`git clone https://github.com/duall/azerothcore-android.git`

### Enter the project's directory

`cd azerothcore`

### Create the build directory

`mkdir build`

### Enter the directory

`cd build`

### Configure azerothcore for building

`cmake ../ -DCMAKE_INSTALL_PREFIX=$HOME/azeroth-server/ \
-DCMAKE_C_COMPILER=$PREFIX/bin/clang \
-DCMAKE_CXX_COMPILER=$PREFIX/bin/clang++ \
-DWITH_WARNINGS=1 -DTOOLS=0 -DSCRIPTS=static \
-DCMAKE_CXX_FLAGS="-D__ANDROID__ -DANDROID" \
-DCMAKE_EXE_LINKER_FLAGS="-Wl,--allow-multiple-definition"`

## Compile Azerothcore

`make -j$(nproc)`

### Install Azerothcore

`make install`

You will find executables in ~/azeroth-server/bin/


## Troubleshooting
##### CANNOT LINK EXECUTABLE "./authserver": library "libmariadb.so" not found: needed by main executable

fix: `ln -sf $PREFIX/lib/aarch64-linux-android/libmariadb.so $PREFIX/lib/libmariadb.so`


