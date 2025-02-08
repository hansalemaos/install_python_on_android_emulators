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

### 3. Install [Magisk Kitsune](https://github.com/1q23lyc45/KitsuneMagisk) - Direct install (modify /system directly)

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

## BlueStacks5

[![Video 1](https://img.youtube.com/vi/tAFduUpmxnA/0.jpg)](https://www.youtube.com/watch?v=tAFduUpmxnA)


### [Download BlueStacks5 offline installer](https://support.bluestacks.com/hc/en-us/articles/4402611273485-BlueStacks-5-offline-installer)

### [Download Kitsune](https://github.com/hansalemaos/install_python_on_android_emulators/raw/refs/heads/main/magisk_kitsune.apk)

### [Download Termux](https://github.com/hansalemaos/install_python_on_android_emulators/raw/refs/heads/main/termux-app_v0.118.1+github-debug_x86_64.apk)

### [Download Termux Boot - optional](https://github.com/hansalemaos/install_python_on_android_emulators/raw/refs/heads/main/termux-boot-app_v0.8.1+github.debug.apk)

### [Download the Magisk module termuxtoadb](https://github.com/hansalemaos/termuxtoadb/raw/refs/heads/main/termuxtoadb.zip)

### [Download the Magisk module make_writeable](https://github.com/hansalemaos/make_writeable/raw/refs/heads/main/make.writeable.zip)


#### 1. Install BlueStacks 10 or 11

There are [instructions on the BlueStacks](https://support.bluestacks.com/hc/en-us/articles/4402611273485-BlueStacks-5-offline-installer) page to avoid crappy Nougat, e.g.

```sh
BlueStacksFullInstaller_5.21.650.1063_amd64_native.exe --defaultImageName Pie64 --imageToLaunch Pie64
```

```sh
BlueStacksFullInstaller_5.21.650.1063_amd64_native.exe --defaultImageName Rvc64 --imageToLaunch Rvc64
```

#### 2. Start the main instance and close it

#### 3. Create ONE NEW instance of the same version

#### 4. Install the Python lib [bluestacks5newinstances](https://github.com/hansalemaos/bluestacks5newinstances)

```py
# Create new instances from now on only using bluestacks5newinstances
# Below is an example of Android 11
# RUN THIS SCRIPT AS ADMIN!!!!

from bluestacks5newinstances import batch_create_bstacks_instances

# don't change the uppercase letters, they are going to be replaced by the script
newinstances_and_adbports = batch_create_bstacks_instances(
    newintancenametocreate_config=r'''bst.instance.Rvc64_NEWID.abi_list="x86,x64,arm,arm64"
bst.instance.Rvc64_NEWID.adb_port="ADBPORTNEW"
bst.instance.Rvc64_NEWID.ads_display_time=""
bst.instance.Rvc64_NEWID.airplane_mode_active="0"
bst.instance.Rvc64_NEWID.airplane_mode_active_time=""
bst.instance.Rvc64_NEWID.android_google_ad_id=""
bst.instance.Rvc64_NEWID.android_id="ANDROID_ID_NEW"
bst.instance.Rvc64_NEWID.android_sound_while_tapping="0"
bst.instance.Rvc64_NEWID.app_launch_count="0"
bst.instance.Rvc64_NEWID.astc_decoding_mode="software"
bst.instance.Rvc64_NEWID.autohide_notifications="0"
bst.instance.Rvc64_NEWID.boot_duration="-1"
bst.instance.Rvc64_NEWID.camera_device=""
bst.instance.Rvc64_NEWID.cpus="4"
bst.instance.Rvc64_NEWID.custom_resolution_selected="0"
bst.instance.Rvc64_NEWID.device_carrier_code="se_72405"
bst.instance.Rvc64_NEWID.device_country_code="076"
bst.instance.Rvc64_NEWID.device_custom_brand=""
bst.instance.Rvc64_NEWID.device_custom_manufacturer=""
bst.instance.Rvc64_NEWID.device_custom_model=""
bst.instance.Rvc64_NEWID.device_profile_code="sttu"
bst.instance.Rvc64_NEWID.display_name="Rvc64_NEWID"
bst.instance.Rvc64_NEWID.dpi="160"
bst.instance.Rvc64_NEWID.eco_mode_max_fps="5"
bst.instance.Rvc64_NEWID.enable_fps_display="0"
bst.instance.Rvc64_NEWID.enable_fullscreen_all_apps="0"
bst.instance.Rvc64_NEWID.enable_high_fps="0"
bst.instance.Rvc64_NEWID.enable_logcat_redirection="0"
bst.instance.Rvc64_NEWID.enable_notifications="0"
bst.instance.Rvc64_NEWID.enable_root_access="0"
bst.instance.Rvc64_NEWID.enable_vsync="0"
bst.instance.Rvc64_NEWID.fb_height="1280"
bst.instance.Rvc64_NEWID.fb_width="720"
bst.instance.Rvc64_NEWID.first_boot="1"
bst.instance.Rvc64_NEWID.game_controls_enabled="0"
bst.instance.Rvc64_NEWID.gl_win_height="-1"
bst.instance.Rvc64_NEWID.gl_win_screen=""
bst.instance.Rvc64_NEWID.gl_win_x="0"
bst.instance.Rvc64_NEWID.gl_win_y="0"
bst.instance.Rvc64_NEWID.google_account_logins=""
bst.instance.Rvc64_NEWID.google_login_popup_shown="0"
bst.instance.Rvc64_NEWID.graphics_engine="aga"
bst.instance.Rvc64_NEWID.graphics_renderer="gl"
bst.instance.Rvc64_NEWID.grm_ignored_rules=""
bst.instance.Rvc64_NEWID.launch_date=""
bst.instance.Rvc64_NEWID.libc_mem_allocator="jem"
bst.instance.Rvc64_NEWID.macro_win_height="-1"
bst.instance.Rvc64_NEWID.macro_win_screen=""
bst.instance.Rvc64_NEWID.macro_win_x="-1"
bst.instance.Rvc64_NEWID.macro_win_y="-1"
bst.instance.Rvc64_NEWID.max_fps="60"
bst.instance.Rvc64_NEWID.pin_to_top="0"
bst.instance.Rvc64_NEWID.ram="4096"
bst.instance.Rvc64_NEWID.show_sidebar="1"
bst.instance.Rvc64_NEWID.status.adb_port="5555"
bst.instance.Rvc64_NEWID.status.ip_addr_prefix_len="24"
bst.instance.Rvc64_NEWID.status.ip_gateway_addr="10.0.2.2"
bst.instance.Rvc64_NEWID.status.ip_guest_addr="10.0.2.15"
bst.instance.Rvc64_NEWID.status.session_id="0"
bst.instance.Rvc64_NEWID.vulkan_supported="1"''',
    newintancenametocreate="Rvc64",
    newtype_fastboot="Normal",
    newtype_root="Normal",
    newtype_data="Normal",
    numberofinstances=1,
)
print(newinstances_and_adbports)

# Examples for other Android versions can be found in the source code: https://github.com/hansalemaos/bluestacks5newinstances/blob/main/__init__.py

```

#### 5. Activate ADB in the BlueStacks options and find all su executables

```sh
# address might vary
adb.exe -s 127.0.0.1:5565 shell

# find all sus (disable windows file sharing before)
find / 2>/dev/null | grep "/su$" | awk '{print "rm -f "$0}'

# output should look like (don't execute the commands yet!):
# rm -f /system/xbin/su
# rm -f /system/xbin/bstk/su
# rm -f /data/downloads/.xb/su
# rm -f /data/downloads/.xb/bstk/su
# rm -f /boot/android/android/system/xbin/bstk/su
# rm -f /boot/android/dataFS/downloads/.xb/su
# rm -f /boot/android/dataFS/downloads/.xb/bstk/su
```

### 6. Install [Magisk Kitsune](https://github.com/1q23lyc45/KitsuneMagisk) - Direct install (modify /system directly)

```sh
adb.exe -s 127.0.0.1:5565 install -g -t "%USERPROFILE%\Downloads\magisk_kitsune.apk"
```

### 7. Copy and paste the code from the [remount script](https://github.com/hansalemaos/install_python_on_android_emulators/blob/main/termux_remountscript.sh) and delete the sus that you found before

```sh

rm -f /system/xbin/su
rm -f /system/xbin/bstk/su
rm -f /data/downloads/.xb/su
rm -f /data/downloads/.xb/bstk/su
rm -f /boot/android/android/system/xbin/bstk/su
rm -f /boot/android/dataFS/downloads/.xb/su
rm -f /boot/android/dataFS/downloads/.xb/bstk/su

```

### 8. Reboot

### 9. Install [Termux](https://github.com/termux/termux-app)

```sh
adb.exe -s 127.0.0.1:5565 install -g -t "%USERPROFILE%\Downloads\termux-app_v0.118.1+github-debug_x86_64.apk"
```

### 10. Open and close Termux

### 11. Install [Termux boot](https://github.com/termux/termux-boot) (optional)

```sh
adb.exe -s 127.0.0.1:5565 install -g -t "%USERPROFILE%\Downloads\termux-boot-app_v0.8.1+github.debug.apk"
```

### 12. Open and close Termux boot (optional)

### 13. Open Termux and write in your adb shell:

```sh
input text 'yes | pkg up;pkg install -y openssh;pkg install -y openssl;pkg install -y python';input keyevent KEYCODE_ENTER
```

### 14. Push the magisk modules to the sdcard

```sh
adb.exe -s 127.0.0.1:5565 push "%USERPROFILE%\Downloads\termuxtoadb.zip" /sdcard
adb.exe -s 127.0.0.1:5565 push "%USERPROFILE%\Downloads\make.writeable.zip" /sdcard

```
### 15. Install the Magisk modules [termuxtoadb](https://github.com/hansalemaos/termuxtoadb) and [make_writeable](https://github.com/hansalemaos/make_writeable)

### 16. Reboot

### 17. Run Python

```sh
nox_adb.exe -s 127.0.0.1:5565
python
```
***
***






