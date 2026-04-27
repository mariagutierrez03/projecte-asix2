---
layout: default
title: "Projecte Intermodular"
---

![foto](./fotos/portada.png)

**Autors:** María Gutiérrez, Edgar Alcaraz i Víctor Hernández  
**Grup:** 3  
**Data:** 27/04/2026  
**Lloc:** Institut de l’Ebre  
**Professors:** Joan Pasqual Almudeve, Víctor Cid i Diego Cervellera  
**Cicle formatiu:** 2n de Superior d’Administració de Sistemes Informàtics en Xarxa   

---

## Introducció

Aquest projecte neix directament de la proposta dels professors, on se'ns demana simular un escenari professional molt concret: crear una empresa de ciberseguretat i fer una auditoria a una altra empresa amb problemes reals. L'objectiu final és doble: demostrar que entenem el món dels negocis i que sabem aplicar les tècniques de hacking ètic.

Per fer-ho, hem creat la nostra consultora anomenada Hexon Security, que treballa sota el lema: "Take care of your company with us". La primera part del treball ha consistit a muntar el pla d'empresa, que és el manual de com funciona Hexon Security. Aquí definim els nostres rols, expliquem què vendrem i com ens organitzem. A més de gestionar totes les tasques amb KanbanFlow.

La segona part és l'encàrrec principal: auditar l'empresa GlobalData Solutions (GDS), que hem creat perquè tingui servidors amb forats de seguretat concrets. La nostra feina d'auditors és fer el Pentesting, és a dir, simular un atac extern per trobar aquests punts febles. Ens hem centrat a trobar i aprofitar vulnerabilitats clàssiques i perilloses, com la Injecció SQL en el seu sistema o l'ús de programari antic. Això ens permetrà demostrar que un atacant pot entrar fàcilment.

Un cop hem aconseguit accedir-hi, la feina més important és la de consultor: presentar la solució. El projecte acaba amb l'entrega de l'informe d'auditoria, on no només ensenyem les proves de l'atac, sinó que donem les instruccions exactes perquè GDS pugui tancar els forats de seguretat i protegir-se de veritat.

---

## Gestió i planificació

### Hexon Security - Empresa ciberseguretat

La nostra empresa, Hexon Security, es dedica a fer pentesting o, dit d'una manera senzilla, a fer de "hacker ètic" per a altres empreses. El nostre objectiu és entrar als sistemes del client abans que ho faci un hacker, per trobar les portes obertes i tancar-les. El nostre lema és: "Take care of your company with us" (Cuida la teva empresa amb nosaltres).

![foto](./fotos/banner.png)

---

### Pla econòmic-financer

Aquesta part explica els diners d'Hexon Security per demostrar que el nostre negoci pot aguantar-se per si mateix.

