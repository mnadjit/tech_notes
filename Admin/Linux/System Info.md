### System Information

#### Hardware Overview
> `sudo lshw -short` <br>
> `sudo dmidecode`
- more details (Desktop Management Interface)

#### CPU
> `sudo lshw -businfo | grep cpu`
- shortest CPU description
> `lscpu`
- CPU overview
> `cat /proc/cpuinfo`
- Details for each core
> `sudo dmidecode -t processor`
- CPU details

#### GPU
> `lspci -vnn | egrep -i vga|3d`

#### Storage
> `sudo lshw -businfo | grep disk`
- Disk size and model
> `lsblk -pf`
- Get info about all block devices (-p: paths; -f: filesystems label and UUID)
> `df -h`
- Get the size of partitions (-h: human readable)
> `sudo fdisk -l`
- list partitions with more details

> `sudo dnf install ncdu` <br>
> `ncdu $path_to_directory`
- NCDU app for displaying disk usage

#### USB
- `lsusb`: simple short list of USB devices
- `lsusb -t`: in a tree format
- `lsusb -tv`: in a tree format with vendor and product IDs

#### Network
- `ip addr`: list of network interfaces with their IP addresses
- `ip link`: list of network interfaces
- `ip link show`: show details of network interfaces
- `ip link set dev <interface> up`: bring up interface
- `ip link set dev <interface> down`: bring down interface

#### Memory
- `free`: show memory usage in bytes
- `free -mh`: show memory usage in MegaBytes and in human readable format
- `cat /proc/meminfo`: show memory usage in human readable format

#### Bluetooth
BluetoothCtl:
- `bluetoothctl`: A tool in the BlueZ package
  - `power on`
  - `agent on`
  - `default-agent`
  - `scan on`
  - `trust <deviceuuid>`
  - `pair <deviceuuid>`
  - `connect <deviceuuid>`
HCI tool:
- `hcitool dev`
- `hci -i <dev> scan`
- _To be added_