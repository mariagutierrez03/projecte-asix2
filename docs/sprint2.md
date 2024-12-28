# Gestió d'usuaris i serveis

Per a la documentació completa visita [mkdocs.org](https://www.mkdocs.org).

---
## Introducció

Començarem instal·lant Ubuntu Linux en un entorn de màquina virtual. L'objectiu és assegurar-nos que el sistema operatiu estigui ben configurat per gestionar usuaris, grups i polítiques de contrasenyes de manera eficaç. En aquesta primera fase, ens centrarem en la creació i gestió de comptes d'usuari locals, així com en l'assignació de permisos als grups i la definició de polítiques de seguretat per a les contrasenyes i accessos.

Un cop tinguem la configuració inicial a punt, passarem a instal·lar i gestionar serveis essencials que són crucials per al bon funcionament del sistema. Això inclou la configuració de serveis i processos, l'optimització de l'ús dels recursos disponibles, i l'administració dels serveis actius segons les necessitats del sistema.

A continuació, ens ocuparem de la creació i gestió de particions i sistemes de fitxers. Ens assegurarem que l'espai es distribueixi de manera adequada, aplicarem quotes de disc i implementarem còpies de seguretat automàtiques per protegir la integritat de les dades.

Finalment, realitzarem proves exhaustives per verificar que tot funcioni correctament, incloent la gestió d'usuaris, grups i serveis, així com la integritat dels fitxers, sistemes de particions i quotes de disc. Documentarem cada pas del procés de manera detallada, que inclourà la creació de comptes d'usuari, la configuració de serveis, l'administració de particions, i el pla de recuperació en cas de desastres. A més, acompanyarem la documentació amb captures de pantalla que il·lustrin les configuracions i ajustaments realitzats durant el procés.

![intro](./fotos/intro4.jpg)

---
## Gestió de processos

La gestió de processos és una part essencial dels sistemes operatius, ja que s’encarrega de controlar els programes que s’executen al sistema. Cada procés és un programa en funcionament amb els seus propis recursos, com la memòria o l’accés a la CPU. El sistema operatiu gestiona tasques com crear, executar, pausar o acabar processos, assegurant que tots funcionin de manera eficient i sense problemes. Això permet que diversos processos puguin compartir els recursos del sistema de forma equilibrada.

---

1. En aquest apartat executarem multiples comandes per administrar els processos, però una de les més importants és `pstree` la qual mostra en forma d’arbre jeràrquic tots els processos actius del sistema, organitzats segons les seves relacions de parentiu. Aquesta depenent de en quin usuari l'executes mostra uns processos o uns altres.       
```
pstree
```
![processos](./fotos/p1.png)
![processos](./fotos/p2.png)

2. A més si no estem iniciats en la sessió d'un usuari i volem saber els seus processos podem afegir el paràmetre `-h`. La comanda completa seria `pstree -h maria`.        
```
pstree -h maria
```
![processos](./fotos/p3.png)

4. A continuació també podem afegir el paràmetre `-p`el qual mostra el PID dels processos. Per fer una prova del que he explicat, obrirem un terminal a part i executarem la comanda `pstree -p -h maria` en el terminal que ja estavem abans. Aqui buscarem la branca que indica el nostre terminal (la qual normalment està en negreta) i la primera subbranca hauria de ser l'altre terminal. Important fixar-nos en el PID del segon terminal. Seguidament executarem la comanda `kill -9 2930` (hauràs de canviar el PID 2930 pel que tu tinguis) aquesta força la terminació immediata d’un procés específic, utilitzant la senyal SIGKILL, que no pot ser ignorada pel procés. Una vegada executada s'hauria de tancar el segon terminal.        
```
pstree -p -h maria
```
```
kill -9 2930
```
![processos](./fotos/p4.png)
![processos](./fotos/p9.png)
![processos](./fotos/p10.png)
![processos](./fotos/p11.png)

5. Ara executarem `top` aquesta mostra en temps real informació detallada sobre els processos actius al sistema, incloent ús de CPU, memòria, temps d'execució i estat dels processos. En la sortida de la comanda top, cada columna representa una informació específica dels processos actius. Aquí tens l’explicació de cada columna que es veu a la captura:        

    - PID: Identificador únic del procés (Process ID).
    - USER: Nom de l'usuari que està executant el procés.
    - PR: Prioritat del procés. Valors més baixos indiquen més prioritat.
    - NI: Valor de nice del procés, que afecta la seva prioritat (pot variar de -20 a 19).
    - VIRT: Memòria virtual utilitzada pel procés (inclou memòria reservada i compartida).
    - RES: Memòria física resident (en RAM) que està utilitzant el procés.
    - SHR: Memòria compartida entre diversos processos.
    - %CPU: Percentatge de CPU utilitzada pel procés.
    - %MEM: Percentatge de memòria RAM utilitzada pel procés.
    - TIME+: Temps total de CPU que el procés ha consumit des que es va iniciar.
    - COMMAND: Nom o comanda del procés executant-se.

    ```
    top
    ```
    ![processos](./fotos/p12.png)

    Per exemple si obrim el firefox ens indicarà que el PID és 3372, USER és maria, consumeix un 85,8% de CPU i un 5,2% de memòria, amb un temps acumulat d'execució de 7 segons.       

    ![processos](./fotos/p13.png)

6. La comanda `renice -n 19 -p 3372` canvia la prioritat del procés amb PID 3372 (en aquest cas, firefox) ajustant el seu valor de nice a 19, que és la prioritat més baixa.        
```
renice -n 19 -p 3372
```
![processos](./fotos/p15.png)
![processos](./fotos/p14.png)

7. La comanda `ps aux` s'utilitza per mostrar una llista completa de tots els processos en execució al sistema, amb informació detallada.       

    - USER: Usuari que executa el procés.
    - PID: Identificador del procés.
    - %CPU i %MEM: Ús de CPU i memòria.
    - VSZ: Mida de la memòria virtual en kilobytes.
    - RSS: Mida de la memòria resident (RAM utilitzada pel procés).
    - TTY: Terminal associat al procés (si no en té, apareix com ?).
    - STAT: Estat del procés (ex.: R executant-se, S dormint, Z zombie).
    - START: Hora en què es va iniciar el procés.
    - TIME: Temps total de CPU utilitzat pel procés.
    - COMMAND: Comanda que va iniciar el procés.  

    ```
    ps aux
    ```
    ![processos](./fotos/p16.png)
     
8. La comanda `ps -a` mostra una llista dels processos que s'estan executant en tots els terminals del sistema, excepte els processos propis de l'usuari que no tenen terminal associat (com els processos en segon pla).     
```
ps -a
```
![processos](./fotos/p17.png)

9. La comanda `ps -A` mostra tots els processos en execució al sistema, incloent tant processos amb terminal associat com processos en segon pla o dimonis.       
```
ps -A
```
![processos](./fotos/p18.png)

10. Seguidament, executarem top i farem Ctrl+Z per aturar-lo d'aquesta manera està en segon pla. Per veure els processos en segon pla tenim la comanda `jobs`.      
```
jobs
```
![processos](./fotos/p21.png)
![processos](./fotos/p22.png)

11. Per veure el PID de top podem executar `pstree -p | grep top`.      
```
pstree -p | grep top
```
![processos](./fotos/p23.png)

12. Seguidament el matarem amb `kill -9 4307` i llavors ens sortirà que top està "matat".       
```
kill -9 4307
```
![processos](./fotos/p24.png)

13. També quan un proces esta en segon pla podem optar per tornar-lo a ficar en primer pla amb `fg %1` (el numero despres del % canvia segons el numero que mostra jobs).       
```
jobs
```
```
fg %1
```
![processos](./fotos/p25.png)

14. Tot seguit, també tenim l'ordre `top &` que executa l'eina top en segon pla, permetent que se segueixi executant mentre el terminal roman disponible per a altres ordres.       
```
top &
```
![processos](./fotos/p26.png)

15. A continuacio tenim la comanda `xeyes` amb la que farem un parell de exemples. Si la executem i després fem Ctrl+Z l'aturem i la podem recuperar amb `fg %5`com hem fet abans en top.     
```
xeyes
```
```
fg %5
```
![processos](./fotos/p29.png)

16. A més també ho podem fer amb `xeyes &` i recuperar de la mateixa manera que abans.      
```
xeyes &
```
```
jobs
```
```
fg %1
```
![processos](./fotos/p30.png)

17. De la mateixa manera funciona executant xeyes i després escriure `bg xeyes` (és igual que fer Ctrl+Z).      
```
bg xeyes
```
![processos](./fotos/p31.png)

18. Per poder veure el PID d'un proces en concret com firefox ho podem fer amb multiples comandes com:
```
pgrep firefox
```
```
ps aux | grep firefox
```
```
pstree -p | grep firefox
```
![processos](./fotos/p32.png)
![processos](./fotos/p33.png)
![processos](./fotos/p34.png)

19. Per últim, la comanda `nice -n 19 xeyes` executa el programa xeyes amb la prioritat més baixa possible, fet que fa que rebi menys recursos de la CPU. Quina és la diferencia entre renice i nice? La diferència entre nice i renice és que nice s'utilitza per establir la prioritat d'un procés en el moment en què es crea, mentre que renice serveix per canviar la prioritat d'un procés que ja està en execució.        
```
nice -n 19 xeyes
```
![processos](./fotos/p36.png)
![processos](./fotos/p37.png)





---
## Gestió d'usuaris i grups

La gestió d'usuaris i grups és una part fonamental del sistema operatiu Ubuntu 24 Desktop. Cada usuari té les seves pròpies configuracions, fitxers i permisos, la qual cosa permet una experiència personalitzada i segura. A més, agrupar usuaris facilita l'administració de permisos i l'accés a recursos compartits.

En aquest apartat, explorarem com crear, modificar i eliminar usuaris i grups. També veurem com establir permisos per assegurar-nos que les dades estiguin protegides i accessibles només per aquells que ho necessiten. Amb unes poques passes senzilles, podreu gestionar els vostres usuaris i grups de manera eficient i efectiva. 

---
### Els fitxers més importants

En la gestió d'usuaris i grups d'Ubuntu, hi ha diversos fitxers clau que contenen informació essencial. A continuació, expliquem els més importants:

- **etc/passwd:** Aquest fitxer és un registre de tots els usuaris del sistema. Conté informació com el nom d'usuari, la identificació d'usuari (UID), el directori inicial i el shell predeterminat. És un fitxer accessible, per la qual cosa tothom pot veure qui són els usuaris del sistema.
- **etc/shadow:** Aquí s'emmagatzema la informació de les contrasenyes dels usuaris. Cada línia correspon a un usuari i conté la seva contrasenya encriptada. Si en aquest fitxer veiem un signe "!", significa que l'usuari està bloquejat i no pot accedir al sistema.
- **etc/gshadow:** Aquest fitxer és similar a /etc/group, però proporciona informació addicional sobre els grups. Aquí es poden veure els administradors de cada grup. És útil per gestionar els permisos i els drets d'accés dels grups d'usuaris.
- **etc/groups:** Conté informació sobre els grups del sistema. Cada línia representa un grup i inclou el nom del grup, el seu identificador (GID) i els membres que en formen part. Aquest fitxer és útil per veure quins usuaris pertanyen a cada grup.
---

### Crear i eliminar usuaris
#### USERADD

1. Per poder crear un nou usuari al sistema, utilitzarem la comanda useradd. Aquesta comanda ens permet afegir usuaris amb diversos paràmetres que ens ajuden a definir les seves característiques. A continuació, veurem alguns dels paràmetres clau que podem utilitzar:
    * **-m:** Aquest paràmetre indica que es crearà un directori d'usuari personal (home directory) automàticament. Això és important perquè cada usuari necessita un espai propi per emmagatzemar els seus fitxers.
    * **-s /bin/bash:** Amb aquest paràmetre, especificarem el shell que utilitzarà l'usuari. En aquest cas, estem indicant que volem que el shell sigui Bash, que és un dels més utilitzats en sistemes Linux.
    * **-d /home/nick:** Aquí podem definir el directori d'inici de l'usuari. En aquest exemple, establim que el directori personal de l'usuari serà /home/nick.
    * **nick:** Aquest és el nom de l'usuari que estem creant. En aquest cas, hem triat "nick" com a nom d'usuari.
    * **&& passwd nick:** Aquesta comanda s'utilitza per establir o canviar la contrasenya per a l'usuari "nick".

    ![useradd](./fotos/s1.png)

2. Una vegada fet, si observem el fitxer /etc/passwd/ podrem visualitzar el nou registre amb el nom del usuari que acabem de crear. 
![useradd](./fotos/s2.png)

#### ADDUSER

1. Per fer-ho d'una forma mes senzilla haurem de executar la comanda adduser (nom d'usuari). Seguidament ens apareixeran apartats per emplenar com la contrasenya, nom complet, número d'espai, telèfon, etc. Si revisem el contingut del fitxer /etc/passwd.   
![useradd](./fotos/au1.png)
![useradd](./fotos/au2.png)

