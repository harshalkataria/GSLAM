# You have checked into harshal-dev branch

Look out for any traps ;)

## Guide to installing the GSLAM in Ubuntu 21.04
Firstly refer to the URL: https://zdzhaoyong.github.io/GSLAM/compile.html

### 1. Compiling
Installing dependencies:
- Qt: Required to compile application qviz\
`sudo apt-get install libqt4-dev // Qt5 should also works `\
Here, for Ubuntu 21.04 qt5-default package is missing, so run the following:\
`sudo apt-get install qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools`\
for more information on Qt: https://wiki.qt.io/About_Qt
- OpenCV: Optional, used by some dataset plugins.\
`sudo apt-get install libopencv-dev `\
Here, this installs opencv version 4.5, instead we want opencv version 2.4.9\
so refer the following to install from source: \
[opencv 2.4.9 from source](https://elementztechblog.wordpress.com/2014/07/28/installing-opencv-2-4-9-in-linux/#:~:text=Decompress%20the%20file%20obtained%20above%20using%20the%20below%20command.&text=cmake%20%2DD%20WITH_TBB%3DON%20%2D,%2DD%20CMAKE_INSTALL_PREFIX%3D%2Fusr%20..&text=Finally%20install%20the%20build%20files%20to%20your%20system.)\
In detail for hirsute:
```
sudo apt-get install build-essential libgtk2.0-dev libjpeg-dev libtiff-dev:i386 libtiff-dev jasper libopenexr-dev cmake python-dev-is-python3 python3-numpy python-tk python3-tk libtbb-dev libeigen3-dev yasm libfaac-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev libx264-dev //libqt4-dev libqt4-opengl-dev// sphinx-common texlive-latex-extra libv4l-dev libdc1394-22-dev libavcodec-dev libavformat-dev libswscale-dev default-jdk ant //libvtk5-qt4-dev//
```
after this too opencv install wasn't successfull due to many errors of libraries

if still want to install using the `libopencv-dev` use `--fix-missing`\
To Uninstall lipopencv-dev completely\
`sudo apt-get purge --auto-remove libopencv-dev`

- Ceres: Optional, used by plugin Optimizer.\
`sudo apt-get intall libceres-dev `\
Compile and install with cmake:
```
mkdir build;cd build;
cmake ..;make;sudo make install
```

## Guide to installing the GSLAM in Ubuntu 20.04
Firstly refer to the URL: https://zdzhaoyong.github.io/GSLAM/compile.html

### 1. Compiling
Installing dependencies: [Reference](https://ubuntuhandbook.org/index.php/2020/07/install-qt4-ubuntu-20-04/)
- Qt: Required to compile application qviz\
`sudo add-apt-repository ppa:rock-core/qt4`\
`sudo apt update`\
`sudo apt-get install libqt4-dev`
- OpenCV: Optional, used by some dataset plugins.\
Install version 2.4 only [Reference](https://bobcares.com/blog/how-to-install-opencv-on-ubuntu-20-04/)
This installs opencv 2.4.13.7
- Ceres: Optional, used by plugin Optimizer.\
`sudo apt-get intall libceres-dev`
- Compile and install with cmake:\
`mkdir build;cd build;`\
`cmake ..;make;sudo make install`

### Bash Tab completion
To activate tab completion support for gslam , please add the following contents to your ~/.bashrc :

```
function_gslam_complete()
{
    COMPREPLY=()
    local cur=${COMP_WORDS[COMP_CWORD]};
    local com=${COMP_WORDS[COMP_CWORD-1]};
    local can=$(${COMP_WORDS[*]:0:COMP_CWORD} -help -complete_function_request)
    local reg='-.+'
    if [[ $com =~ $reg ]];then
      COMPREPLY=($(compgen -df -W "$can" -- $cur))
    else
      COMPREPLY=($(compgen -W "$can" -- $cur))
    fi
}
complete -F function_gslam_complete "gslam"
```
