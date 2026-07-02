# Tina5SDK 527 

包含：`repo status` 中实际新增/修改的源码、配置、下载包、固件包；未追踪目录完整展开复制。

排除：`out/`、`bak/`、`project/`、`a133-tina-aidesktop/`、`tools/OpenixCLI/`、`tools/serial_agent/`、`prebuilt/rootfsbuilt/`、`.local_patch/`、编译缓存目录。

注意：`openwrt/target/` 和 `openwrt/openwrt/target/` 是源码配置目录，不按缓存排除。

使用：
```sh
scripts/apply_overlay.sh /path/to/TinaSDK
# 审查 meta/delete_list.txt 后，如需删除：
scripts/apply_deletes.sh /path/to/TinaSDK
```