#### USERDEL

1. Per poder eliminar un usuari haurem d'utilitzar la comanda userdel que aquesta te diferents parametres el quals podem arribar a ser utils, en aquest apartat veurem dues opcions.
    * **-r:**
    * **-f:** 

    ![useradd](./fotos/s3.png)

2. Una vegada fet si revisem el fitxer /etc/passwd podem observar que l'usuari **nick** ja no existeix.
![useradd](./fotos/s4.png)

3. Seguidament també tenim el parametre **-f**, aquest 
![useradd](./fotos/s5.png)
![useradd](./fotos/s6.png)

---

#### Afegir usuaris per GUI

1. Per poder administrar el usuaris i grups per entorn gràfic haurem de instal·lar per terminal un programa anomenat gnome-system-tools.  
![useradd](./fotos/s7.png)

2. Una vegada dins del programa, veurem els diferents usuaris del sistema, des del aqui podrem afegir, suprimir i gestionar grups.  
![useradd](./fotos/s8.png)

---

### Log usuari per GUI i terminal

1. Per iniciar sessió pel terminal haurem de executar la comanda "su" i seguidament el nom del usuari amb el que volem inciar-la. Per comprovar que ja estem dins podem executar la comanda pwd, aquesta en mostrarà la home de l'usuari.
![useradd](./fotos/s9.png)

