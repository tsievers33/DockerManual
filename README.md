# Docker Handleiding

Tom Sievers

April 2023


# Inhoudsopgave

1. [Systeem setup benodigd voor Docker](#systeem-setup-benodigd-voor-docker)
2. [Installatie WSL2](#installatie-wsl2)
3. [Installatie Docker Desktop](#installatie-docker-desktop)
4. [Aan de slag met Docker en PHP](#aan-de-slag-met-docker-en-php)
5. [Aan de slag met Docker en C# .NET Core](#aan-de-slag-met-docker-en-c-net-core)
6. [Conclusie](#conclusie)

# Contents
Docker is een handig hulpmiddel waarmee je applicaties in zogenaamde "containers" kunt ontwikkelen, uitvoeren en delen. Dit maakt het gemakkelijker om je applicatie te laten werken op verschillende computers, omdat alles wat nodig is voor de applicatie in de container zit.

PHP en C\# zijn populaire programmeertalen die veel worden gebruikt voor het maken van websites en andere apps. In deze handleiding leer je hoe je Docker kunt gebruiken met PHP en C\#. Lees voor meer informatie over Docker en de mogelijkheden de volgende get-started handleiding: [https://docs.docker.com/get-started/](https://docs.docker.com/get-started/)

## Systeem setup benodigd voor Docker

**Virtualisatie**

Om Docker Desktop uit te kunnen voeren moet er een systeeminstelling wijzigen. Mogelijk staat deze al goed, dit kun je controleren door naar taakbeheer te gaan (Ctrl + Shift + Esc) en dan bij Prestaties -\> Processor te kijken naar 'Virtualisatie:'. Als dit op 'Ingeschakeld' staat ga dan door naar "Installatie Docker Desktop". Om virtualization in te schakelen moet een EUFI (BIOS) instelling gewijzigd worden, volg hiervoor het stappenplan hieronder.

Voor iets meer informatie zou je ook de Troubleshoot van Docker kunnen raadplegen: [https://docs.docker.com/desktop/troubleshoot/topics/#virtualization](https://docs.docker.com/desktop/troubleshoot/topics/#virtualization)

**EUFI benaderen**

Als je weet hoe je in je EUFI komt kun je dit stukje overslaan en daar direct heen gaan. Het benaderen van de firmware van je computer kan iets zijn wat niet altijd even makkelijk gaat. Gelukkig is er op Windows een manier om daar indirect heen te gaan. Zoek op 'Geavanceerde opstartopties' (of ga bij Instellingen naar Systeem -\> Systeemherstel) en klik (lees eerst wat je moet doen) op 'Nu Opnieuw Opstarten'. Je computer start opnieuw op en je komt in je EUFI terecht.

**EUFI instelling wijzigen**

1. Zodra je in de BIOS/UEFI-instellingen bent, zoek dan naar de virtualisatie-instellingen. Deze zijn vaak te vinden onder tabbladen zoals Advanced, Security of Processor. De specifieke naam varieert ook afhankelijk van het merk en model van je computer. De termen die je zoekt zijn iets in de trant van 'Virtualization Technology (VT)', 'Intel® Virtualization Technology', 'AMD-V' (voor AMD-processors), 'Virtualization Extensions' of 'Vanderpool'. Als je zoekt op je modelnummer en "how to enable virtualization" kun je het vaak wel vinden.
2. Schakel de virtualisatie-instelling in. Dit doe je meestal door de instelling te selecteren en vervolgens Enter te drukken, of door met de pijltjestoetsen te navigeren.
3. Nadat je de wijzigingen hebt aangebracht, vergeet dan niet om je BIOS/UEFI-instellingen op te slaan voordat je afsluit. Dit doe je meestal door naar het tabblad Exit te gaan en Save and Exit te selecteren, of door op F10 te drukken. Je computer zou dan opnieuw moeten opstarten met de nieuwe instellingen.

**Installatie WSL2**

Voor Windows 10/11 is het eerst belangrijk om WSL2 in te schakelen, als je dit al hebt of je hebt een ander besturingssysteem, dan kun je dit stuk overslaan.

1. Open PowerShell als beheerder. Hiervoor kun je de Windows zoekfunctie gebruiken, typ "PowerShell", rechtermuisklik op het resultaat en kies "Uitvoeren als beheerder".
2. Kopieer en plak de volgende commando's in de PowerShell:

dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

3. Zet WSL2 als de standaardversie met het volgende commando:

wsl --set-default-version 2

4. Herstart je computer om deze wijzigingen door te voeren.

**Installatie Docker Desktop**

Als de setup van het systeem gelukt is ga dan verder met het installeren van Docker Desktop volg de installatiehandleiding van jouw OS;

Linux: [https://docs.docker.com/desktop/install/linux-install/](https://docs.docker.com/desktop/install/linux-install/)

Mac: [https://docs.docker.com/desktop/install/mac-install/](https://docs.docker.com/desktop/install/mac-install/)

Windows: [https://docs.docker.com/desktop/install/windows-install/](https://docs.docker.com/desktop/install/windows-install/)


# Conclusie

Je hebt nu geleerd hoe je Docker kunt gebruiken op Windows, MacOS en Linux. Door Docker te combineren met deze programmeertalen, kun je gemakkelijker apps maken die op verschillende computers werken, wat handig is voor samenwerking en het delen van je werk. Je kan de Docker Images die je hebt gemaakt ook nog pushen naar de Docker Hub. Lees voor meer informatie over Docker de volgende get-started handleiding: [https://docs.docker.com/get-started/](https://docs.docker.com/get-started/)
