# Docker Handleiding

Tom Sievers

Augustus 2023

# Contents


Docker is een handig hulpmiddel waarmee je apps in zogenaamde"containers" kunt ontwikkelen, uitvoeren en delen. Dit maakt het gemakkelijker om je app te laten werken op verschillende computers, omdat alles wat nodig is voor de app in de containerzit.

PHP en C\# zijn populaire programmeertalen die veel worden gebruikt voor het maken van websites en andere apps. In deze handleiding leer je hoe je Docker kunt gebruiken met PHP en C\#. Lees voor meer informatie over Docker en de mogelijkheden de volgende get-started handleiding: [https://docs.docker.com/get-started/](https://docs.docker.com/get-started/)

**Systeem setup benodigd voor Docker**

**Virtualisatie**

Om Docker Desktop uit te kunnen voeren moet er een systeeminstelling wijzigen. Mogelijk staat deze al goed, dit kun je controleren door naar taakbeheer te gaan (Ctrl + Shift + Esc) en dan bij Prestaties -\> Processor te kijken naar 'Virtualisatie:'. Als dit op 'Ingeschakeld' staat ga dan door naar "Installatie Docker Desktop". Om virtualization in te schakelen moet een EUFI (BIOS) instelling gewijzigd worden, volg hiervoor het stappenplan hieronder.