2. Per fer el inici de sessió des de la interficie grafica, haurem de sortir de la sessió actual i entrar en l'usuari correcte, de forma habitual introduint la contrasenya. 
![useradd](./fotos/s10.png)
![useradd](./fotos/s11.png)

3. Seguidament una vegada hem entrat, obrirem un terminal i comprovarem el pwd. Podem veure que quan fem un "ls -la" hi han moltes mes carpetes que abans, això és degut a que les carpetes de la home no és creen fins que l'usuari no inicia sessió des de fora.    
![useradd](./fotos/s12.png)

---

### Bloquejar i desbloquejar usuaris

1. Per poder bloquejar usuaris haurem de escriure la comanda "usermod -L (nom d'usuari que volem bloquejar)". Seguidament per poder comprovar si els canvis s'han aplicat, revisarem el fitxer /etc/shadow. Dins d'aquest fitxer baixarem fins trobar l'usuari i si apareix el simbol d'exclamació com mosra la captura de pantalla, vol dir que l'usuari està bloquejat. Una altra forma per comprovar-ho és tancat la sessió i observar que no apareix l'usuari.  
![useradd](./fotos/s13.png)
![useradd](./fotos/s14.png)
![useradd](./fotos/s15.png)
---

2. Per poder desbloquejar l'usuari haurem de esciure la comanda "usermod -U (nom d'usuari)". Seguidament si tornem a revisar el fitxer "/etc/passwd" veurem que no té el signe d'exclamació. Per acabar de comprovar-ho sortirem de la sessió actual i veurem que l'usuari torna a estar. 
![useradd](./fotos/s16.png)
![useradd](./fotos/s17.png)
![useradd](./fotos/s19.png)
---

3. 
![useradd](./fotos/s20.png)
![useradd](./fotos/s21.png)

---

### Modificar nom d’un usuari

1. Per poder modificar el nom d'usuari, haurem de modificar també diferents fitxers i directoris, ja que, ha de coincidir per tant de funcionar. Necessitarem seguir 4 parts indispensables: 
    * usermod -l:
    * 

![useradd](./fotos/s23.png)
![useradd](./fotos/s22.png)

2. 
![useradd](./fotos/s24.png)
![useradd](./fotos/s25.png)

---

### Crear i eliminar grups
#### GROUPADD

1. Per afegir un grup amb groupadd nomes haurem de ejecutar la comanda "groupadd (nom del grup)". Seguidament mirarem el fitxer "/etc/gshadow" i comprovarem que realment està. 
![useradd](./fotos/s26.png)
![useradd](./fotos/s27.png)

2. Seguidament, per aplicar un gid customitzat haurem d'afegir el parametre "-g (número de gid desitjat)". Després comprovarem els canvis al fitxer "/etc/group".
![useradd](./fotos/s30.png)
![useradd](./fotos/s31.png)

