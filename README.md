1. Скачайте архив:

Перейдите на официальную страницу релизов [LongSoft/UEFITool Releases ](https://github.com/LongSoft/UEFITool/releases) и выберите файл UEFIPatch_0.28.0_linux_x86_64.zip.
```bash
wget https://github.com/LongSoft/UEFITool/releases/download/0.28.0/UEFIPatch_0.28.0_linux_x86_64.zip
```
2. Распакуйте и подготовьте файл:

```bash
unzip UEFIPatch_0.28.0_linux_x86_64.zip
chmod +x UEFIPatch
```

3. Использование

Для работы утилиты в одной папке с ней должны находиться:
- исполняемый файл UEFIPatch.
- дамп BIOS
- файл со списком патчей patches.txt

4. Команда для установки патча
```bash
./UEFIPatch bios_backup.bin patches.txt -o patched_bios.bin
```


79E0EDD7-9D1D-4F41-AE1A-F896169E5216 10 P:C8390F0F84:C8390F90E9
79E0EDD7-9D1D-4F41-AE1A-F896169E5216 10 P:C8390F7516:C8390F7500
79E0EDD7-9D1D-4F41-AE1A-F896169E5216 10 P:C8394F0474:C8394F04EB

Пробелы в конце строк и пустая строка в конце файла.

```bash
echo "79E0EDD7-9D1D-4F41-AE1A-F896169E5216 10 P:C8390F0F84:C8390F90E9 " > whitelist_only.txt
echo "79E0EDD7-9D1D-4F41-AE1A-F896169E5216 10 P:C8390F7516:C8390F7500 " >> whitelist_only.txt
echo "79E0EDD7-9D1D-4F41-AE1A-F896169E5216 10 P:C8394F0474:C8394F04EB " >> whitelist_only.txt
```




# Удаление белого списка оборудования на ноутбуке Thinkpad T430.

## Подготовительный этап

Создадим каталог для работы
```bash
mkdir ~/UEFI
```

Перейдем в него
```bash
cd ~/UEFI
```

### Утилита модификации UEFI BIOS.

Для модификации потребуется утилита [UEFIPatch из пакета UEFITool(github.com)](https://github.com/LongSoft/UEFITool). При чем необходимо использовать последнюю доступную версию без пометки NE (New Engine). На момент написания это была версия 0.28.0.

Создадим для UEFIPatch свой каталог
```bash
mkdir UEFIPatch_0_28_0
```
Перейдем в него и скопируем в него архив с UEFIPatch
```bash
wget https://github.com/LongSoft/UEFITool/releases/download/0.28.0/UEFIPatch_0.28.0_linux_x86_64.zip
```

Разархивируем содержимое архива:
```bash
unzip UEFIPatch_0.28.0_linux_x86_64.zip
```

И сделаем файл UEFIPatch исполняемым:
```bash
chmod +x UEFIPatch
```

Созданим файл модификатор для UEFIPatch
```bash
echo "79E0EDD7-9D1D-4F41-AE1A-F59E9B451396 10 P:410084C0751032C0:410084C0EB1032C0" > patches_thinkpad_t430.txt
```
Важно чтобы в конце файла была пустая строка.

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




```bash
```


```bash
```

```bash
```

```bash
```
https://github.com/thrimbor/thinkpad-uefi-sign
Записываем биос обратно(4мб)
```bash
sudo flashrom -p ch341a_spi -w bios_2_81_4mb_patched.bin
```
