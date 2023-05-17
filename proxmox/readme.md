# PROXMOX
Zbiór instrukcji związanych z Proxmox

## [PL/ENG] Instalacja TrueNAS
[ENG] TrueNAS Core 12 Install and Basic Setup [Watch](https://www.youtube.com/watch?v=WjLaK8yQAag)
[PL] TrueNAS - własny serwer danych od podstaw [Oglądnij](https://www.youtube.com/watch?v=-wxi7mBJpWo)
[PL] Instrukcja instalacji TrueNAS razem z instrukcją podłączenia dysku do Maszyny Wirtualnej [Patrz niżej]
[ENG] How to run TrueNAS on Proxmox? [Watch](https://www.youtube.com/watch?v=M3pKprTdNqQ)
### [PL] Instrukcja 
1. Logujemy się do TrueNAS
2. W menu z lewej strony wybieramy Storage > Pools
3. Kilikamy przycisk "ADD" > "Create Pool"
4. Uwaga! Jeżeli, gdy pojawi się ostrzeżenie o tym, że dyski nie mają unikalnego numeru seryjnego
    Odznaczamy: [x] Show disks with non-unique serial numbers
> Warning: There are 3 disks available that have non-unique serial numbers. Non-unique serial numbers can be caused by a cabling issue and adding such disks to a pool can result in lost data.
5. Zaznaczamy podłączone dyski i klikamy: :arrow-right:
6. Wybieramy Stripe / Mirror / Raid-Z > Odznaczamy [x] Force > Potwierdzamy: [x] Confirm   
    - Jeśli wybieramy: **Stripe** wykorzystuje całą pojemność dysków do przechowywania i nie ma nadmiarowości. Uszkodzone lub zdegradowane dyski w pasku mogą spowodować utratę danych!
    > The current pool layout has these cautions:
    > - A stripe data vdev is highly discouraged and will result in data loss if it fails
    > - One or more data vdevs has disks of different sizes.
    > Create the pool with this layout?
    - Jeśli wybieramy: **Mirror** wymaga co najmniej dwóch dysków i tworzy kopię lustrzaną danych z jednego dysku na każdym innym dysku w vdev, co może ograniczyć całkowitą pojemność.
    > The current pool layout has these cautions:
    > - One or more data vdevs has disks of different sizes.
    > Create the pool with this layout?
    - Jeśli wybieramy: **Raid-Z** oferują różne proporcje redundancji danych i całkowitej pojemności wybranych dysków.
    > Ostrzeżenie jak dla **Mirror** 

> Mixing disks of different sizes in a vdev is not allowed. 
> Caution: A stripe data vdev is highly discouraged and will result in data loss if it fails

7. Nadajemy nazwę w polu Name
8. Klikamy: "Create" 
9. Potwierdzamy informację o **wyczyszczeniu dysków** [ ] Confirm > Klikamy: "CREATE POOL"
    The contents of all added disks will be erased.

## [PL] Nowy Dysk w Linux
[PL] Zarządzanie dyskami w systemach GNU/Linux (Część I) - zagadnienia podstawowe [Oglądnij](https://www.youtube.com/watch?v=B7AVlP4GpZQ)

## [PL/ENG] Podłączenie partycji dysku do maszyny wirtualnej na proxmox
[PL] PROXMOX - Podłączenie dysku fizycznego do Maszyny Wirtualnej (VM) na przykładzie FreeNAS [Oglądnij](https://www.youtube.com/watch?v=31bSvxg-uAY)
    - Instrukcja instalacji TrueNAS razem z instrukcją podłączenia dysku do Maszyny Wirtualnej
[ENG] Passthrough Physical Disk to Virtual Machine (VM) [Instruction](https://pve.proxmox.com/wiki/Passthrough_Physical_Disk_to_Virtual_Machine_(VM))

 ### [PL] Instrukcja podłączenia dysku do maszyny wirtualnej
1. Szukamu nr seryjnego dysku - serial
2. Szukamy id dysku
3. Podłączenie dysku do maszyny wirtualnej
```
lshw -class disk -class storage
ls -l /dev/disk/by-id/ | grep <numer_seryjny>
qm set <nr_maszyny_wirtualnej> -scsi<kolejny_nr> /dev/disk/by-id/<id_dysku>
```

## [PL/ENG] Instalacja i konfiguracja Plex
[ENG] TrueNAS Core 12 Plex Plugin Install and Setup [Watch](https://www.youtube.com/watch?v=looBzNEtjDQ)

### [PL] Instrukcja Instalacji i konfiguracji Plex 
1. Logujemy się do TrueNAS
2. w menu z lewej strony wybieramy Storage > Pools
3. Klikamy trzy kropki po prawej stronie > "Add Dataset" 
4. Nadajemy nazwę > Klikamy "CREATE" z podstawowymi ustawieniami
5. Tworzymy użytkowników: 
    - w menu z lewej strony wybieramy Accounts > Users
    > All built-in users except root are hidden by default. Use the gear icon (top-right) to toggle the display of built-in users.
    - Klikamy "ADD" > Uzupełniamy: "Full Name" | "Username" | "Password" | "Confirm Password" > Klikamy "SUBMIT"
6. Tworzymy grupę użytkowników 
    - w menu z lewej strony wybieramy Accounts > Groups
    - Klikamy "ADD" > Uzupełniamy: "Name" > Klikamy "SUBMIT"
7. Dodajemy użytkowników do grupy: Klikamy :arrow_down_small: > "MEMBERS" > Wybieramy użytkowników > :arrow_right: > "SAVE"
8. W menu z lewej strony "Sharing" > "Windows Shares (SMB)"  > "ADD"
    - wybieramy ścieżkę dostępu > "SUBMIT"
    > Enable this service to start automatically.
    - Configure ACL Klikamy: "CONFIGURE NOW" > [x] Create a costume ACL > "CONTINUE" 
     - "Group" > [x] Apply Group 
     - owner@ :arrow_right: "Perrmision Type: Basic" > "Permissions: Full Control" > "Flags: Inherit"
     - group@ :arrow_right: "Perrmision Type: Basic" > "Permissions: Full Control" > "Flags: Inherit"
     - Klikamy "SAVE"
9. Udostępniamy pliki:
    - W eksploatorze plików wpisujemy adres IP maszyny z TruNAS \\10.1.2.102 
        - odajemy login i hasło użytkownika 
        - wklejamy pliki
10. Instalujemy Plex
    - wchodzimy na stronę TrueNAS i w menu z lewej strony wybieramy Plugins