#### ADDGROUP

1. El cas de la comanda addgroup és molt paregut al anterior, ja que només haurem de introduir la comanda i consecutivament el nom del grup. L'única diferencia notable és el fet de què t'informa dels canvis aplicats. Si anem al fitxer "/etc/group" podrem veure que el grup està creat.
![useradd](./fotos/s34.png)
![useradd](./fotos/s35.png)


#### GROUPDEL

1. Per eliminar un grup en groupdel haurem d'utilitzar la mateixa estructura que en les dues anteriors. Seguidament revisar que realment ja no està al fitxer "/etc/group".
![useradd](./fotos/s32.png)

#### DELGROUP

1. Una altra forma de eliminar grups és utilitzar la comanda delgroup. 
![useradd](./fotos/s37.png)

---

### Afegir i treure usuaris de grups
#### USERMOD

1. Per poder afegir un usuari haurem d'utilitzar la comanda "usermod -aG (nom grup) (nom usuari)". Si comprovem el resultat a "/etc/group" veurem que l'usuari ara ja està afegit.
![useradd](./fotos/s38.png)
![useradd](./fotos/s39.png)

2. Seguidament per treure l'usuari ficarem la mateixa comanda, però en el parametre "-G" només.
![useradd](./fotos/s50.png)

### CANVIAR LA FOTOOOOO!!!!
![useradd](./fotos/s51.png)

#### GPASSWD
1. A més també podem afegri usuaris a grups amb la comanda "gpasswd -a (nom ususari) (nom grup)". 
![useradd](./fotos/s40.png)
![useradd](./fotos/s41.png)

2. En aquesta mateixa comanda també podem treure usuaris de grups amb el parametre "-d".
![useradd](./fotos/s45.png)
![useradd](./fotos/s46.png)

#### ADDUSER
1. En adduser també podem afegir ususaris a grups, utilitzant la comanda "adduser (nom usuari) (nom grup)". 
![useradd](./fotos/s42.png)
![useradd](./fotos/s43.png)

2. En una comanda pareguda a l'anterior podem eliminar aquests usuaris dels grups, "deluser (nom usuari) (nom grup)"
![useradd](./fotos/s47.png)
![useradd](./fotos/s48.png)

---

### Modificar grup principal d’un usuari
1. Per modificar el nom el grup principal d'un usuari haurem d'utilitzar la comanda "usermod -g (nom grup) (nom usuari)". Per comprovar-ho farem un "id (nom usuari)", aqui si revisem el gid veurem que ara està canviat.
![useradd](./fotos/s52.png)

---
## Gestió de permisos

### Permissos normals

1. El primer haurem de fer és crear 4 usuaris, en el meu cas he creat a Lola, Laura, Mariona i Martina.
![chmod](./fotos/1.png) 
![chmod](./fotos/2.png)
![chmod](./fotos/3.png) 
![chmod](./fotos/4.png)

2. Seguidament, revisarem que realment estan creats els 4 usuaris al fitxer /etc/passwd. 
![chmod](./fotos/5.png)

3. Després crearem un grup anomenat grup-a i afegirem als usuaris lola i mariona.
![chmod](./fotos/6.png)

4. L'ultim pas 
![chmod](./fotos/7.png)



#### CHGRP
1. 
![chmod](./fotos/8.png)

2. 
![chmod](./fotos/9.png)

#### CHMOD
1. 
![chmod](./fotos/10.png)

2. 
![chmod](./fotos/11.png)

3. 
![chmod](./fotos/12.png)

4. 
![chmod](./fotos/13.png)

5. 
![chmod](./fotos/14.png)

6. 
![chmod](./fotos/15.png)

#### CHOWN


### Permissos especials
#### STICKY
1. 
![chmod](./fotos/16.png)

2. 
![chmod](./fotos/17.png)

3. 
![chmod](./fotos/18.png)

#### SUID
1. 
![chmod](./fotos/20.png)
![chmod](./fotos/19.png)
2. 
![chmod](./fotos/21.png)

#### SGID
1. 
![chmod](./fotos/22.png)

### Permissos en ACL 
1. 
![chmod](./fotos/24.png)

2. 
![chmod](./fotos/25.png)

3. 
![chmod](./fotos/26.png)

4. 
![chmod](./fotos/27.png)

5. 
![chmod](./fotos/28.png)

6. 
![chmod](./fotos/29.png)


---
## Sistemas de fitxers i particions
### Estructura física
L’estructura física fa referència als components tangibles que constitueixen un sistema d’emmagatzematge. Aquests inclouen discos durs (HDD), unitats d'estat sòlid (SSD), memòries flash, i altres dispositius. Els elements físics importants són les pistes, sectors i cilindres en el cas dels HDD, i les cel·les d'emmagatzematge en els SSD. Aquesta estructura és la base sobre la qual es construeixen els mecanismes d'emmagatzematge i recuperació de dades.

---

### Estructura lògica
L’estructura lògica representa com es gestionen i organitzen les dades dins del sistema operatiu. Inclou elements com el sistema de fitxers, carpetes, i enllaços simbòlics. Els sistemes de fitxers (com NTFS, FAT32, ext4) defineixen la manera com es llegeixen, escriuen i organitzen les dades emmagatzemades al dispositiu físic. Aquesta estructura permet als usuaris accedir a la informació d'una manera comprensible i eficient.

---

### Estructura de la informació
L’estructura de la informació descriu com s’organitzen i gestionen les dades tant a nivell físic com lògic dins d’un dispositiu d’emmagatzematge. Inclou aspectes com les unitats mínimes on es desen les dades i com aquestes són agrupades per optimitzar el rendiment. A continuació, es detalla uns conceptes clau dins d’aquesta estructura:

