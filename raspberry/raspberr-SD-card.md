# SD卡操作

## 恢复SD分区
----
### window dos下操作
```shell
## ctrl + R, 运行diskpart
diskpart

## 进入diskpart后，执行 list disk
DISKPART> list disk

  磁盘 ###  状态           大小     可用     Dyn
  --------  -------------  -------  -------  ---
  磁盘 0    联机              465 GB  2048 KB
  磁盘 1    联机               22 GB      0 B
  磁盘 2    联机               14 GB  3072 KB

## 选择要要恢复的盘
DISKPART> select disk 2

磁盘 2 现在是所选磁盘。


## 执行清除命令 clean
DISKPART> clean

DiskPart 成功地清除了磁盘。

## 再次确认是否清除了
DISKPART> list disk

  磁盘 ###  状态           大小     可用     Dy
  --------  -------------  -------  -------  --
  磁盘 0    联机              465 GB  2048 KB
  磁盘 1    联机               22 GB      0 B
* 磁盘 2    联机               14 GB    14 GB

## 我的电脑-管理-磁盘管理-选择磁盘并新加卷
```