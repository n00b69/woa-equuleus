<img align="right" src="https://github.com/n00b69/woa-polaris/blob/main/polaris.png" width="350" alt="Windows 11 running on equuleus">

# Запуск Windows на Xiaomi Mi 8 Pro

## Переустановка Windows

### Требования
- [Образ mass storage](https://github.com/n00b69/woa-equuleus/releases/download/Files/msc.img)

- [Образ ARM Windows](https://arkt-7.github.io/woawin/)
  
- [Драйвера](https://github.com/n00b69/woa-equuleus/releases/tag/Drivers)

- [Образ UEFI](https://github.com/n00b69/woa-equuleus/releases/tag/UEFI)

### Загрузитесь в msc
> Замените `путь\к\msc.img` действительным путём к образу msc
```cmd
fastboot boot путь\к\msc.img
```

#### Включите режим mass storage
> После загрузки в UEFI используйте кнопки регулировки громкости для навигации по меню и кнопку питания для подтверждения
- Выберите **UEFI Boot Menu**.
- Выберите **USB Attached SCSI (UAS) Storage**.
- Нажмите кнопку **питания** дважды чтобы подтвердить.

### Diskpart
```cmd
diskpart
```

#### Выбрать раздел Windows 
> Используйте `list volume` чтобы найти его, замените `$` номером раздела **WIN8PRO**
```cmd
select volume $
``` 

#### Добавить букву к разделу Windows
```cmd
assign letter x
``` 

#### Выйдите из diskpart
```cmd
exit
```

#### Отформатируйте раздел Windows
> Перейдите в Проводник Windows > Этот компьютер и выберите **WIN8PRO**. Щелкните правой кнопкой мыши и отформатируйте как NTFS.

### Установка Windows
> Замените `путь\к\install.esd` актуальным путём к install.esd (файл также может называться install.wim или 22631.2861.XXXXXXX.esd)
```cmd
dism /apply-image /ImageFile:путь\к\install.esd /index:6 /ApplyDir:X:\
```

> Если вы получите `Error 87`, проверьте индекс вышего образа используя `dism /get-imageinfo /ImageFile:путь\к\install.esd`, затем замените `index:6` действтельным индексом Windows 11 Pro в вашем образе

### Установка драйверов
- Распакуйте пакет драйверов, затем откройте файл `OfflineUpdater.cmd` (Если появляется ошибка, запустите `OfflineUpdaterFix.cmd`)

> Введите букву диска **WIN8PRO** (должна быть **X**) затем нажмите Enter

### Загрузка в Windows
Перезагрузите телефон. Если в итоге он загрузится в Android, а не в Windows, перепрошейте UEFI заново с помощью WOA Helper.

#### Настройка Windows
> Сейчас Windows на вашем устройстве настроится. Это займёт некоторое время. В конечном итоге телефон перезагрузится, и после этого должна запуститься программа начальной установки (oobe).

> [!Tip]
> If this is your first time booting Windows and you wish to skip the Microsoft Account login, press the **I don't have internet** button in the WiFi page, then when prompted, press the **Continue with limited setup** button.

## Готово!











