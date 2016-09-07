# installHEP

UBUNTU MATE 16.04 ARCH=64.

INSTALL CLHEP
-------------
sudo apt-get install cmake cmake-curses-gui
sudo apt-get install git dpkg-dev make g++ gcc binutils libx11-dev libxpm-dev libxft-dev libxext-dev

cd $HOME
mkdir CLHEP
cd CLHEP
wget http://proj-clhep.web.cern.ch/proj-clhep/DISTRIBUTION/tarFiles/clhep-2.3.1.1.tgz
tar xvf clhep-2.3.1.1.tgz
mkdir 2.3.1.1-build 2.3.1.1-install
cd 2.3.1.1-build
cmake -DCMAKE_INSTALL_PREFIX=$HOME/CLHEP/2.3.1.1-install $HOME/CLHEP/2.3.1.1/CLHEP
make -j4
make test
make install

edit .bashrc and add
export PATH=$PATH:$HOME/2.3.1.1-install/bin:$HOME/2.3.1.1-install/include
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$HOME/CLHEP/2.3.1.1-install/lib



INSTALL PYTHIA8
---------------

cd $HOME
mkdir PYTHIA8
cd PYTHIA8
wget home.thep.lu.se/~torbjorn/pythia8/pythia8219.tgz
tar xvfz pythia8219.tgz
cd pythia8219
./configure
make -j4

edit .bashrc and add
....................
export PYTHIA8DATA=$HOME/PYTHIA8/pythia8219/share/Pythia8/xmldoc
export PYTHIA=$HOME/PYTHIA8/pythia8219/lib



INSTALL ROOT 5.34.36
--------------------
cd $HOME
mkdir ROOT
cd ROOT
wget https://root.cern.ch/download/root_v5.34.36.source.tar.gz 
tar xvvfz root_v5.34.36.source.tar.gz
mv root 5.34.36
cd 5.34.36
sudo apt-get install gfortran libssl-dev libpcre3-dev libglu1-mesa-dev libglew-dev libftgl-dev libmysqlclient-dev libfftw3-dev graphviz-dev libavahi-compat-libdnssd-dev libldap2-dev python-dev libxml2-dev libkrb5-dev libgsl-dev libqt4-dev
./configure linuxx8664gcc --enable-pythia8 --all
make -j4

edit .bashrc and add
....................
source $HOME/ROOT/5.34.36/bin/thisroot.sh



INSTALL GEANT4 10.02.P02
------------------------
Get file from geant4.cern.ch :
geant4.10.02.p02.tar.gz
and put it at $HOME/GEANT4


cd $HOME/GEANT4
mkdir 10.02.p02-build 10.02.p02-install
tar xvfz geant4.10.02.p02.tar.gz
mv geant4.10.02.p02 10.02.p02

sudo apt-get install libxerces-c-dev libxerces-c-doc libxerces-c-samples libxerces-c3.1 gccxml
sudo apt-get install libxmu-dev


cd 10.02.p02-build
cmake -DCMAKE_INSTALL_PREFIX=$HOME/GEANT4/10.02.p02-install \
-DCLHEP_ROOT_DIR=$HOME/CLHEP/2.3.1.1-install \
-DGEANT4_USE_SYSTEM_CLHEP=ON \
-DGEANT4_USE_SYSTEM_EXPAT=ON \
-DGEANT4_USE_GDML=ON \
-DGEANT4_USE_QT=ON \
-DGEANT4_USE_OPENGL_X11=ON \
-DGEANT4_USE_RAYTRACER_X11=ON \
$HOME/GEANT4/10.02.p02
make -j4
make install

create folder for data

mkdir -p $HOME/GEANT4/10.02.p02-install/share/Geant4-10.2.2/data

and download these files from webpage

G4ABLA.3.0.tar.gz
G4EMLOW.6.48.tar.gz
G4ENSDFSTATE.1.2.3.tar.gz
G4NDL.4.5.tar.gz
G4NEUTRONXS.1.4.tar.gz
G4PhotonEvaporation.3.2.tar.gz
G4PII.1.3.tar.gz
G4RadioactiveDecay.4.3.2.tar.gz
G4SAIDDATA.1.1.tar.gz
G4TENDL.1.0.tar.gz
RealSurface.1.0.tar.gz

change directory to data and extract all

for i in $(ls); do tar xvvfz $i; done


edit .bashrc and add
source $HOME/GEANT4/10.02.p02-install/bin/geant4.sh
export G4ABLA3.0=$HOME/GEANT4/10.02.p02-install/share/Geant4-10.2.2/data/G4ABLA3.0
export G4EMLOW6.48=$HOME/GEANT4/10.02.p02-install/share/Geant4-10.2.2/data/G4EMLOW6.48
export G4ENSDFSTATE1.2.3=$HOME/GEANT4/10.02.p02-install/share/Geant4-10.2.2/data/G4ENSDFSTATE1.2.3
export G4NDL4.5=$HOME/GEANT4/10.02.p02-install/share/Geant4-10.2.2/data/G4NDL4.5
export G4NEUTRONXS1.4=$HOME/GEANT4/10.02.p02-install/share/Geant4-10.2.2/data/G4NEUTRONXS1.4
export G4PII1.3=$HOME/GEANT4/10.02.p02-install/share/Geant4-10.2.2/data/G4PII1.3
export G4SAIDDATA1.1=$HOME/GEANT4/10.02.p02-install/share/Geant4-10.2.2/data/G4SAIDDATA1.1
export G4TENDL1.0=$HOME/GEANT4/10.02.p02-install/share/Geant4-10.2.2/data/G4TENDL1.0
export PhotonEvaporation3.2=$HOME/GEANT4/10.02.p02-install/share/Geant4-10.2.2/data/PhotonEvaporation3.2
export RadioactiveDecay4.3.2=$HOME/GEANT4/10.02.p02-install/share/Geant4-10.2.2/data/RadioactiveDecay4.3.2
export RealSurface1.0=$HOME/GEANT4/10.02.p02-install/share/Geant4-10.2.2/data/RealSurface1.0


