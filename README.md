# blocknetwork

```
sudo cp /usr/bin/systemd-run /usr/local/bin/systemd-run2
sudo chmod u+s /usr/local/bin/systemd-run2
```

```
systemd-run2 --uid=1000 --gid=1000 --scope -p IPAddressAllow=localhost -p IPAddressDeny=any %command%
```

# blocknet.sh  （enter the game then run script to block network)

```
sudo cp /usr/bin/systemd-run /usr/local/bin/systemd-run2
sudo chmod u+s /usr/local/bin/systemd-run2
```

```
systemd-run2 --uid=1000 --gid=1000 --scope %command%
```

```
$ cat ./blocknet.sh 
#!/bin/bash
#set -x

SUDO_PASSWORD=3389

SCOPE_NAME=$(echo $SUDO_PASSWORD | sudo -S systemctl list-units "run-p*.scope" --state=running --no-legend | awk '{print $1}')

if [ -z "$SCOPE_NAME" ]; then
    echo "Scope Not Found"
    exit 1
fi

IS_BLOCKED=$(systemctl show "$SCOPE_NAME" -p IPAddressDeny --value)

if [ "$IS_BLOCKED" == "" ]; then
    echo $SUDO_PASSWORD | sudo -S systemctl set-property "$SCOPE_NAME" IPAddressAllow=localhost IPAddressDeny=any
    echo ">>> systemctl set-property "$SCOPE_NAME" IPAddressAllow=localhost IPAddressDeny=any"
else
    echo $SUDO_PASSWORD | sudo -S systemctl set-property "$SCOPE_NAME" IPAddressAllow= IPAddressDeny=
    echo ">>> systemctl set-property "$SCOPE_NAME" IPAddressAllow= IPAddressDeny="
fi

exit 0
```

# isolate_home

```
./isolate_home.sh 1548510
```

```
#!/bin/bash
#set -x

APPID=$1

if [ -z "$APPID" ]; then
    echo "使用方法: $0 <AppID>"
    exit 1
fi

TARGET_DIR="$HOME/.local/share/Steam/steamapps/compatdata/$APPID/pfx/dosdevices"

if [ ! -d "$TARGET_DIR" ]; then
    echo "错误: 目录 $TARGET_DIR 不存在。"
    exit 1
fi

echo "正在处理 AppID: $APPID 的驱动器映射（强制创建全量映射）..."

cd "$TARGET_DIR" || exit

# 遍历 a 到 z
for letter in {a..z}; do
    # 绝对不能动 C 盘，否则 Proton 环境会损坏
    if [ "$letter" == "c" ]; then
        continue
    fi

    # 1. 处理单冒号映射 (例如 d:)
    # 强制删除（无论是否存在，无论是文件还是死链接）
    rm -f "${letter}:"
    # 统一创建指向 ../drive_c 的软链接
    ln -s "../drive_c" "${letter}:"

    # 2. 处理双冒号映射 (例如 d::)
    rm -f "${letter}::"
    ln -s "../drive_c" "${letter}::"

    echo "已强制映射: ${letter}: 和 ${letter}:: -> ../drive_c"
done

echo "完成！现在除了 c: 以外，所有 a-z 的盘符都已指向 ../drive_c。"
```

# remove isolate_home

```
./isolate_home_rm.sh 1548510
```

```
#!/bin/bash
#set -x

APPID=$1

if [ -z "$APPID" ]; then
    echo "使用方法: $0 <AppID>"
    exit 1
fi

TARGET_DIR="$HOME/.local/share/Steam/steamapps/compatdata/$APPID/pfx/dosdevices"

if [ ! -d "$TARGET_DIR" ]; then
    echo "错误: 目录 $TARGET_DIR 不存在。"
    exit 1
fi

echo "正在还原 AppID: $APPID 的驱动器映射 (清理多余快捷方式)..."

cd "$TARGET_DIR" || exit

# 遍历 a 到 z
for letter in {a..z}; do
    # 绝对不要删除 c:，它是系统盘
    if [ "$letter" == "c" ]; then
        continue
    fi

    # 删除单冒号快捷方式 (如 a:, b:, d: ...)
    if [ -L "${letter}:" ]; then
        rm "${letter}:"
        echo "已删除快捷方式: ${letter}:"
    fi

    # 删除双冒号快捷方式 (如 a::, b::, d:: ...)
    if [ -L "${letter}::" ]; then
        rm "${letter}::"
        echo "已删除快捷方式: ${letter}::"
    fi
done

echo "清理完成！Proton 将在下次启动游戏时恢复默认映射。"
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
