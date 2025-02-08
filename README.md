# Install Python with root access on Android emulators

Tutorials - how to install Python with root access on Android emulators

## Nox Player

[![Video 1](https://img.youtube.com/vi/99mOZ3nhG8I/0.jpg)](https://www.youtube.com/watch?v=99mOZ3nhG8I)


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

# output should look like (don't execute the commands yet!):
# rm -f /system/bin/su
# rm -f /system/xbin/su
```

### 3. Install [Magisk Kitsune](https://github.com/1q23lyc45/KitsuneMagisk)

```sh
nox_adb.exe -s 127.0.0.1:62025 install -g -t "%USERPROFILE%\Downloads\magisk_kitsune.apk"
```

### 4. Copy and paste the code from the [remount script](https://github.com/hansalemaos/install_python_on_android_emulators/blob/main/termux_remountscript.sh) and delete the sus that you found before

```sh

rm -f /system/bin/su
rm -f /system/xbin/su

```

### 5. Reboot

### 6. Install [Termux](https://github.com/termux/termux-app)

```sh
nox_adb.exe -s 127.0.0.1:62025 install -g -t "%USERPROFILE%\Downloads\termux-app_v0.118.1+github-debug_x86_64.apk"
```

### 7. Open and close Termux

### 8. Install [Termux boot](https://github.com/termux/termux-boot) (optional)

```sh
nox_adb.exe -s 127.0.0.1:62025 install -g -t "%USERPROFILE%\Downloads\termux-boot-app_v0.8.1+github.debug.apk"
```

### 9. Open and close Termux boot (optional)

### 10. Open Termux and write in your adb shell:

```sh
input text 'yes | pkg up;pkg install -y openssh;pkg install -y openssl;pkg install -y python';input keyevent KEYCODE_ENTER
```

### 11. Push the magisk modules to the sdcard

```sh
nox_adb.exe -s 127.0.0.1:62025 push "%USERPROFILE%\Downloads\termuxtoadb.zip" /sdcard
nox_adb.exe -s 127.0.0.1:62025 push "%USERPROFILE%\Downloads\make.writeable.zip" /sdcard

```
### 12. Install the Magisk modules [termuxtoadb](https://github.com/hansalemaos/termuxtoadb) and [make_writeable](https://github.com/hansalemaos/make_writeable)

### 13. Reboot

### 14. Run Python

```sh
nox_adb.exe -s 127.0.0.1:62025
python
```
***
***