Voor iets meer informatie zou je ook de Troubleshoot van Docker kunnen raadplegen: [https://docs.docker.com/desktop/troubleshoot/topics/#virtualization](https://docs.docker.com/desktop/troubleshoot/topics/#virtualization)

**EUFI benaderen**

Als je weet hoe je in je EUFI komt kun je dit stukje overslaan en daar direct heen gaan. Het benaderen van de firmware van je computer kan iets zijn wat niet altijd even makkelijk gaat. Gelukkig is er op Windows een manier om daar indirect heen te gaan. Zoek op 'Geavanceerde opstartopties' (of ga bij Instellingen naar Systeem -\> Systeemherstel) en klik (lees eerst wat je moet doen) op 'Nu Opnieuw Opstarten'. Je computer start opnieuw op en

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

1. Zet WSL2 als de standaardversie met het volgende commando:

wsl --set-default-version 2

1. Herstart je computer om deze wijzigingen door te voeren.

**Installatie Docker Desktop**

Als de setup van het systeem gelukt is ga dan verder met het installeren van Docker Desktop volg de installatiehandleiding van jouw OS;

Linux: [https://docs.docker.com/desktop/install/linux-install/](https://docs.docker.com/desktop/install/linux-install/)

Mac: [https://docs.docker.com/desktop/install/mac-install/](https://docs.docker.com/desktop/install/mac-install/)

Windows: [https://docs.docker.com/desktop/install/windows-install/](https://docs.docker.com/desktop/install/windows-install/)

# Aan de slag met Docker enPHP

1. Maak een nieuw bestand in de hoofdmap van je PHP project genaamd `Dockerfile` (dus zonder extensie) enopenhetinbijvoorbeeld PhpStorm.
2. Plak de volgende code in deDockerfile:

```Dockerfile
FROM php:8.2-apache

COPY . /var/www/html

EXPOSE 80
```

Deze code vertelt Docker om een container te maken met PHP 8.1 en Apache (een webserver) erin. Je app wordt gekopieerd naar de container en de container zal naar verzoeken luisteren op poort 80.

3. Klik rechts op Dockerfile en klik op `Run 'Dockerfile'`. Stel bij Image tag een zelf verzonnen image tag bijvoorbeeld: local/docker-test en klik bij sectie Run op `Modify` en selecteer `Bind ports` en `Bind mounts`. Zet bij `Bind ports` (Folder icoon) zoals onderstaande afbeelding zodat je het web-project straks op http://localhost:8080 kan bereiken. Zorg dat je niet per ongeluk een lege regel aanmaakt (klik op OK en niet op enter)!

![](RackMultipart20230824-1-7hufcb_html_98e07298689cd89c.png)

4. Klik op `Bind mounts` op het Folder icoon en selecteer bij `Host path` de map van je webproject waar je index.php staat (vaak de hoofdmap van je project) en zet bij `Container path`: /var/www/html (zie onderstaande afbeelding). Dit doen we zodat de wijzigingen die je op je development maakt, direct zichtbaar zijn in de Docker Container zonder de Image opnieuw te bouwen. Zorg dat je niet per ongeluk een lege regel aanmaakt (klik op OK en niet op enter)!

![](RackMultipart20230824-1-7hufcb_html_cf602057359f162b.png)

Bind Mounts instellingen

Zie onderstaand of je alles hebt ingevuld en klik op OK, mocht je dingen willen aanpassen, dan kun je op de Dockerfile rechts klikken \> `More Run/Debug` \> Modify Run Configuration…

![](RackMultipart20230824-1-7hufcb_html_e1ff6775c6df9baf.png)

Dockerfile Run settings

1. Klik op de groene start button bovenaan in PhpStorm, Docker download de php:8.2 image, zie ook [https://hub.docker.com/\_/php](https://hub.docker.com/_/php) . Je hebt nu een button `Services` onderin PhpStorm, als je hier op klikt komt je Docker service tevoorschijn. Bij Build Log zie je logs van het bouwen van je Dockerfile, bij Log komt de log van Apache2 tevoorschijn en bij Dashboard heb je de controle over de Docker Container.
2. Open een webbrowser en ga naar [http://localhost:8080](http://localhost:8080/). Je ziet nu je PHP-app draaien inDocker!

3. Aan de slag met Docker en C#

# Aan de slag met Docker enC# .NET Core

1. Maak een nieuw bestand in de hoofdmap van je C# project genaamd `Dockerfile` (zonder extensie) en open het in bijvoorbeeld Visual Studio.
2. Plak de volgende code in de Dockerfile:

```Dockerfile
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build-env

WORKDIR /app

# Kopieer csproj en herstel afhankelijkheden

COPY \*.csproj ./

RUN dotnet restore

# Kopieer alles en bouw

COPY . ./

RUN dotnet publish -c Release -o out

# Bouw runtime image

FROM mcr.microsoft.com/dotnet/aspnet:7.0 WORKDIR /app

COPY --from=build-env /app/out . ENTRYPOINT ["dotnet", "my-csharp-app.dll"]
```

Deze code vertelt Docker om een container te maken met .NET 7.0 SDK en ASP.NET 7.0. Je C#-app wordt in de container gebouwd en uitgevoerd.

1. Maak een nieuw bestand genaamd my-csharp-app.csproj en plak de volgende codeerin:

```xml
<Project Sdk="Microsoft.NET.Sdk"\>

  <PropertyGroup\>

  <OutputType\>Exe\</OutputType\>

  <TargetFramework\>net7.0\</TargetFramework\>

  </PropertyGroup\>

</Project\>
```

2. Bouw en start je Docker-container met de volgendecommando's:

```bash
docker build -t my-csharp-app .

docker run --rm --name my-csharp-container my-csharp-app
```

In je terminal of opdrachtprompt zie je nu je C#-app draaien inDocker!

# Conclusie

Je hebt nu geleerd hoe je Docker kunt gebruiken met PHP en C\# op Windows, macOS en Linux. Door Docker te combineren met deze programmeertalen, kun je gemakkelijker apps maken die op verschillende computers werken, wat handig is voor samenwerking en het delen van je werk. Je kan de Docker Images die je hebt gemaakt ook nog pushen naar de Docker Hub. Lees voor meer informatie over Docker de volgende get-started handleiding: [https://docs.docker.com/get-started/](https://docs.docker.com/get-started/)

![Shape1](RackMultipart20230824-1-7hufcb_html_77d9050c87e65e13.gif)

