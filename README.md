RICOH Aficio SP 100SU Linux CUPS driver
---------------------------------------

This is an open-source CUPS filter for RICOH Aficio SP 100SU laser printer.

# How to build on Debian/Ubuntu

```
sudo apt install -y dpkg-dev
mkdir build && cd build
git clone https://github.com/Marisa-Chan/aficio_sp100su
cd aficio_sp100su
dpkg-buildpackage -nc
cd ../
sudo apt install ./aficio-sp100su_*.deb
```

# How to build (generic)

```
git clone https://github.com/Marisa-Chan/aficio_sp100su
cd aficio_sp100su
cmake -S src -B build
cmake --build build
sudo cmake --install build
```
