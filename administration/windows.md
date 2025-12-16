# Windows

## Reset pass with phys access

если битлокера нет, то загружаемся с установочной убунты

```bash
blkid # находим здесь устройтсво с TYPE=ntfs
ntfsfix -d /dev/disk # фиксим лок файлы и тд
mount -t ntfs-3g -o remove_hiberfile /dev/disk /mnt/win
cd /mnt/win/Windows/System32/config
sudo chntpw -l SAM 
sudo chntpw -u "admin-name" SAM
```
