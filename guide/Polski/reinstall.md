<img align="right" src="https://github.com/n00b69/woa-equuleus/blob/main/equuleus.png" width="350" alt="Windows 11 running on equuleus">

# Windows na Xiaomi Mi 8 Pro

## Ponowna instalacja Windows

### Wymagania
- [Obraz UEFI](https://github.com/n00b69/woa-equuleus/releases/tag/UEFI)

- [Windows na ARM](https://worproject.com/esd)

- [Sterowniki](https://github.com/n00b69/woa-equuleus/releases/tag/Drivers)

### Uruchom do UEFI
> Zastąp `path\to\equuleus-uefi.img` rzeczywistą ścieżką obrazu UEFI
```cmd
fastboot boot path\to\equuleus-uefi.img
```

#### Włączanie trybu pamięci masowej
> Po uruchomieniu systemu UEFI użyj przycisków głośności do poruszania się po menu i przycisku zasilania, aby potwierdzić
- Wybierz **UEFI Boot Menu**.
- Wybierz **USB Attached SCSI (UAS) Storage**.
- Naciśnij przycisk dwa razy aby potwierdzić.

### Diskpart
```cmd
diskpart
```

#### Wybieranie partycji Windows
> Wpisz `list Volume`, aby ją znaleźć, zamień `$` na rzeczywistą liczbę **WIN8PRO**
```diskpart
select volume $
```

#### Dodanie litery do systemu Windows
```cmd
assign letter x
```

#### Wyjdź z Diskpart
```cmd
exit
```

#### Formatting Windows
> Go to Windows Explorer > This PC and select **WIN8PRO**. Right click and format as NTFS.

### Installing Windows
> Zamień `ścieżka\do\install.esd` na rzeczywistą ścieżkę do pliku install.esd (może on również nosić nazwę install.wim lub 22631.2861.XXXXXXX.esd)
```cmd
dism /apply-image /ImageFile:ścieżka\do\install.esd /index:6 /ApplyDir:X:\
```

> Jeśli pojawi się komunikat `Błąd 87`, sprawdź indeks obrazu za pomocą polecenia `dism /get-imageinfo /ImageFile:ścieżka\do\install.esd`, a następnie zastąp `index:6` rzeczywistym numerem indeksu systemu **Windows 11 Pro** w Twoim obrazie

### Instalowanie sterowników
- Wypakuj archiwum ze sterownikami, a następnie otwórz plik `OfflineUpdater.cmd` (jeśli pojawi się błąd, otwórz `OfflineUpdaterFix.cmd`)
 
> Jeśli poprosi Cię o podanie litery, wpisz literę dysku **WIN8PRO** (którą powinna być **X**), a następnie naciśnij enter.

### Uruchom do Androida
Uruchom ponownie telefon. Jeśli zamiast systemu Windows wylądujesz w systemie Android, ponownie wykonaj flashowanie UEFI za pomocą WOA Helper.

#### Konfiguracja Windowsa
> Twoje urządzenie skonfiguruje teraz system Windows. To zajmie trochę czasu. W końcu uruchomi się ponownie, a następnie powinna rozpocząć się konfiguracja wstępna (oobe).

> [!Tip]
> If this is your first time booting Windows and you wish to skip the Microsoft Account login, press the **I don't have internet** button in the WiFi page, then when prompted, press the **Continue with limited setup** button.

## Skończone!
