#### MIDA DEL SECTOR
La mida del sector és la unitat mínima física on es guarden les dades en un dispositiu d'emmagatzematge. Per defecte, aquesta mida sol ser de 512 bytes, però pot variar en dispositius més moderns amb sectors de 4 KB (4096 bytes). Aquesta mida està definida de fàbrica i no es pot modificar. Tot i això, el sistema operatiu no treballa directament amb sectors sinó amb blocs, que són unitats lògiques més grans on es guarden les dades.  


Per poder revisar els discs haurem d'executar la comanda "fdisk -l", aquesta és molt utils ja que et mostra l'identificador del disc (/dev/sda), el tamany (50 GB), el tipus (GPT o MBR), número de sectors, tamany del sector, etc.
```
sudo fdisk -l
```
![chmod](./fotos/m3.png)
![chmod](./fotos/m7.png)



#### MIDA DEL BLOC
El bloc és la unitat mínima lògica d'emmagatzematge utilitzada pel sistema operatiu. La mida del bloc es pot configurar durant el procés de formatatge d'una partició. La mida del bloc influeix en l'eficiència de l'emmagatzematge: blocs més grans poden ser més ràpids però poden generar més espai desaprofitat (fragmentació interna).    

Per mostrat els blocs haurem de especificar quina partició sobre tot. La comanda és la següent:
```
tune2fs -l /dev/sda2 | grep Block
```
![chmod](./fotos/m5.png)

#### FRAGMENTACIÓ INTERNA
La fragmentació interna es produeix quan un fitxer no omple completament un bloc assignat, deixant espai sense utilitzar. Aquest espai es considera desaprofitat. La mida del bloc és clau per minimitzar aquest tipus de fragmentació. Si reduïm la mida dels blocs, es pot disminuir la fragmentació interna, però això pot impactar negativament el rendiment, ja que el sistema haurà de gestionar més blocs.   

1. Seguidament, crearem un fitxer nou anomenat hola, en el que escriurem "bon dia". Després comprovarem que existeix amb un "ls" i mostrarem el contigut per terminal amb "cat". Per demostrar la fragmentació interna executarem la comanda "du -b hola" i "du -sh hola". Podem comprovar que en la primera comanda mostra un 8  que vol dir que el fitxer ocupa 8 Bytes, en la segona comanda mostra la mida real que ocupa el fitxer, aquesta és 4Kb.    
```
echo "bon dia" > hola
```
```
ls
```
```
cat hola
```
```
du -b hola
```
```
du -sh hola
```
![chmod](./fotos/m9.png)

2. Per últim, si revisem per GUI els parametres del fitxers, ens mostra 8 Bytes.
![chmod](./fotos/m8.png)


#### FRAGMENTACIÓ EXTERNA
La fragmentació externa passa quan els fitxers es guarden en blocs dispersos en lloc de ser contigus. Això afecta el rendiment, ja que es necessiten més operacions per accedir a les dades. Aquesta situació és més habitual en dispositius d'emmagatzematge que han estat utilitzats durant molt de temps sense una reorganització (per exemple, una desfragmentació).   

Aquesta es pot resoldre fent una desfragmentació, aquesta l'aconseguirem executant la comanda "e4defrag -c /dev/sda2" per visualitzar el que es necessita desfragmentar. Tot seguit per realitzar el proces escriurem la mateixa comanda, però sense el parametre "-c". D'aquesta manera aconseguirem organitzar el fitxers i augmentar el rendiment del disc. 
```
e4defrag -c /dev/sda2
```
```
e4defrag /dev/sda2
```
![chmod](./fotos/m11.png)
![chmod](./fotos/m12.png)
![chmod](./fotos/m13.png)

---

### Tipus de formateig
Hi ha tres tipus principals de formatatge, que es diferencien en la manera com preparen el dispositiu i tracten els blocs defectuosos:

* Formatatge de baix nivell: És un procés lent que organitza els sectors físics i reescriu tota la informació. Marca els blocs defectuosos i elimina completament totes les dades, recuperant l'estructura física del dispositiu. Sovint és realitzat pels fabricants.

* Formatatge intermig: No esborra les dades existents, però analitza el dispositiu i marca els blocs defectuosos perquè no s’utilitzin en el futur. És útil per diagnosticar problemes sense perdre informació.

* Formatatge ràpid: És molt més veloç perquè no comprova ni marca blocs defectuosos ni esborra les dades físicament. Només elimina l'índex del sistema de fitxers, fent que els fitxers semblin esborrats però encara estiguin presents físicament fins que es sobreescriguin.

La diferència principal entre aquests tipus és el tractament de les dades i dels blocs defectuosos, així com la velocitat i la profunditat del procés.

---

### Creacio de particions i formateig
1. Per començar, afegirem un disc dur de 2 GB i executarem la comanda "fdisk -l", per revisar que detecta el disc.
```
fdisk -l
```
![chmod](./fotos/1c.png)

2. Seguidament, crearem una particio i utilitzarem la mitad del disc dur.
```
fdisk /dev/sdb
```
![chmod](./fotos/2c.png)

3. Una vegada fet, revisarem una altra vegada amb el "fdisk -l" que ara el disc te una nova particio, la sdb1.
```
fdisk -l
```
![chmod](./fotos/3c.png)
![chmod](./fotos/4c.png)

4. El següent que farem és formatar la nova particio en format ext4 i amb mida de block 2048.
```
mkfs.ext4 -b 2048 /dev/sdb1
```
![chmod](./fotos/5c.png)

5. Com a comprovació haurem d'executar la comanda següent, la qual mostra la mida de block de la particio sdb1, per comprovar que el parametre -b de la comanda anterior ha funcionat: 
```
tune2fs -l /dev/sdb1 | grep Block
```
![chmod](./fotos/6c.png)

---