Per començar, sabem que hem de fer una inversió inicial per tenir el material bàsic, com ara els tres ordinadors potents per fer les auditories i els diners per posar l'empresa legalment. En total, posem que la inversió inicial es mou al voltant dels 6.300 €, que assumim que posem els tres socis. Després, cada mes tenim unes despeses fixes d'uns 440 € (la quota d'autònoms i despeses petites com la internet), que hem de pagar sí o sí.

Però el més important són els nostres serveis. Per fer l'empresa més creïble, no venem només un tipus d'auditoria. Hexon Security té tres tipus de serveis:

- L'Auditoria integral (el servei complet), que val 2.500 €.  
- L'Anàlisi bàsica de vulnerabilitats (una revisió ràpida) que venem per 800 €.  
- La formació al personal (tallers sobre seguretat), que val 500 € cada sessió.  

Per ser rendibles i pagar-nos un sou net d'uns 1.200 € a cadascú, hem de guanyar uns 4.040 € al mes. Aconseguir aquesta xifra és molt més fàcil amb la barreja de serveis. Per exemple, amb una sola Auditoria Integral i dues Anàlisis Bàsiques al mes, ja superem l'objectiu (4.100 €). Això vol dir que la nostra empresa és molt estable i creïble, ja que no depèn d'un únic ingrés gran, i demostra que Hexon Security és un negoci viable.

---

### L'Equip darrere d'Hexon Security - SCRUM

Som tres persones, cadascuna amb un paper clau:

- **Edgar serà el cap (CEO):** Ell s'encarrega de parlar amb els clients, entendre què necessiten i de dissenyar el pla general de l'auditoria. A més, liderarà la part més de xarxes i servidors.  
- **Víctor serà el tècnic:** Ell té el coneixement profund de com funcionen les aplicacions web (les pàgines i els sistemes que usen els clients). Ell s'encarregarà d'intentar explotar les vulnerabilitats més complexes, com les de codi o les bases de dades.  
- **María serà la responsable d'organització i documentació:** És la persona que posa ordre al caos. Ella s'assegura que seguim els procediments correctes, gestiona el temps i, el més important, escriu l'informe final que li donarem al client, detallant els problemes i les solucions.

![foto](./fotos/SCRUM-2.png)

---

### Per què Hexon Security triomfarà?

Hem detectat que moltes empreses petites i mitjanes (PyMEs) inverteixen molts diners en publicitat o nous ordinadors, però gairebé res en seguretat. Nosaltres venim a omplir aquest buit oferint auditories professionals a un preu accessible. El nostre valor afegit és que no només diem "això està malament", sinó que demostrem que podem entrar-hi i expliquem pas a pas com ho han d'arreglar.

---

## Global Data Solutions - Empresa auditada

La nostra empresa client fictícia es diu GlobalData Solutions (GDS). És una empresa de gestió de dades que té un sistema online perquè els seus clients puguin consultar informació i factures. Aquesta empresa té dos tipus de servidors que auditaran:

- **El servidor web (Frontend):** És on els usuaris de GDS entren amb un usuari i contrasenya. Aquest servidor executa l'aplicació.  
- **El servidor de gestió Interna:** És el cor de l'empresa, on guarden els fitxers importants. Aquest servidor hauria d'estar molt protegit, però no ho està.

![foto](./fotos/banner2.png)

---

### Els servidors tenen vulnerabilitats reals

Perquè el nostre projecte sigui pràctic i real, els servidors de GDS tenen tres grans errors o "vulnerabilitats" que nosaltres podrem explotar:

- **Error de configuració (sistemes antics):** El seu servidor de gestió interna utilitza un programa antic (per exemple, una versió vella d'un servei web o un sistema d'arxius) que ja té un defecte de seguretat conegut. Aquest defecte permet, per exemple, que un atacant executi ordres a l'ordinador sense permís (això es diu RCE o Execució Remota de Codi). Aquesta serà la feina: trobar la versió del programa i aplicar l'atac conegut.  
- **Injecció SQL (SQL Injection):** El formulari de login de la seva pàgina web (on poses usuari i contrasenya) està mal fet. El sistema agafa el que escrius i ho envia directament a la base de dades sense comprovar si és una ordre perillosa. L’empresa de ciberseguretat podrà escriure un codi especial a la casella de la contrasenya que enganyi la base de dades i li digui: "No et preocupis per la contrasenya, deixa'm passar". Això permetrà a Hexon Security entrar a l'aplicació sense tenir cap usuari vàlid.  
- **Contrasenyes de fàbrica o molt dèbils:** El seu servidor de gestió interna té un accés (per exemple, per FTP o RDP) amb un usuari que és "admin" i una contrasenya molt simple com "12345". Hexon Security provarà les contrasenyes més comunes (un atac de "força bruta" molt ràpid) i aconseguirà accés als fitxers interns de l'empresa.

![foto](./fotos/SQL-Injection-1.png)

---

### Planificació de l’auditoria

La nostra feina es divideix en fases, com en qualsevol projecte.

- **Fase de reconeixement:** Comencem investigant GDS sense tocar els seus sistemes. Busquem a internet les seves adreces, quins programes fan servir o quines versions de programari.  
- **Fase d'exploració:** Ara sí, utilitzem eines com escàners per veure quins "ports" tenen oberts i quins serveis estan actius. Això ens dirà on hem de buscar problemes.  
- **Fase d'explotació:** Aquí és on s’utilitzen les eines (com Kali Linux) per explotar les tres vulnerabilitats que hem comentat abans (l'SQL Injection, l'RCE i la contrasenya feble). L'objectiu és demostrar que podem prendre el control o robar dades.  
- **Fase d'informe i solució:** Un cop hem demostrat que hem pogut entrar, es documenta tot el procés. Fem una llista de problemes, els hi posem una nota (de "crític" a "baix") i, el més important, escrivim la solució exacta per a cada problema (ex. "Actualitzeu el programari a la versió 2.5" o "Sanejar les entrades d'usuari al formulari de login").

---

### Metodologia i organització

#### Eines de gestió de tasques (Kanban Flow)

Per garantir l'eficiència i la transparència en el projecte, Hexon Security utilitza la metodologia Kanban, implementada mitjançant l'eina digital KanbanFlow. Aquesta metodologia ens permet visualitzar tot el treball pendent, el que està en marxa i el que ja s'ha acabat.

Tal com es veu a la imatge, el nostre tauler es divideix en quatre columnes principals:

- **Per fer:** Les tasques pendents que hem de començar. Aquí tenim tant la part administrativa (pla d'empresa, CVs) com les tasques tècniques (auditoria SSH, enumeració).  
- **Fer avui:** Les tasques prioritàries que ens hem compromès a començar o acabar avui (actualment, el nostre tauler mostra que estan buides, indicant que ja s'han mogut o completat els objectius del dia).  
- **En progrés:** Les tasques que un membre de l'equip està fent activament en aquest moment.  
- **Fet** Les tasques finalitzades. L'objectiu és tenir totes les tasques en aquesta columna al final del projecte.  

A més, cada tasca té assignat un responsable (EA - Edgar, MG - Maria, VC - Víctor) i una estimació de temps (per exemple, 4h per al 'Pla d'empresa'), la qual cosa ens ajuda a gestionar la càrrega de treball i els terminis.

![foto](./fotos/kanban1.png)

---

## Gestió de riscos i incidències

### Anàlisi de riscos

Durant l’auditoria de l’empresa Global Data Solutions, hem fet un estudi per detectar quins elements i processos de l’empresa podrien estar exposats a possibles riscos o problemes. L’objectiu d’aquest estudi és saber quins riscos són més probables i quins podrien tenir un impacte més gran, per així decidir quines accions cal prendre primer.

Hem revisat diferents parts de la infraestructura, com els servidors interns, els formularis de la web, els accessos dels administradors i la informació dels clients. Cada risc s’ha analitzat segons la seva probabilitat i les conseqüències que podria causar, obtenint un resultat que ens indica quines coses cal arreglar de manera urgent i quines es poden gestionar amb mesures preventives més senzilles.

A més, hem proposat solucions pràctiques com actualitzar el programari, reforçar les contrasenyes, separar parts de la xarxa per protegir-les millor o formar els usuaris perquè reconeguin intents de phishing.

![foto](./fotos/analisi-riscos.png)

---

## Acords i abast del servei

### Anàlisi de mercat

L’objectiu d’aquest apartat és analitzar com està el mercat laboral a les Terres de l’Ebre en el sector de la ciberseguretat i la informàtica. També volem veure quines oportunitats hi ha per a persones joves amb ganes d’aprendre i formar-se.

#### Ocupacions principals

En aquest sector hi ha diversos perfils importants:

- **Tècnics i tècniques en ciberseguretat:** protegeixen xarxes i sistemes informàtics.  
- **Analistes i consultors:** estudien vulnerabilitats i ajuden les empreses a millorar la seguretat.  
- **Auditors o ethical hackers:** fan proves per detectar problemes abans que els hackers els puguin aprofitar.  
- **Administradors de sistemes i xarxes:** mantenen servidors i serveis funcionant correctament.  
- **Enginyers de seguretat:** dissenyen sistemes segurs des del principi dels projectes.  

#### Perfils i competències

Segons el SEPE, la demanda d’aquests professionals ha crescut molt. Les empreses busquen persones amb titulació en informàtica, telecomunicacions o FP superior, experiència en administració de sistemes i xarxes, i certificacions com **CompTIA Security+**, **CEH** o **OSCP**. També valoren que sàpigues analitzar problemes, treballar sota pressió i comunicar-te bé amb l’equip. Els llocs solen ser a jornada completa, tot i que alguns poden requerir estar disponibles per incidències.

![foto](./fotos/sepe.png)

#### Tendències i oportunitats

Els perfils amb més sortida ara mateix són **administradors de sistemes**, **programadors** i **analistes TIC**. Però els especialistes en ciberseguretat, els enginyers de sistemes amb coneixements de seguretat i els professionals de **Big Data** estan creixent molt ràpidament. Aquest creixement és a causa de la digitalització i l’augment d’incidents de seguretat.  

Altres ocupacions amb potencial inclouen tècnics de suport informàtic, administradors de xarxes, consultors de seguretat i desenvolupadors de software segur.

#### Empreses a les Terres de l’Ebre

Hi ha diverses empreses i institucions on aquests perfils poden treballar i créixer professionalment. L’Hospital Verge de la Cinta, el Consell Comarcal del Baix Ebre i l’Ajuntament de Tortosa ofereixen oportunitats al sector públic. Entre les empreses privades, DISI Serveis Informàtics, REHAU, Pentrilo, EbreSoft i iTebre ofereixen feina relacionada amb informàtica, seguretat i desenvolupament de software.         

---

### Formació complementaria

#### Ofertes de feina i requisits principals
Per preparar-nos millor pel mercat laboral, hem fet una ullada a les ofertes publicades al portal de [Feina Activa](https://feinaactiva.gencat.cat/web/guest/home) dins de l’àmbit informàtic i TIC. Podeu veure totes les ofertes que vam consultar en aquest enllaç: [Ofertes tècnics informàtics a Tarragona i Reus](https://feinaactiva.gencat.cat/es/search/offers/list?type=province&province=43&i=0&keywords=TECNIC%20INFORMATIC).

A Tortosa no hi havia cap oferta disponible, així que vam ampliar la cerca a Tarragona i Reus. A la taula següent hem resumit les oportunitats més rellevants, indicant la formació imprescindible, la formació valorada i altres característiques importants de cada lloc de treball. Aquesta informació ens ajuda a veure en quines competències hem de reforçar-nos per tenir més opcions de feina.

| Empresa | Localitat | Oferta de feina | Formació imprescindible | Formació valorada | Altres característiques |
|---------|-----------|----------------|------------------------|-----------------|------------------------|
| Institut Pere Mata, S.A. | Reus | Enginyer/a informàtic/a: desenvolupament d’aplicatius sanitaris, integració de dades, helpdesk | Grau/Llicenciatura en Informàtica, 2 anys experiència | Power BI, Pentaho, Mirth, Visual Studio, Intersystems Caché, experiència sanitària | Contracte indefinit, jornada completa, 2.500–2.590 €/mes, nivell C1 català/espanyol/anglès, vehicle propi |
| Aula Magna | Tarragona | Tècnic/a informàtic/a: manteniment equips, xarxes, Moodle, suport a usuaris | FP Grau Mitjà/Superior en Informàtica | Moodle, Linux, seguretat informàtica | Contracte 4 mesos (substitució), jornada completa, 1.565–1.830 €/mes, possibilitat continuïtat mitja jornada |
| Ajuntament de Tarragona | Tarragona | Cap de Servei TIC: direcció i coordinació TIC municipals | Grau Enginyeria Informàtica/Telecomunicacions | Experiència en administració pública i gestió d’equips TIC | Concurs públic, nivell C1 català, jornada completa |
| Empresa informàtica - Tècnic/a de camp | Tarragona | Suport tècnic in situ: TPVs, xarxes, videovigilància, manteniment servidors | Experiència mínima 2 anys en hardware i xarxes | TPV, electrònica, manteniment en farmàcies, CCTV | Contracte variable, jornada flexible, vehicle propi, presencial |
| Ajuntament de Reus | Reus | Tècnic/a de sistemes: administració i manteniment de sistemes i xarxes municipals | CFGS en Sistemes, DAW/DAM o equivalent | Ciberseguretat, bases de dades, virtualització | Concurs-oposició, jornada completa, convocatòria pública |

#### Formació complementària segons el SEPE

Hem consultat l’informe del [SEPE](https://www.sepe.es/HomeSepe/que-es-observatorio/deteccion-necesidades-formativas.html) sobre les necessitats formatives del sector informàtic. Hem vist quina formació valoren les empreses. Per a programadors i enginyers informàtics cal coneixements avançats en Java, Python, .NET, bases de dades, Power BI, Pentaho, Agile/DevOps i Cloud. Per a tècnics de sistemes i xarxes és important dominar xarxes, Windows i Linux, virtualització i seguretat. I per a tècnics de suport cal formació en resolució d’incidències, atenció a usuaris i eines com Jira o GLPI. Aquesta informació ens ajuda a saber exactament en què cal formar-nos per tenir més opcions de feina.            


#### Com completar la nostra formació

Per preparar-nos per treballar en llocs com l’Institut Pere Mata o els ajuntaments de Reus i Tarragona, hem vist que cal reforçar la nostra formació en programació (Java, SQL, PHP), anàlisi de dades (Power BI, Pentaho), ciberseguretat, administració de sistemes i gestió de projectes amb Agile o DevOps. La bona notícia és que no cal començar de zero, ja que tenim la base del CFGS d’ASIX. Ara només hem de fer cursos complementaris, que podem trobar a entitats com Multimèdia Tarragona, Fundació Esplai, COETIC, UOC, UAB, Aula Magna o plataformes com SOC, Conforcat i Fundesplai. Hem planificat un calendari amb cursos de programació, dades, Cloud/DevOps, ciberseguretat i Moodle, així podem actualitzar-nos, aprendre coses noves i tenir més opcions de feina sense tornar a fer un cicle complet.             

---

### Elaboració del contracte simbòlic

En aquesta part del projecte hem elaborat un contracte simbòlic d’auditoria de seguretat entre una empresa auditora i un client. L’objectiu ha estat definir un marc professional i legal per a la realització d’un pentesting, simulant una situació real dins del sector de la ciberseguretat.         


S’ha definit l’abast de l’auditoria, indicant quins sistemes s’analitzen i quins queden fora, així com les accions permeses i les limitacions per garantir que les proves es facin de forma controlada i sense causar danys. Finalment, s’ha establert el lliurament d’un informe amb els resultats i recomanacions de millora en seguretat.

---

## Execució tècnica i resultats

### Disseny de l'entorn vulnerable
Per a aquest projecte, hem dissenyat un entorn que simula una infraestructura empresarial real d'Alta Disponibilitat (HA). El nostre objectiu ha estat crear un escenari on la prioritat sigui la continuïtat del servei, cosa que ens permet analitzar com la redundància pot arribar a ser, alhora, un punt feble si no es gestiona correctament.

Com es veu en el diagrama, l'arquitectura es basa en dos nodes principals (Servidor 1 i Servidor 2) configurats per treballar en paral·lel. Hem establert una connexió constant entre ells per a la sincronització i replicació de dades. Això vol dir que qualsevol canvi o fitxer es replica automàticament; una característica que, des de l'òptica de la seguretat, ens resulta molt interessant, ja que un atac amb èxit al node principal es podria propagar de forma transparent al secundari.

Dins de cada servidor, hem desplegat els quatre serveis clau que volem posar a prova:

* DHCP i DNS: Són els pilars de la xarxa. Els hem inclòs per veure com podem manipular l'assignació d'IPs o la resolució de noms per desviar el trànsit.

* Servei Web: És la part més exposada de l'entorn, on buscarem vulnerabilitats en les aplicacions allotjades.

* Servei FTP: L'hem configurat com a punt de transferència de fitxers per auditar la seguretat de les dades en trànsit i el control d'accessos.

Finalment, hem definit un accés unificat per als clients de la xarxa. Amb aquesta estructura, el nostre pla és simular com interactuen els usuaris amb els serveis mentre intentem comprometre el sistema o forçar una fallada en els mecanismes de failover. En definitiva, hem buscat un equilibri entre un sistema robust i un laboratori ple de vectors d'atac per explorar.          
<img width="1408" height="768" alt="Gemini_Generated_Image_w7joeww7joeww7jo" src="https://github.com/user-attachments/assets/da30ee24-7544-46e3-85be-05d76c3e20fa" />

### Configuració de l'entorn d'auditoria


### Aplicació d'auditoria i ús d'eines


### Disseny i desenvolupament de l'aplicació Python

#### Documentació de l’arquitectura i funcionament del projecte

En aquest apartat explico el meu projecte d’auditoria de ciberseguretat. L’objectiu és que qualsevol persona pugui comprendre què fa cada fitxer i com es relacionen entre ells, independentment del seu nivell tècnic.

---

#### 1. Interfície i control de l’aplicació

##### main_enterprise.py
Aquest és el fitxer principal i el punt d’entrada de tota l’aplicació. Aquí és on creo la interfície gràfica utilitzant *CustomTkinter*, amb un estil més modern i professional. També gestiono les animacions, els panells de resultats i tota la lògica que permet que l’usuari interactuï amb l’aplicació sense que es quedi bloquejada.  
Per aconseguir-ho, els escanejos s’executen en paral·lel o de forma asíncrona.        
<img width="1517" height="924" alt="image" src="https://github.com/user-attachments/assets/e05090fc-672c-4d69-b7e5-0b01737bb266" />


##### estils_enterprise.py
En aquest fitxer centralitzo tots els colors, tipografies i estils visuals. Això em permet mantenir el codi més net i facilita molt canviar el tema visual en el futur.        
<img width="1517" height="924" alt="image" src="https://github.com/user-attachments/assets/8b661b78-8dba-46dd-a62a-59b8d0a41291" />



---

#### 2. Mòduls d’escaneig i auditoria

Aquests mòduls són els encarregats de fer les diferents parts de l’auditoria. Cada un té una funció específica i treballen de manera independent.

##### port_scanner.py
Realitza escanejos de ports per detectar quins serveis estan oberts en un objectiu. Pot utilitzar *nmap* o sockets propis, i està optimitzat perquè funcioni ràpid gràcies al paral·lelisme.      
<img width="1517" height="924" alt="image" src="https://github.com/user-attachments/assets/b0c62070-a798-4f63-a8c0-37bd0fe22053" />

##### ssh_audit_module.py
Analitza serveis SSH oberts i comprova si tenen configuracions insegures, algoritmes febles o banners exposats.      
<img width="1517" height="924" alt="image" src="https://github.com/user-attachments/assets/4f4a818b-380d-4b80-8fcd-00a79b50a689" />

##### enum4linux_scan.py
Automatitza l’eina *enum4linux* per obtenir informació de serveis SMB/Samba. A més, interpreta els resultats perquè siguin més fàcils d’entendre.        
<img width="1517" height="924" alt="image" src="https://github.com/user-attachments/assets/61e58fb0-c0d5-4885-8121-6e3e4edb49eb" />

##### theharvester_osint.py
Integra *theHarvester* per fer recollida d’informació OSINT: dominis, subdominis, correus electrònics i altres dades públiques relacionades amb un objectiu.      
<img width="1517" height="924" alt="image" src="https://github.com/user-attachments/assets/5f4f686a-3aab-48c3-a9d0-a01e2e6e39e7" />

##### web_scanner.py
Analitza serveis web i revisa aspectes com capçaleres de seguretat, directoris exposats o configuracions potencialment vulnerables.

> Les carpetes `theHarvester/` i `enum4linux/` contenen el codi i les dependències necessàries per fer funcionar aquests mòduls externs.      
<img width="1517" height="924" alt="image" src="https://github.com/user-attachments/assets/1281a8ce-1716-4765-a5d0-02dcc8ccc8dd" />

---

#### 3. Utilitats, processament i notificacions

##### utils.py
Inclou funcions de suport que utilitzo en diferents parts del projecte: classificació de vulnerabilitats, neteja de textos, gestió de rutes d’exportació i altres tasques auxiliars.        
<img width="1517" height="924" alt="image" src="https://github.com/user-attachments/assets/052c7a84-5eae-4ff5-94b8-37114e044b40" />

##### pdf_generator.py
Genera els informes finals utilitzant *reportlab*. He creat dos formats diferents:
- **Client**: més senzill i fàcil d’entendre.
- **Professional**: molt més detallat i pensat per auditors o equips tècnics.        
<img width="1517" height="924" alt="image" src="https://github.com/user-attachments/assets/322108f4-7455-4593-bf21-5c081b57b502" />

##### telegram_api.py
Permet enviar notificacions automàtiques a través d’un bot de Telegram. El token del bot es guarda al fitxer `.env` per seguretat.        
<img width="1517" height="924" alt="image" src="https://github.com/user-attachments/assets/a087faf3-6e1b-4189-9b62-ef78600ad5ad" />

---

#### 4. Execució, contenidors i entorn

##### executar_enterprise.sh
Script que facilita l’execució del projecte en un entorn local. Prepara les dependències i llança l’aplicació.        
<img width="1517" height="924" alt="image" src="https://github.com/user-attachments/assets/0bb1fce6-0ba4-4ee8-9522-02fd139c2d16" />

##### executar_docker.sh
Permet executar el projecte dins d’un contenidor Docker, ideal per evitar problemes de compatibilitat i mantenir totes les eines encapsulades.      
<img width="1517" height="924" alt="image" src="https://github.com/user-attachments/assets/d2adf972-12c7-4b02-b397-05a7ef3b57c5" />

##### Dockerfile i .dockerignore
Defineixen com es construeix la imatge Docker: sistema base, eines necessàries (com *nmap*), dependències Python i configuració d’execució.      
<img width="1517" height="924" alt="image" src="https://github.com/user-attachments/assets/5d037fcd-4da5-48a8-a985-ded548cb0baf" />

##### requirements.txt
Llista totes les llibreries Python necessàries per fer funcionar el projecte.        
<img width="1517" height="724" alt="image" src="https://github.com/user-attachments/assets/9f217fe9-627d-4ad5-ad7b-98ee0b79c88b" />

##### Documentació addicional
Inclou fitxers com:
- `README.md`
- `README_TELEGRAM.md`
- `DOCKER_GUIA.md`
- `LICENSE`

Aquests expliquen com utilitzar el projecte, com configurar Docker i com funciona el bot de Telegram.

---

#### 5. Esquema general del sistema

Així és com es relacionen totes les parts del projecte:
<img width="697" height="607" alt="image" src="https://github.com/user-attachments/assets/96e8897a-2cbc-406c-ade3-77ed7afda63a" />

### Resultats

### Informe de vulnerabilitats trobades

---

## Incidències

Durant el desenvolupament i les proves del projecte hem tingut algunes incidències que hem anat resolent a mesura que apareixien. Aquestes són les més destacades:

### 1. Problemes amb els escaneigs en rangs CIDR
Alguns mòduls, com **SSH Audit** i **Enum4Linux**, no acceptaven rangs de xarxa (ex: `192.168.0.0/24`) i mostraven errors de resolució.
**Solució:** limitar aquests mòduls perquè només funcionin amb IPs individuals i avisar l’usuari.

### 2. Falta de permisos en alguns escaneigs
Quan l’eina s’executava sense permisos d’administrador, alguns escaneigs (ports i vulnerabilitats) no retornaven resultats correctes.
**Solució:** afegir un avís recomanant executar l’aplicació amb *sudo*.

### 3. API keys no configurades al mòdul OSINT
Les funcionalitats de SecurityScorecard i BuiltWith no funcionaven per falta d’API keys.
**Solució:** documentar on s’han d’afegir i mostrar un missatge d’error clar.

### 4. Retards en l’escaneig de vulnerabilitats
En xarxes amb molts hosts, el procés trigava més del previst i semblava que l’aplicació s’havia quedat bloquejada.
**Solució:** afegir un indicador de progrés i missatges d’estat.

### 5. Informació incompleta en la detecció de serveis
En alguns dispositius antics, Nmap retornava dades incompletes o versions incorrectes.
**Solució:** mostrar “N/A” quan la informació no és fiable i evitar errors al panell de resultats.

---

## Conclusió

Aquest projecte ens ha servit per aprendre de veritat com funciona una auditoria de seguretat i tot el que implica treballar en equip. Hem creat una empresa fictícia, hem organitzat les tasques, hem desenvolupat una eina pròpia i hem fet una auditoria completa com si fos un cas real.

A nivell tècnic hem après a utilitzar eines de ciberseguretat, a detectar vulnerabilitats i a entendre millor com funcionen les xarxes i els serveis. També hem vist la importància de documentar bé el que fem i d’explicar-ho de manera clara perquè qualsevol persona ho pugui entendre.

En general, aquest projecte ens ha ajudat a posar en pràctica tot el que hem estudiat i a veure que som capaços de treballar com un equip professional. Ens quedem amb l’experiència, els coneixements i la sensació d’haver fet una feina completa i útil.

---

## Webgrafia

### 1. Fonts de Ciberseguretat i Pentesting
- **OWASP Foundation.** (2024). *OWASP Top 10 – Vulnerabilities and Security Guidelines*.  
  https://owasp.org

- **MITRE Corporation.** (2024). *MITRE ATT&CK Framework*.  
  https://attack.mitre.org

- **NIST.** (2024). *Cybersecurity Framework (CSF)*.  
  https://www.nist.gov/cyberframework

- **CVE Details.** (2024). *Common Vulnerabilities and Exposures Database*.  
  https://www.cvedetails.com


### 2. Eines utilitzades en l’auditoria
- **Nmap Project.** (2024). *Nmap Security Scanner*.  
  https://nmap.org

- **Cisco CX Security.** (2024). *Enum4linux – SMB Enumeration Tool*.  
  https://github.com/CiscoCXSecurity/enum4linux

- **Laramies, C.** (2024). *theHarvester – OSINT Gathering Tool*.  
  https://github.com/laramies/theHarvester

- **Offensive Security.** (2024). *Kali Linux Documentation*.  
  https://www.kali.org

- **ReportLab Developers.** (2024). *ReportLab PDF Toolkit Documentation*.  
  https://www.reportlab.com/dev/docs


### 3. Desenvolupament de l’aplicació Python
- **Python Software Foundation.** (2024). *Python 3 Documentation*.  
  https://docs.python.org/3

- **Schimansky, T.** (2024). *CustomTkinter – Modern UI for Tkinter*.  
  https://github.com/TomSchimansky/CustomTkinter

- **Docker Inc.** (2024). *Docker Documentation*.  
  https://docs.docker.com

- **GitHub.** (2024). *Repositori i bones pràctiques de desenvolupament*.  
  https://github.com


### 4. Gestió del projecte i metodologia SCRUM
- **Atlassian.** (2024). *Scrum Guide & Agile Methodologies*.  
  https://www.atlassian.com/agile/scrum

- **KanbanFlow.** (2024). *KanbanFlow – Task Management Tool*.  
  https://kanbanflow.com


### 5. Anàlisi de mercat i formació professional
- **SEPE.** (2024). *Informe de necessitats formatives del sector TIC*.  
  https://www.sepe.es

- **Feina Activa.** (2024). *Ofertes TIC a Catalunya*.  
  https://feinaactiva.gencat.cat

- **Servei d’Ocupació de Catalunya (SOC).** (2024). *Formació i certificacions professionals*.  
  https://serveiocupacio.gencat.cat


### 6. Recursos generals de desenvolupament i xarxes
- **W3Schools.** (2024). *Web Development Tutorials*.  
  https://www.w3schools.com

- **Mozilla Foundation.** (2024). *MDN Web Docs*.  
  https://developer.mozilla.org

- **Cisco Networking Academy.** (2024). *Networking & Cybersecurity Learning Platform*.  
  https://www.netacad.com

---

## Annexos

### Annex - 1 Altres documents de suport

A continuació es mostren tots els documents externs utilitzats o generats durant el projecte. Tots estan allotjats a Google Drive i disponibles per a consulta.

### Document 1 – Informe anàlisi de mercat
[Accedir al document](https://drive.google.com/file/d/1GY8h2x8DUa1mmJFDsqSDdBc80n_MMZkC/view?usp=sharing)

### Document 2 – Document anàlisi de mercat a la zona
[Accedir al document](https://drive.google.com/file/d/12n2_zfU1OhRE_dLl1p2wxlH_1EGmc49m/view?usp=sharing)

### Document 3 – Full de càlcul anàlisi de riscos(Google Sheets) 
[Accedir al full de càlcul](https://docs.google.com/spreadsheets/d/1ZOqm3yH9TqcVv-uMncqEnoJv5SiRxy1y/edit?usp=sharing&ouid=107386172793702573921&rtpof=true&sd=true)

### Document 4 – Document contracte simbòlic
[Accedir al document](https://drive.google.com/file/d/1MjqqdDcT6AqqtutKnLbIIkG96ZJiXLCC/view?usp=sharing)

### Document 5 – Document formació complementària
[Accedir al document](https://drive.google.com/file/d/1H88PxxbeFa39Jw9obiI3Kb8C4HxL1yvw/view?usp=sharing)


---
