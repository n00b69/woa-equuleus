<img align="right" src="https://github.com/n00b69/woa-equuleus/blob/main/equuleus.png" width="350" alt="Windows 11 running on equuleus">

# Запуск Windows на Xiaomi Mi 8 Pro

## Обновление драйверов 

### Требования
- [Образ mass storage](https://github.com/n00b69/woa-equuleus/releases/download/Files/msc.img)

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [Образ UEFI](https://github.com/n00b69/woa-equuleus/releases/tag/UEFI)

- [Драйвера](https://github.com/n00b69/woa-equuleus/releases/tag/Drivers)

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
```cmd
diskpart
```

#### Выбрать раздел Windows 
> Используйте `list volume` чтобы найти его, замените `$` номером раздела **WINEQUULEUS**
```diskpart
select volume $
```

#### Добавить букву к разделу Windows
```cmd
assign letter X
```

### Выйти из diskpart
```cmd
exit
```

### Установка драйверов 
> [!Note]
> Этот процесс займёт +- 20 минут. Не волнуйтесь, это нормально.

- Распакуйте пакет драйверов, затем откройте файл `OfflineUpdater.cmd` (Если появляется ошибка, запустите `OfflineUpdaterFix.cmd`)

> Введите букву диска **WINEQUULEUS** (должна быть **X**) затем нажмите Enter

### Reboot your device
> Не забудьте также заменить образ UEFI в Android, иначе вы можете столкнуться с "синим экраном смерти" (BSoD) при последующей загрузке в Windows.
```cmd
adb reboot
```

## Готово!












