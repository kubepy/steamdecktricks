# blocknetwork

```
sudo cp /usr/bin/systemd-run /usr/local/bin/systemd-run2
sudo chmod u+s /usr/local/bin/systemd-run2
```

```
systemd-run2 --uid=1000 --gid=1000 --scope -p IPAddressAllow=localhost -p IPAddressDeny=any %command%
```

# steamdecktricks

```
DXVK_CONFIG="dxgi.maxDeviceMemory = 8192; dxgi.maxSharedMemory = 8192" %command%
```

`zh_CN.UTF-8`:
```
LANG=zh_CN.UTF-8 LC_CTYPE=zh_CN.UTF-8 LC_ALL=zh_CN.UTF-8 %command%
```

`zh_TW.UTF-8`:
```
LANG=zh_TW.UTF-8 LC_CTYPE=zh_TW.UTF-8 LC_ALL=zh_TW.UTF-8 %command%
```

`ja_JP.UTF-8`:
```
LANG=ja_JP.UTF-8 LC_CTYPE=ja_JP.UTF-8 LC_ALL=ja_JP.UTF-8 %command%
```

`PROTON_REMOTE_DEBUG_CMD` & `PRESSURE_VESSEL_FILESYSTEMS_RW` for multiple tasks running
```
PROTON_REMOTE_DEBUG_CMD="~/Documents/patch/Magical_Girl_Celesphonia_JP_Patch_v3.exe" PRESSURE_VESSEL_FILESYSTEMS_RW="~/Documents/patch/Magical_Girl_Celesphonia_JP_Patch_v3.exe" LANG=ja_JP.UTF-8 LC_CTYPE=ja_JP.UTF-8 LC_ALL=ja_JP.UTF-8 %command%
```

# steamdecktricks（long command)

`zh_CN.UTF-8`:
```
LANG=zh_CN.UTF-8 LANGUAGE=zh_CN:zh LC_CTYPE=zh_CN.UTF-8 LC_NUMERIC=zh_CN.UTF-8 LC_TIME=zh_CN.UTF-8 LC_COLLATE=zh_CN.UTF-8 LC_MONETARY=zh_CN.UTF-8 LC_MESSAGES=zh_CN.UTF-8 LC_PAPER=zh_CN.UTF-8 LC_NAME=zh_CN.UTF-8 LC_ADDRESS=zh_CN.UTF-8 LC_TELEPHONE=zh_CN.UTF-8 LC_MEASUREMENT=zh_CN.UTF-8 LC_IDENTIFICATION=zh_CN.UTF-8 LC_ALL=zh_CN.UTF-8 %command%
```

`zh_TW.UTF-8`:
```
LANG=zh_TW.UTF-8 LANGUAGE=zh_TW:zh LC_CTYPE=zh_TW.UTF-8 LC_NUMERIC=zh_TW.UTF-8 LC_TIME=zh_TW.UTF-8 LC_COLLATE=zh_TW.UTF-8 LC_MONETARY=zh_TW.UTF-8 LC_MESSAGES=zh_TW.UTF-8 LC_PAPER=zh_TW.UTF-8 LC_NAME=zh_TW.UTF-8 LC_ADDRESS=zh_TW.UTF-8 LC_TELEPHONE=zh_TW.UTF-8 LC_MEASUREMENT=zh_TW.UTF-8 LC_IDENTIFICATION=zh_TW.UTF-8 LC_ALL=zh_TW.UTF-8 %command%
```

`ja_JP.UTF-8`:
```
LANG=ja_JP.UTF-8 LANGUAGE=ja_JP:ja LC_CTYPE=ja_JP.UTF-8 LC_NUMERIC=ja_JP.UTF-8 LC_TIME=ja_JP.UTF-8 LC_COLLATE=ja_JP.UTF-8 LC_MONETARY=ja_JP.UTF-8 LC_MESSAGES=ja_JP.UTF-8 LC_PAPER=ja_JP.UTF-8 LC_NAME=ja_JP.UTF-8 LC_ADDRESS=ja_JP.UTF-8 LC_TELEPHONE=ja_JP.UTF-8 LC_MEASUREMENT=ja_JP.UTF-8 LC_IDENTIFICATION=ja_JP.UTF-8 LC_ALL=ja_JP.UTF-8 %command%
```

`PROTON_REMOTE_DEBUG_CMD` & `PRESSURE_VESSEL_FILESYSTEMS_RW` for multiple tasks running
```

PROTON_REMOTE_DEBUG_CMD="/home/deck/Documents/patch/Magical_Girl_Celesphonia_JP_Patch_v3.exe" PRESSURE_VESSEL_FILESYSTEMS_RW="/home/deck/Documents/patch/Magical_Girl_Celesphonia_JP_Patch_v3.exe" LANG=ja_JP.UTF-8 LANGUAGE=ja_JP:ja LC_CTYPE="ja_JP.UTF-8" LC_NUMERIC="ja_JP.UTF-8" LC_TIME="ja_JP.UTF-8" LC_COLLATE="ja_JP.UTF-8" LC_MONETARY="ja_JP.UTF-8" LC_MESSAGES="ja_JP.UTF-8" LC_PAPER="ja_JP.UTF-8" LC_NAME="ja_JP.UTF-8" LC_ADDRESS="ja_JP.UTF-8" LC_TELEPHONE="ja_JP.UTF-8" LC_MEASUREMENT="ja_JP.UTF-8" LC_IDENTIFICATION="ja_JP.UTF-8" LC_ALL="ja_JP.UTF-8" %command%
```

# steamdecktricks（env command)
```
sudo vim /etc/environment
```
```
JPN='LANG=ja_JP.UTF-8 LC_CTYPE=ja_JP.UTF-8 LC_ALL=ja_JP.UTF-8'
CNN='LANG=zh_CN.UTF-8 LC_CTYPE=zh_CN.UTF-8 LC_ALL=zh_CN.UTF-8'
TWN='LANG=zh_TW.UTF-8 LC_CTYPE=zh_TW.UTF-8 LC_ALL=zh_TW.UTF-8'
```

````
eval $(echo "$JPN %command%")
````
