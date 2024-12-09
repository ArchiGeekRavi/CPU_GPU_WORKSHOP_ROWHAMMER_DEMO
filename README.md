# Rowhammer Demonstration
    1. Ravi Kumar Choubey
    2. Mrityunjay Shukla

## Prequitistics
RAMSES is implemented by Vusec and provides mapping functions for Intel Sandy Bridge, Ivy Bridge and Haswell memory controllers. Our Experiment was tested on Intel Haswell system with DDR3 Memory Module.

## Steps:
### 1. Check the system environment

##### Intel Architecture :- 
```bash
gcc -march=native -Q --help=target|grep march
```
##### Model information :-
```bash
cat /proc/cpuinfo | fgrep -i model

```
##### DRAM information :- 
```bash
sudo dmidecode -t memory
```
##### OS version :-
```bash
lsb_release -a

```

### 2. Build and test

##### Clone the github and add ramses as a submodule
```bash
git clone https://github.com/vusec/hammertime.git
cd hammertime
rm -rf ramses 
git rm --cached ramses
git submodule add https://github.com/vusec/ramses.git
```

##### Run and Profiling bit flips for rowhammer vulnerability :-
```bash
#Build at Hammertime root directory
make

#Detect system’s memory configuration
sudo ramses/tools/msys_detect.py

#Profiling: single (--s or single) and double hammering (--double)
sudo profile/profile --s 256m mem.msys 2>&1 | tee myprof_s.res
sudo profile/profile --double 256m mem.msys 2>&1 | tee myprof_d.res
```