### Muntatge de particions
#### TEMPORAL
1. Per fer un muntatge temporal primer haurem de crear una carpeta en la que afegirem un nou fitxer, anomenat "hola". Seguidament executarem la comanda que fa possible el muntatge temporal "mount -t ext4 /dev/sdb1 /var/particio1". Si tornem a visualitzar el contigut de la carpeta veurem que el fitxer "hola", ja no està, això no vol dir que estigui esborrat sinó que al muntar la carpeta desapareix. A més per verificar que un muntatge està correctament realitzat veurem que apareix lost+found dins del directori.
```
cd /var
```
```
mkdir particio1
```
```
cd particio1/
```
```
touch hola
```
```
mount -t ext4 /dev/sdb1 /var/particio1
```
![chmod](./fotos/mt1.png)

2. Seguidament, quan creem fitxers dins del directori muntat, una vegada es desmunta desapareixen, però no s'esborren.
```
cd particio1/
```
```
touch adeu
```
![chmod](./fotos/mt2.png)

---

#### DEFINITIVA

1. Per començar, si volem un muntatge definitiu haurem de afegir una nova linia al fitxer /etc/fstab. 
```
nano /etc/fstab
```
```
/dev/sdb1   /var/particio1  ext4    defaults    0   0
```
![chmod](./fotos/md1.png)
![chmod](./fotos/md2.png)

2. Una vegada acabat reiniciarem la vm i una vegada es torne a encendre carregara el muntatge.     
```
reboot
```
![chmod](./fotos/md3.png)

3. Seguidament si comprovem el directori veurem que ja està muntat.
```
sudo su
```
```
cd /var
```
```
ls particio1/
```
![chmod](./fotos/md4.png)

---

### Comparticio de carpeta a traves de servidor Samba

La compartició de carpetes a través de Samba és una manera eficient i flexible de permetre que diferents dispositius d’una xarxa, independentment del seu sistema operatiu (Windows, Linux, macOS), accedeixin a recursos compartits com fitxers i carpetes. Samba és un programari de codi obert que implementa el protocol SMB/CIFS, facilitant la comunicació i la transferència de dades entre ordinadors de diverses plataformes. Aquesta funcionalitat és àmpliament utilitzada tant en entorns domèstics com empresarials per compartir dades de manera segura i còmoda.

---

#### EXT4 ~ Ubuntu
(Fourth Extended Filesystem) és un sistema de fitxers avançat utilitzat principalment en Linux, que ofereix millores significatives en rendiment, escalabilitat i fiabilitat en comparació amb els seus predecessors ext2 i ext3. És capaç de gestionar sistemes de fitxers de fins a 1 exabyte i fitxers individuals de fins a 16 terabytes. Inclou característiques com el journaling per garantir la integritat de les dades, l’al·locació retardada per optimitzar l’ús de l’espai i el control de fragmentació per millorar l’eficiència. Gràcies a aquestes funcionalitats, ext4 s’ha convertit en un dels sistemes de fitxers més utilitzats en entorns Linux.

1. El primer que haurem de fer és canviar l'adaptador de xarxa a pont.
![chmod](./fotos/ex1.png)
![chmod](./fotos/ex2.png)

2. Seguidament, instal·larem a la màquina real el smbclient.
```
sudo apt install smbclient
```
![chmod](./fotos/ex3.png)

3. Després tornarem a la vm i instal·larem nautilus-shared.
```
sudo apt install nautilus-share
```
![chmod](./fotos/ex4.png)

4. Per utilitzar-lo haurem de fer clic sobre un directori i escollir l'opcio recursos compartits.
![chmod](./fotos/ex5.png)

5. Aqui veurem que tenim diferents opcions de permissos, però si intentem aplicarlos veurem que realment no podem.
![chmod](./fotos/ex6.png)
![chmod](./fotos/ex7.png)
![chmod](./fotos/ex8.png)

6. Per compartir recursos hi ha una millor forma que amb nautilus-shared i aquesta és samba. Per això haurem de instal·lar-lo a la vm.      
```
sudo apt install samba
```
![chmod](./fotos/ex9.png)

7. Per poder afegir un nou recurs haurem d'anar a smb.conf, aqui anirem fins al final del fitxer i afegirem totes aquestes linies, que com podem veure son per definir la ruta, l'usuari, els permissos, etc.
```
nano /etc/samba/smb.conf
```
![chmod](./fotos/ex10.png)
![chmod](./fotos/ex11.png)

8. Una vegada fet haurem de reinciar el servei samba amb la següent comanda:
```
systemctl restart smbd nmbd
```
![chmod](./fotos/ex12.png)

9. Després anirem al directori i li canviarem un parell de coses: permissos (que en aquest cas, són totalment permissius) i usuari + grup propietari (aquest seran nobody:nogroup, per a que qualsevol usuari pugui accedir i crear).
```
cd /var
```
```
ls -l
```
```
chmod 777 particio1/
```
```
chown nobody:nogroup particio1/
```
```
ls -l | grep particio1
```
![chmod](./fotos/ex13.png)

10. Seguidament crearem l'usuari que haviem deifnit abans en el fitxer smb.conf, anonemat "platano". Després li assignarem una contrasenya per al samba.
```
adduser platano
```
```
smbpasswd -a platano
```
![chmod](./fotos/ex14.png)
![chmod](./fotos/ex15.png)

11. Tot seguit, visutalitzarem des de la maquina real els recursos commpartits del servidor (maquina virtual), veurem que ens apareix el directori en qüestió.
```
sudo smbclient -L //192.168.203.208
```
![chmod](./fotos/ex16.png)
![chmod](./fotos/ex17.png)

12. A partir de la interficie grafica anirem a fitxers, altres ubicacions i afegirem la següent linia en el recuadre que marca la captura: smb://192.168.203.208/particio1.
```
smb://192.168.203.208/particio1
```
![chmod](./fotos/ex18.png)

