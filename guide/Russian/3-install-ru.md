<img align="right" src="https://github.com/n00b69/woa-equuleus/blob/main/equuleus.png" width="350" alt="Windows 11 running on equuleus">

# Запуск Windows на Xiaomi Mi 8 Pro

## Установка Windows

### Требования
- [Образ mass storage](https://github.com/n00b69/woa-equuleus/releases/download/Files/msc.img)

- [Образ ARM Windows](https://arkt-7.github.io/woawin/)
  
- [Драйвера](https://github.com/n00b69/woa-equuleus/releases/tag/Drivers)

- [Devcfg исправления touch](https://github.com/n00b69/woa-equuleus/releases/download/Files/devcfg-polaris.img)

- [Образ UEFI](https://github.com/n00b69/woa-equuleus/releases/tag/UEFI)

### Загрузитесь в msc
> Замените `путь\к\msc.img` актуальным путём к образу msc
```cmd
fastboot boot путь\к\msc.img
```

#### Включите режим mass storage
> После загрузки в UEFI используйте кнопки регулировки громкости для навигации по меню и кнопку питания для подтверждения
- Выберите **UEFI Boot Menu**.
- Выберите **USB Attached SCSI (UAS) Storage**.
- Нажмите кнопку **питания** дважды чтобы подтвердить.

### Diskpart
> [!WARNING]
> НЕ УДАЛЯЙТЕ, НЕ СОЗДАВАЙТЕ И НЕ ИЗМЕНЯЙТЕ КАКИМ-ЛИБО ИНЫМ ОБРАЗОМ РАЗДЕЛЫ, НАХОДЯСЬ В DISKPART!!! ЭТО МОЖЕТ ПРИВЕСТИ К УДАЛЕНИЮ UFS ИЛИ НЕВОЗМОЖНОСТИ ЗАГРУЗКИ В FASTBOOT!!! ЭТО ОЗНАЧАЕТ, ЧТО ВАШЕ УСТРОЙСТВО БУДЕТ ОКИРПИЧЕНО БЕЗ КАКОГО-ЛИБО РЕШЕНИЯ! (за исключением доставки устройства в Xiaomi или его перепрошивки с помощью [EDL](edl-ru.md))
```cmd
diskpart
```

#### Выбрать раздел Windows 
> Используйте `list volume` чтобы найти его, замените `$` номером раздела **WINEQUULEUS**
```cmd
select volume $
``` 

#### Добавить букву к разделу Windows
```cmd
assign letter x
``` 

#### Выбрать раздел ESP
> Используйте `list volume` чтобы найти его, замените `$` номером раздела **ESPEQUULEUS**
```cmd
select volume $
``` 

#### Добавьте букву к ESP
```cmd
assign letter y
```

#### Выйти из diskpart
```cmd
exit
```

### Установка Windows
> [!Warning]
> НЕ ИСПОЛЬЗУЙТЕ 24H2!!!

> Замените `путь\к\install.esd` актуальным путём к install.esd (файл также может называться install.wim или 22631.2861.XXXXXXX.esd)
```cmd
dism /apply-image /ImageFile:путь\к\install.esd /index:6 /ApplyDir:X:\
```

> Если вы получите `Error 87`, проверьте индекс вышего образа используя `dism /get-imageinfo /ImageFile:путь\к\install.esd`, затем замените `index:6` действтельным индексом Windows 11 Pro в вашем образе

### Копирование вашего boot.img в Windows
- Перетащите **rooted_boot.img** на диск **WINEQUULEUS** в проводнике Windows, затем переименуйте его в **boot.img**.

### Установка драйверов
- Распакуйте пакет драйверов, затем откройте файл `OfflineUpdater.cmd` (Если появляется ошибка, запустите `OfflineUpdaterFix.cmd`)

> Введите букву диска **WINEQUULEUS** (должна быть **X**) затем нажмите Enter
  
#### Создать файлы загрузчика Windows
> Если возникнет какая-либо ошибка, например "Сбой при инициализации системного тома библиотеки", снова откройте `diskpart` и назначьте **ESPEQUULEUS** любую новую букву, затем замените букву `Y` в следующих командах на букву, которую вы только что добавили.
```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

#### Включение тестовой подпись
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" testsigning on
```

#### Отключите восстановление
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" recoveryenabled no
```

#### Отключите проверку целостности
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" nointegritychecks on
```

#### Удалите букву диска для ESP
> Если это не сработает, проигнорируйте это и перейдите к следующей команде. Этот фантомный диск исчезнет при следующей перезагрузке ПК.
```cmd
mountvol y: /d
```

### Перезагрузитесь в fastboot
> Удерживайте кнопку **уменьшение громкости** + **питание**, чтобы перезагрузить телефон в режим fastboot

#### Исправить touch
> Замените `путь\к\devcfg-equuleus.img` актуальным путём к образу
```cmd
fastboot flash devcfg_ab path\to\devcfg-equuleus.img
```

#### Загрузитесь в UEFI
> Замените `путь\к\equuleus-uefi.img` актуальным путём к образу UEFI
```cmd
fastboot boot путь\к\equuleus-uefi.img
```

### Перезагрузка в Android
Ваше устройство должно перезагрузиться само после +- 10 минут ожидания, после чего вы загрузитесь в Android для последнего шага.

## [Последний шаг: Настройка двойной загрузки](4-dualboot-ru.md)
