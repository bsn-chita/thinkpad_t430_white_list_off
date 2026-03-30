# Удаление белого списка оборудования на ноутбуке Thinkpad T430.

## Утилита модификации UEFI BIOS.
[UEFITool на github.com](https://github.com/LongSoft/UEFITool)

Для полноценной модификации (редактирования) BIOS необходимо использовать последнюю доступную версию без пометки NE (New Engine). На момент написания это была версия 0.28.0.

Копируем на компьютер утилиту UEFIPatch:

```bash
wget https://github.com/LongSoft/UEFITool/releases/download/0.28.0/UEFIPatch_0.28.0_linux_x86_64.zip
```

Разархивируем:
```bash
unzip UEFIPatch_0.28.0_linux_x86_64.zip
```

Делаем файл UEFIPatch исполняемым:
```bash
chmod +x UEFIPatch
```

## Backup BIOS с помощью программатора

Биос на thinkpad t430 хранится в двух микросхемах 4мб + 8мб(12мб)
Непосредственно биос хранится в микросхеме 4мб.
Алгоритм чтения биос: два раза прочитать, сравнить, переименовать и сохранить как валидную копию.

```bash
sudo flashrom -p ch341a_spi -r bios_2_81_4mb_1.bin
sudo flashrom -p ch341a_spi -r bios_2_81_4mb_2.bin
md5sum bios_2_81_4mb_1.bin bios_2_81_4mb_2.bin
cp bios_2_81_4mb_1.bin bios_2_81_4mb_backup.bin
```

То же самое делаем со второй микросхемой

```bash
sudo flashrom -p ch341a_spi -r bios_2_81_8mb_1.bin
sudo flashrom -p ch341a_spi -r bios_2_81_8mb_2.bin
md5sum bios_2_81_8mb_1.bin bios_2_81_8mb_2.bin
cp bios_2_81_8mb_1.bin bios_2_81_8mb_backup.bin
```
Далее получаем полный биос
```bash
дописать получение полного при чем порядок влияет
```

создание файла модификатора для UEFIPatch
```bash
echo "79E0EDD7-9D1D-4F41-AE1A-F59E9B451396 10 P:410084C0751032C0:410084C0EB1032C0" > patches_thinkpad_t430.txt
```



```bash
```


```bash
```

```bash
```

```bash
```

```bash
```