13. Després afegirem l'usuari "platano" i la contrasenya que hem assignat per al samba anteriorment. Seguidament ja estarem dins del directori.     
![chmod](./fotos/ex19.png)
![chmod](./fotos/ex20.png)

14. Per últim, farem unes proves de connexió. El que haurem de fer és crear una carpeta o fitxer des de la maquina real i després comprovar al servidor que s'han realitzat els canvis a temps real.
![chmod](./fotos/ex21.png)
![chmod](./fotos/ex22.png)
![chmod](./fotos/ex23.png)

---

#### NTFS ~ Windows
(New Technology File System) és un sistema de fitxers desenvolupat per Microsoft, utilitzat principalment en sistemes Windows, que destaca per la seva seguretat, eficiència i funcionalitats avançades. Pot gestionar volums de fins a 16 exabytes i fitxers de fins a 256 terabytes, a més d’integrar un sistema de permisos avançats basats en ACL per controlar l’accés a fitxers i carpetes. També inclou journaling per garantir la integritat davant fallades, així com compressió i xifratge de fitxers mitjançant EFS. Gràcies a aquestes característiques, NTFS és el sistema de fitxers per defecte en les versions modernes de Windows.

1. Per començar, comprovarem l'estat del disc amb fdisk -l, com podem observar queda encara la mitad.
```
fdisk -l
```
![chmod](./fotos/nt1.png)

2. Per tant, crearem l'altra particio.
```
fdisk /dev/sdb
```
```
fdisk -l
```
![chmod](./fotos/nt2.png)
![chmod](./fotos/nt3.png)

3. Seguidament la formatarem, però en aquest cas NO serà en ext4 sinó en NTFS.
```
mkfs.ntfs /dev/sdb2
```
![chmod](./fotos/nt4.png)

4. Una vegada fet crearem el directori particio2 i crearem el fitxer hola (com a la particio1).
```
cd /var
```
```
mkdir particio2
```
```
cd particio2
```
```
touch hola
```
![chmod](./fotos/nt5.png)

5. Tot seguit, farem un mutatge definitiu al fitxer fstab. Com podem comprovar aqui també serà necessari canviar ext4 per NTFS.
```
/dev/sdb2   /var/particio2  ntfs    defaults    0   0
```
![chmod](./fotos/nt6.png)

6. Seguidament afegirem un nou recurs compartit al fitxer smb.conf, aquest tindrà un usuari diferent anomenat "fresa". Quan acabessim haurem de reinciar el servei samba.
```
systemctl restart smbd nmbd
```
![chmod](./fotos/nt8.png)
![chmod](./fotos/nt9.png)

7. Després canviarem permissos i propietaris a la carpeta que volem compartir, però si ens fixem quan reivsem el resultat no s'apliquen els canvis de propietaris, això és perquè la particio es NTFS.
```
chmod 777 particio2
```
![chmod](./fotos/nt10.png)

8. Per poder solucionar-ho haurem d'anar també al fstab i afegir nobody, nogroup a la linia de muntatge.
```
/dev/sdb2   /var/particio2  ntfs    defaults,uid=nobody,gid=nogroup    0   0
```
![chmod](./fotos/nt11.png)
![chmod](./fotos/nt12.png)

9. Una vegada fet, haurem de crear l'usuari "fresa" i afegir una contrasenya de samba especifica del usuari.
```
adduser fresa
```
```
smbpasswd -a fresa
```
![chmod](./fotos/nt13.png)
![chmod](./fotos/nt14.png)

10. Ara des de la maquina real comprovarem els recursos compartits del servidor.
```
sudo smbclient -L //192.168.1.155
```
![chmod](./fotos/nt15.png)

11. Ens connectarem amb l'usuari fresa i ja tindrem acces. Per comprovar-ho crearem la carpeta "prova".
![chmod](./fotos/nt16.png)
![chmod](./fotos/nt17.png)

12. Després anirem al servidor i veurem que l'carpeta esta creada.
![chmod](./fotos/nt18.png)

13. Seguidament, ens connectarem des de Windows, per fer-ho haurem de estar amb una vm en adaptador pont. Despés afegirem una nova unitat de xarxa, qual portara la ruta "\\\192.168.1.155\particio2". A més haurem de marcar l'opció "Conectar con otras credenciales" sinó no funcionarà.      
![chmod](./fotos/nt20.png)![chmod](./fotos/nt21.png)

14. Tot seguit, ficarem les credencials de l'usuari fresa i ja tindrem acces al recurs compartit.
![chmod](./fotos/nt22.png)
![chmod](./fotos/nt23.png)

15. Per últim, crearem una carpeta nova des de windows i comprovarem que apareix tant al servidor com a la maquina real.
![chmod](./fotos/nt24.png)
![chmod](./fotos/nt25.png)
![chmod](./fotos/nt26.png)

---
## Còpia de seguretat i automatització de tasques

---

## Quotes de disc
Les quotes de disc a Ubuntu són una eina que permet limitar la quantitat d'espai en disc que pot utilitzar cada usuari o grup al sistema. Això és útil per evitar que un usuari ocupi tot l’espai disponible i per gestionar millor els recursos en entorns compartits, com servidors o ordinadors multiusuari. Les quotes es poden configurar per definir límits tant en la quantitat de fitxers com en la mida total que es pot emmagatzemar, assegurant un ús més equilibrat i controlat de l'espai disponible.

1. El primer que haurem de fer és afegir un disc nou, en aquest cas de 5 GB.      
```
fdisk -l
```
![chmod](./fotos/q1.png)

2. Seguidament farem una unica particio en tot el disc.    
```
fdisk /dev/sdc
```
![chmod](./fotos/q2.png)

3. Després la formatarem amb ext4.      
```
mkfs.etx4 /dev/sdc1
```
![chmod](./fotos/q3.png)

