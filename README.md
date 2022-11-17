# Gaming

### apk install
* [tmgp](https://imtt.dd.qq.com/sjy.20002/sjy.00001/16891/apk/55F5F988DB6EBA6CB4BFC507AC380F66.apk?fsname=com.tencent.tmgp.sgame_3.81.1.8_381010801.apk&hsr=4d5s)
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

* get process id
```
adb shell pidof com.tencent.tmgp.sgame
```

* Process status
```
adb shell ps -T (get all thread info)
```


* taskset
```
adb shell taskset -p [mask] [pid]
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
