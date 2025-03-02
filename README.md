# -Install-Kali-VM-Alfa-WIFI-Adapter-Fix-Fetch-and-Linux-Header-Error
## Prerequisites
- Install **VirtualBox**
- Install **Kali Linux 64-bit** for VirtualBox

### Default Credentials
- **Username:** kali
- **Password:** kali

---

## Step 1: Fix Display Issues
Kali Linux default display might be too small. Adjust the resolution under **Display Settings** for better usability.

## Step 2: Connect Alfa Network USB Adapter
We are working with the **Alfa Network AC600 USB adapter (AWUS036ACS)**.
- Available on **Amazon** or **Walmart** (~$25).

## Step 3: Update Kali Linux
Open the Kali Linux terminal and run:
```bash
sudo apt update && sudo apt upgrade -y
```

## Step 4: Check Kernel Version
Run the following command to find your distribution and version:
```bash
uname -r
```

To ensure the latest version of the distro, run:
```bash
sudo apt dist-upgrade -y
```

## Step 5: Identify USB Adapter
After plugging in the **Alfa USB adapter**, wait a few seconds and navigate to:
- **Virtual Machine Menu → Devices** (Top left of VirtualBox)

Check all connected USB devices with:
```bash
lsusb
```
You should see your WLAN adapter in the list.

---

## Step 6: Install Realtek Driver
### Identify the Model Number
The model number should be **Realtek RTL8812AU**.
Run:
```bash
sudo apt install realtek-rtl88xxau-dkms
```

### Fix Missing Headers
If there are missing headers, update the sources list:
```bash
sudo nano /etc/apt/sources.list
```
Add the following line at the bottom:
```plaintext
deb https://mirrors.ocf.berkeley.edu/kali/ kali-rolling main contrib non-free non-free-firmware
```
Save and exit (**CTRL + X → Y → ENTER**).

---

## Step 7: Install Aircrack-ng Driver from GitHub
Clone the repository:
```bash
git clone https://github.com/aircrack-ng/rtl8812au.git
```
Navigate into the directory:
```bash
cd rtl8812au
```
Build the driver:
```bash
sudo make
```

### Resolve Missing Dependencies
If any dependencies are missing, download them from:
[**Kali Packages**](https://http.kali.org/kali/pool/main/l/linux/)

After dependencies are installed, complete the setup with:
```bash
sudo make install
```

---

## Final Step: Enable WiFi
After installation, you should now be able to detect and connect to WiFi networks.

By default, Kali Linux does not enable WiFi interfaces automatically. You can check available WiFi networks with:
```bash
iwconfig