4. Tot seguit comprovarem que la particio esta creada.      
```
fdisk -l
```
![chmod](./fotos/q4.png)

5. A continuacio farem una actualitzacio del repositori de paquets i instal·larem **quota**.        
```
sudo apt update
```
```
sudo apt install quota
```
![chmod](./fotos/q5.png)
![chmod](./fotos/q6.png)

6. Seguidament crearem una carpeta en /mnt anomenada dades.     
```
cd /mnt
```
```
mkdir dades
```
![chmod](./fotos/q7.png)

7. Posteriorment, anirem a afegir una nova linia a /etc/fstab per muntar la carpeta creada a la particio del disc de 5GB. Important afegir usrquota i grpquota ja que aixi podrem establir quotes.      
```
/dev/sdc1   /mnt/dades  ext4    defaults,usrquota,grpquota  0   0
```
![chmod](./fotos/q8.png)

8. Una vegada fet reinciarem el sistema i comprovarem que el directori ja esta muntat. A més afegirem dos comandes crucials `quotacheck -cug /mnt/dades` que verifica i crea els fitxers de quotes per a usuaris i grups en un sistema de fitxers, i `quotaon /mnt/dades` que activa la gestió d’aquestes quotes. També crearem un usuari nou al que establirem quotes, anomenat usuari1.       
```
reboot
```
```
ls /mnt/dades
```
```
quotacheck -cug /mnt/dades
```
```
quotaon /mnt/dades
```
```
ls /mnt/dades
```
```
adduser usuari1
```
![chmod](./fotos/q9.png)
![chmod](./fotos/q10.png)

9. Després executarem la comanda `quota -u usuari1` que mostra l’ús del disc i els límits de quota assignats a un usuari específic. Com podem comprovar el resultat marca que no en té cap.     
```
quota -u usuari1
```
![chmod](./fotos/q11.png)

10. Per afegir quotes a un usuari haurem de executar la comanda `edquota -u usuari1`. Aqui ens mostrara diferents columnes, nosaltres només haurem de tindre en compte dos: soft i hard. El soft limit és un límit flexible que es pot superar temporalment durant un període de gràcia, mentre que el hard limit és un límit estricte que no es pot superar mai. Això permet advertir l'usuari abans d'arribar al límit màxim absolut. En aquest cas hem establert com a soft limit 1024 i en hard 2048.       
```
edquota -u usuari1
```
![chmod](./fotos/q12.png)
![chmod](./fotos/q13.png)

11. Seguidament, executarem la comanda `repquota /mnt/dades` aquesta mostra un informe detallat de l’ús de disc i les quotes de usuaris i grups en un sistema de fitxers.       
```
repquota /dev/sdc1
```
![chmod](./fotos/q14.png)

12. Tot seguit, afeguirem permissos 777 a la carpeta dades.
```
cd /mnt
```
```
chmod 777 dades/
```
![chmod](./fotos/q16.png)

13. A continuació entrarem amb usuari1 i crearem un fitxer especificant tamany i contingut. Si fem un `quota -u usuari1` veurem que segons el tamany assignat del fitxer el resultat determina l'espai utilitzat.       
```
dd if=/dev/zero of=test bs=1K count=800
```
```
quota -u usuari1
```
![chmod](./fotos/q17.png)

14. Si ho comprovem des de root amb repquota també ens indicara el mateix espai i l'usuari que l'ocupa.         
```
repquota /dev/sdc1
```
![chmod](./fotos/q18.png)

15. Ara tornarem a ser usuari1 i crearem 2 fitxers més per observar que passa si sobre passem el limit. Com podem observar al fitxer test2 salta l'avís, però podem continuar creant més fitxers. Com és possible? El sistema accepta el fitxer que estàs creant però realment està buit, per tant s'estan aplicant les restriccions de quota de manera correcta.       
```
dd if=/dev/zero of=test1 bs=1K count=800
```
```
dd if=/dev/zero of=test2 bs=1K count=800
```
```
dd if=/dev/zero of=test3 bs=1K count=800
```
![chmod](./fotos/q19.png)
![chmod](./fotos/q20.png)
![chmod](./fotos/q21.png)
![chmod](./fotos/q22.png)
![chmod](./fotos/q23.png)

16. Si ho comprovem, podrem observar que indica 6 dies de gràcia, els grace days només són aplicables al soft limit, indicant el temps durant el qual es pot excedir aquest límit abans que es comencin a imposar restriccions.     
```
quota -u usuari1
```
![chmod](./fotos/q24.png)

17. Com a dada interessant si no volem grace days amb la comanda `edquota -t` podem modificar-los a 0.      
```
edquota -t
```
![chmod](./fotos/q26.png)
![chmod](./fotos/q25.png)

18. Ara per poder fer la següent part eliminarem tots el fitxers creats i revisarem la quota.        
```
cd /mnt/dades
```
```
rm tes*
```
```
ls
```
```
quota -u usuari1
```
![chmod](./fotos/q28.png)

19. Per poder mostrar de forma més clara com funciona quota, delimitarem soft a 100 i hard a 400.       
```
edquota -u maria
```
![chmod](./fotos/q30.png)
![chmod](./fotos/q32.png)

20. Seguidament, descarregarem una foto d'internet i l'apegarem a /mnt/dades, com podem comprovar si la foto passa el limit salta un error de quota.        
![chmod](./fotos/q31.png)

21. Però si ens donem compte la foto segueix al directori i a més és visible, això és perquè li baixa la qualitat per a que pugui d'alguna forma entrar dins del limit de la quota.     
![chmod](./fotos/q34.png)

22. Si provem de tornar a copiar la foto aquesta, ja no serà visible, perquè la quota ja està plena per l'altra.        
![chmod](./fotos/q35.png)
![chmod](./fotos/q36.png)

---
