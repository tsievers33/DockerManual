#### Voorbereiding

1.  **Zorg ervoor dat Docker geïnstalleerd is.** Als Docker nog niet is geïnstalleerd kan je de Docker guide volgen in deze repository.
2.  **Zorg ervoor dat je een werkend Laravel project hebt.** Als je geen werkend laravel project hebt,
    zoek er dan één online of vraag het aan je klasgenoten.
3.  **Zorg ervoor dat je project op WSL geïnstalleerd is.** Dit houdt dus ook in dat je php, Composer & Node moet installeren op WSL.


### Stappenplan

#### Startup en bouwen van container
- Open wsl en navigeer naar de folder waarin je project zich bevind.
- Kopieer de ```.dockerignore``` & ```Dockerfile``` vanuit [de handleiding](https://github.com/tsievers33/DockerManual/tree/main/praktische_voorbeelden/larvel-development).
- Run het volgende commando om jouw image te bouwen:
```bash
docker build -t mijn-naam/laravel-app .
```
```mijn-naam/laravel-app``` is de naam van jouw image. Je kan dit vervangen door een andere naam als je dat wil.
De punt . aan het einde van het commando geeft aan dat Docker moet bouwen met de Dockerfile in de huidige directory.

#### Starten van de container
Na het succesvol bouwen van de docker image, kan je het volgende commando uitvoeren om de container te starten:
```bash
docker run -d -p 8000:80 laravel-app
```
De optie ```-d``` zorgt ervoor dat de container op de achtergrond draait.
```-p 8000:80``` mapt poort 80 van de container naar poort 8000 op hun host-machine.
Dit betekent dat ze toegang kunnen krijgen tot hun Laravel-applicatie door naar [http://localhost:8000](http://localhost:8000) te gaan in hun webbrowser.