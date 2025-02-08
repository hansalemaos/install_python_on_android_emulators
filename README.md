# Install Python with root access on Android emulators

Tutorials - how to install Python with root access on Android emulators

## Nox Player

### [Download Nox Player](https://support.bignox.com/en/win-release)

### [Download Kitsune](https://github.com/hansalemaos/install_python_on_android_emulators/raw/refs/heads/main/magisk_kitsune.apk)

### [Download Termux](https://github.com/hansalemaos/install_python_on_android_emulators/raw/refs/heads/main/termux-app_v0.118.1+github-debug_x86_64.apk)

### [Download Termux Boot - optional](https://github.com/hansalemaos/install_python_on_android_emulators/raw/refs/heads/main/termux-boot-app_v0.8.1+github.debug.apk)

### [Download the Magisk module termuxtoadb](https://github.com/hansalemaos/termuxtoadb/raw/refs/heads/main/termuxtoadb.zip)

### [Download the Magisk module make_writeable](https://github.com/hansalemaos/make_writeable/raw/refs/heads/main/make.writeable.zip)



#### 1. Enable Root on your emulator

#### 2. Find all su executables

```sh
cd "C:\Program Files (x86)\Nox\bin"

# get the ip:port of your emulator - 127.0.0.1:62025 in my case
nox_adb.exe devices -l

nox_adb.exe -s 127.0.0.1:62025 shell

# find all sus
find / 2>/dev/null | grep "/su$" | awk '{print "rm -f "$0}'

# output should look like:

rm -f /system/bin/su
rm -f /system/xbin/su
```

### 3. Install Kitsune 

```sh
nox_adb.exe -s 127.0.0.1:62025 install -g -t "%USERPROFILE%\Downloads\magisk_kitsune.apk"
```

### 4. Copy 


### 3. Install Termux

```sh
nox_adb.exe -s 127.0.0.1:62025 install -g -t "%USERPROFILE%\Downloads\termux-app_v0.118.1+github-debug_x86_64.apk"
```

### 4. Open and close Termux

### 5. Install Termux boot (optional)

```sh
nox_adb.exe -s 127.0.0.1:62025 install -g -t "%USERPROFILE%\Downloads\termux-boot-app_v0.8.1+github.debug.apk"
```

### 5. Open and close Termux boot (optional)

### 6. Open Termux and write in your adb shell:

```sh
input text 'yes | pkg up;pkg install -y openssh;pkg install -y openssl;pkg install -y python';input keyevent KEYCODE_ENTER
```

### 7. Push the magisk module to the 





