# pigpio for ArchLinux ARM
Harware revision information obtained from `/root/rpiinfo.txt` instead of `/proc/cpuinfo`.

## Compile and install
```
git clone -b pkg https://github.com/zrel/pigpio.git
cd pigpio
makepkg -si
```

## Create HW info file
Copy sample file (for RPi 4 B) and update its content if necessary to match current Raspberry board.
```
sudo cp <path/to/this/folder>/rpiinfo.txt /root/rpiinfo.txt
```
Then you can run the pigpio service
```
sudo systemctl enable pigpiod.service
sudo systemctl start pigpiod.service
```
## Test commands for direct execution
```
git clone -b pkg https://github.com/zrel/pigpio.git
cd pigpio
tar -xzvf pigpio-500.tar.gz
cd pigpio-500
make
sudo LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/alarm/pigpio/pigpio-500/ ./pigpiod -k
```
