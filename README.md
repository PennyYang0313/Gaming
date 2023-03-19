# Gaming

### apk install
* [王者榮耀 tmgp](https://imtt.dd.qq.com/sjy.20002/sjy.00001/16891/apk/55F5F988DB6EBA6CB4BFC507AC380F66.apk?fsname=com.tencent.tmgp.sgame_3.81.1.8_381010801.apk&hsr=4d5s)
```
cd /path/to/Download/Folder
adb install com.tencent.tmgp.sgame_3.81.1.8_381010801.apk
```
   * login
      *  [Wechat](http://weixin.qq.com/)
      ```
      cd /path/to/Download/Folder
      adb install weixin8028android2240_arm64.apk
      ```
* [傳說對決 kgtw](https://m.apkpure.com/tw/garena-%E5%82%B3%E8%AA%AA%E5%B0%8D%E6%B1%BA%EF%BC%9A%E5%85%AD%E9%80%B1%E5%B9%B4%E7%89%88%E6%9C%AC/com.garena.game.kgtw/download?from=details)
```
cd /path/to/Download/Folder
adb install "Garena 傳說對決：六週年版本_1.47.1.1_Apkpure.apk"
```
   * login
      * [FB](https://d.apkpure.com/b/APK/com.facebook.katana?version=latest)
      ```
      cd /path/to/Download/Folder
      adb install Facebook_393.0.0.34.106_Apkpure.apk
      ```
### get info
* get process id
```
adb shell pidof com.tencent.tmgp.sgame
adb shell pidof com.garena.game.kgtw
```

* Process status
```
adb shell ps -T (get all thread info)
```

* get package name
```
adb shell pm list packages -f
```

### control
* taskset
```
(only process)       adb shell taskset -p [mask] [pid]
(process all thread) adb shell taskset -ap [mask] [pid]
```
* 調整上下限頻率
```
adb shell "chmod 660 /sys/devices/system/cpu/cpufreq/policy0/scaling_min_freq"
adb shell "chmod 660 /sys/devices/system/cpu/cpufreq/policy0/scaling_max_freq"
adb shell "echo 0 > /sys/devices/system/cpu/cpufreq/policy0/scaling_min_freq"
adb shell "echo 99999999 > /sys/devices/system/cpu/cpufreq/policy0/scaling_max_freq"
adb shell "echo sugov_ext > /sys/devices/system/cpu/cpufreq/policy0/scaling_governor"
adb shell "echo performance > /sys/devices/system/cpu/cpufreq/policy0/scaling_governor"
```
* 定頻
```
adb shell "chmod 660 /sys/devices/system/cpu/cpufreq/policy0/scaling_min_freq"
adb shell "chmod 660 /sys/devices/system/cpu/cpufreq/policy0/scaling_max_freq"
adb shell "echo [freq] > /sys/devices/system/cpu/cpufreq/policy0/scaling_min_freq"
adb shell "echo [freq] > /sys/devices/system/cpu/cpufreq/policy0/scaling_max_freq"
adb shell "chmod 440 /sys/devices/system/cpu/cpufreq/policy0/scaling_min_freq"
adb shell "chmod 440 /sys/devices/system/cpu/cpufreq/policy0/scaling_max_freq"
```


### simpleperf
```
adb shell simpleperf stat --use-devfreq-counters -p [pid] --duration [second]
adb shell simpleperf stat --use-devfreq-counters -t [tid] --duration [second]
```
* --per-core

### systrace
* [linux](https://dl.google.com/android/repository/platform-tools_r33.0.0-linux.zip)
* [Windows](https://dl.google.com/android/repository/platform-tools_r33.0.0-windows.zip)
#### 環境 (for windows)
* [python 2.7](https://www.python.org/downloads/release/python-2718/)
* [pywin](https://pypi.org/project/pypiwin32/219/#files)
```
cd /path/to/systrace/folder/
python systrace.py -t [time] 
```

### [perfetto](https://developer.android.com/studio/command-line/perfetto) 
* [UI](https://ui.perfetto.dev/)

* record_android_trace (for windows)
  * 下載
  ```
  curl -O https://raw.githubusercontent.com/google/perfetto/master/tools/record_android_trace
  ```
  * 執行
  ```
  python3 record_android_trace -o trace_file.perfetto-trace -t 10s -b 32mb \ sched freq idle am wm gfx view binder_driver hal dalvik camera input res memory 
  ```
* ADB Shell
```
adb push perfetto_config.pbtx data/misc/perfetto-traces/
adb shell perfetto --txt -c data/misc/perfetto-traces/perfetto_config.pbtx -o data/misc/perfetto-traces/trace_file.perfetto-trace
adb pull /data/misc/perfetto-traces/trace_file.perfetto-trace
```
