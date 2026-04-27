# Documentació de l’Arquitectura i Funcionament del Projecte

En aquest document explico de manera clara i entenedora com està organitzat el meu projecte d’auditoria de ciberseguretat. L’objectiu és que qualsevol persona pugui comprendre què fa cada fitxer i com es relacionen entre ells, independentment del seu nivell tècnic.

---

## 1. Interfície i Control de l’Aplicació

### main_enterprise.py
Aquest és el fitxer principal i el punt d’entrada de tota l’aplicació. Aquí és on creo la interfície gràfica utilitzant *CustomTkinter*, amb un estil més modern i professional. També gestiono les animacions, els panells de resultats i tota la lògica que permet que l’usuari interactuï amb l’aplicació sense que es quedi bloquejada.  
Per aconseguir-ho, els escanejos s’executen en paral·lel o de forma asíncrona.

### estils_enterprise.py
En aquest fitxer centralitzo tots els colors, tipografies i estils visuals. Això em permet mantenir el codi més net i facilita molt canviar el tema visual en el futur.

---

## 2. Mòduls d’Escaneig i Auditoria

Aquests mòduls són els encarregats de fer les diferents parts de l’auditoria. Cada un té una funció específica i treballen de manera independent.

### port_scanner.py
Realitza escanejos de ports per detectar quins serveis estan oberts en un objectiu. Pot utilitzar *nmap* o sockets propis, i està optimitzat perquè funcioni ràpid gràcies al paral·lelisme.

### ssh_audit_module.py
Analitza serveis SSH oberts i comprova si tenen configuracions insegures, algoritmes febles o banners exposats.

### enum4linux_scan.py
Automatitza l’eina *enum4linux* per obtenir informació de serveis SMB/Samba. A més, interpreta els resultats perquè siguin més fàcils d’entendre.

### theharvester_osint.py
Integra *theHarvester* per fer recollida d’informació OSINT: dominis, subdominis, correus electrònics i altres dades públiques relacionades amb un objectiu.

### web_scanner.py
Analitza serveis web i revisa aspectes com capçaleres de seguretat, directoris exposats o configuracions potencialment vulnerables.

> Les carpetes `theHarvester/` i `enum4linux/` contenen el codi i les dependències necessàries per fer funcionar aquests mòduls externs.

---

## 3. Utilitats, Processament i Notificacions

### utils.py
Inclou funcions de suport que utilitzo en diferents parts del projecte: classificació de vulnerabilitats, neteja de textos, gestió de rutes d’exportació i altres tasques auxiliars.

### pdf_generator.py
Genera els informes finals utilitzant *reportlab*. He creat dos formats diferents:
- **Client**: més senzill i fàcil d’entendre.
- **Professional**: molt més detallat i pensat per auditors o equips tècnics.

### telegram_api.py
Permet enviar notificacions automàtiques a través d’un bot de Telegram. El token del bot es guarda al fitxer `.env` per seguretat.

---

## 4. Execució, Contenidors i Entorn

### executar_enterprise.sh
Script que facilita l’execució del projecte en un entorn local. Prepara les dependències i llança l’aplicació.

### executar_docker.sh
Permet executar el projecte dins d’un contenidor Docker, ideal per evitar problemes de compatibilitat i mantenir totes les eines encapsulades.

### Dockerfile i .dockerignore
Defineixen com es construeix la imatge Docker: sistema base, eines necessàries (com *nmap*), dependències Python i configuració d’execució.

### requirements.txt
Llista totes les llibreries Python necessàries per fer funcionar el projecte.

### .env.example
Plantilla on l’usuari pot afegir claus, contrasenyes o tokens sense exposar-los directament al codi.

### Documentació addicional
Inclou fitxers com:
- `README.md`
- `README_TELEGRAM.md`
- `DOCKER_GUIA.md`
- `LICENSE`

Aquests expliquen com utilitzar el projecte, com configurar Docker i com funciona el bot de Telegram.

---

## 5. Esquema General del Sistema

Així és com es relacionen totes les parts del projecte:

