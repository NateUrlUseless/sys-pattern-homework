# Домашнее задание к занятию "`Уязвимости и атаки на информационные системы`" - `Вангер А.Ю.`
### Задание 1 
Установим ecryptfs в ВМ

```
apt install ecryptfs-utils cryptsetup -y
```

Добавим пользователя cryptouser:

```
sudo adduser cryptouser
su - cryptouser
```

![1](https://github.com/NateUrlUseless/sys-pattern-homework/blob/main/img/111.png)

Зашифруем содержимое каталога:

```
sudo ecryptfs-migrate-home -u cryptouser
sudo ls -la /home/cryptouser
```

![2](https://github.com/NateUrlUseless/sys-pattern-homework/blob/main/img/333.png)
### Задание 2 

Установим поддержку luks:

```
sudo apt install cryptsetup -y
```

![3](https://github.com/NateUrlUseless/sys-pattern-homework/blob/main/img/444.png)

Создадим новый раздел размером 100 МБ с помощью утилиты gparted:

```
sudo apt install gparted -y
sudo gparted
```
![4](https://github.com/NateUrlUseless/sys-pattern-homework/blob/main/img/666.png)

Зададим тип файловой системы - luks2 для раздела /dev/sdb1:

```
sudo cryptsetup -y -v --type luks2 luksFormat /dev/sdb1
```

![5](https://github.com/NateUrlUseless/sys-pattern-homework/blob/main/img/777.png)

Смонтируем раздел:
```
sudo cryptsetup luksOpen /dev/sdb1 luks_disk
ls /dev/mapper/disk
```

![6](https://github.com/NateUrlUseless/sys-pattern-homework/blob/main/img/888.png)

Отформатируем раздел:

```
sudo dd if=/dev/zero of=/dev/mapper/luks_disk
sudo mkfs.ext4 /dev/mapper/luks_disk
```

Монтирование открытого раздела:

```
mkdir .secret
sudo mount /dev/mapper/luks_disk .secret/
```
