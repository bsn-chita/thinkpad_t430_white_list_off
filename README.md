# Удаление белого списка оборудования на ноутбуке Thinkpad T430.

## Утилита модификации UEFI BIOS.
[UEFITool на github.com](https://github.com/LongSoft/UEFITool)

Для полноценной модификации (редактирования) BIOS необходимо использовать именно последнюю доступную версию без пометки NE (New Engine). На момент написания это была версия 0.28.0.

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