INSTALL ECAT
------------
Download the file ecat.tar.gz from website http://opengatecollaboration.org/ECAT

cd $HOME
mkdir ECAT
cd ECAT
tar xvfz ecat.tar.gz
cp Makefile.unix Makefile
make 
cd utils
cp Makefile.unix Makefile
sudo apt-get install happycoders-libsocket
sudo cp /usr/lib/libsocket.so.0 /usr/lib/libsocket.so
make 
cd ../
add header #include <string.h> to file applynorm.c

mkdir include lib
cp *.h include/
cp libecat.a lib/



INSTALL LMF
-----------

mv lmf_v3_0.tar_2.gz lmf_v3_0.tar.gz
tar xvfz lmf_v3_0.tar.gz
mv lmf_v3.0 3.0
cd 3.0
./configure
make clean
make 

src/testField.c:53:11: error: invalid type argument of unary ‘*’ (have ‘int’) if (*gets(reply) == 'y') {
#FIXME#


INSTALL GATE
------------

Get file gate_v7.2.tar.gz from webpage
http://opengatecollaboration.org/GATE72
and put it on $HOME/GATE/

cd $HOME/GATE/
tar xvfz gate_v7.2.tar.gz
mv gate_v7.2 7.2
mkdir 7.2-build 7.2-install
cd 7.2-build
ccmake ../7.2


type c
type e
change GATE_INSTALL_PREFIX
type c
type e
type g
see screenshot
make -j4
sudo make install

edit .bashrc and add
export PATH=$PATH:$HOME/GATE/gate_v7.2-install/bin



INSTALL FORM
------------
sudo apt-get install autoconf
sudo apt-get install libgmp-dev zlib1g-dev
mkdir FORM
cd FORM
git clone https://github.com/vermaseren/form
autoreconf -i
./configure
make
make install
sudo cp $HOME/FORM/form-install/bin/form /usr/local/bin/form



INSTALL MAGNETOCOSMICS
----------------------
Get magnetocosmics_static_2.0.tar.gz

cd $HOME
mkdir MAGNETOCOSMICS
cd MAGNETOCOSMICS
tar xvfz magnetocosmics_static_2.0.tar.gz
mv magnetocosmics static2.0
cd static2.0/bin
sudo cp STATIC_MAGNETOCOSMICS /usr/local/bin/
sudo cp scale_vrmlfile.sh /usr/local/bin/



INSTALL PLANETOCOSMICS
----------------------

Get planetocosmics_static_root_v2.0.tar.gz

cd $HOME
mkdir PLANETOCOSMICS
cd PLANETOCOSMICS
tar xvfz planetocosmics_static_root_v2.0.tar.gz
mv planetocosmics static2.0
cd static2.0/bin
sudo cp PLANETOCOSMICS_ROOT_STATIC /usr/local/bin/
sudo cp scale_vrmlfile.sh /usr/local/bin/



INSTALL LATEX
-------------

sudo apt-get install texlive-full
cd $HOME
mkdir LATEX
cd LATEX
wget http://desktop-publishing.web.cern.ch/desktop-publishing/cernrep.zip
unzip cernrep.zip
cp cernrep/*.sty .



INSTALL JAVA SDK 8.101
----------------------
```
mkdir $HOME
cd $HOME
```
Go to 
```
http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
and download the file 
jdk-8u101-linux-x64.tar.gz
tar xvfz jdk-8u101-linux-x64.tar.gz
mv jdk1.8.0_101 1.8.0_101
```

edit .bashrc and add
```
export PATH=$PATH:$HOME/JDK/1.8.0_101/bin:$HOME/JDK/1.8.0_101/include
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$HOME/JDK/1.8.0_101/lib
```


INSTALL ANDROID STUDIO
----------------------
```
sudo apt-get install lib32z1 lib32ncurses5 lib32bz2-1.0 lib32stdc++6 
cd $HOME
mkdir ANDROID-STUDIO
cd ANDROID-STUDIO
wget https://dl.google.com/dl/android/studio/ide-zips/2.1.2.0/android-studio-ide-143.2915827-linux.zip
unzip android-studio-ide-143.2915827-linux.zip
mv android-studio-ide-143.2915827-linux 143.2915827
```
edit .bashrc and add
```
export PATH=$PATH:$HOME/ANDROID-STUDIO/143.2915827/bin
```
studio.sh

and follow instructions.


INSTALL NODEJS
--------------
```
cd $HOME
mkdir NODEJS
cd NODEJS
wget https://nodejs.org/dist/v4.4.7/node-v4.4.7.tar.gz
tar xvfz node-v4.4.7.tar.gz
mv node-v4.4.7 4.4.7
cd 4.4.7
mkdir install
./configure --prefix=$HOME/NODEJS/4.4.7/install
make -j4
make install
```
edit .bashrc and add
```
export PATH=$PATH:$HOME/NODEJS/4.4.7/install/bin
```

INSTALL APACHE, MYSQL, PHP SERVER
---------------------------------
```
sudo apt-get install apache2
sudo apt-get install mysql-server php-mysql
sudo apt-get install php libapache2-mod-php php-mcrypt
```

