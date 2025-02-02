# Administració de dominis i seguretat

Per a la documentació completa visita [mkdocs.org](https://www.mkdocs.org).

---
## Introducció


![intro](./fotos/intro.jpg)

---

## Instal·lació domini ldap

Un domini LDAP és una estructura que ens ajuda a gestionar usuaris, grups i recursos dins d'una xarxa de manera centralitzada. Funciona com un directori organitzat jeràrquicament, similar a un arbre, on podem trobar usuaris, grups, i altres recursos (impressores, servidors) organitzats en Unitats Orgàniques (UOs), com si fossin carpetes dins del domini.

Estructura bàsica d'un domini LDAP:

* UOs: Contenen grups d'usuaris i recursos (ex. "Recursos Humans", "TI").
* Usuaris: Representen les persones de la xarxa, amb atributs com nom, correu, contrasenya, etc.
* Grups: Col·leccions d'usuaris amb permisos similars (ex. "Administradors").
* Recursos: Impressores, servidors, etc.

Per crear l'esquema bàsic d'un domini LDAP tenim dues opcions:

* Fitxers LDIF: Creem un fitxer amb la informació (usuaris, grups, etc.) i el carreguem al servidor LDAP. És útil per afegir moltes dades de cop.

* Comanda `ldapadd`: Utilitzem aquesta comanda per afegir directament la informació al servidor LDAP. Llegirà un fitxer LDIF i afegirà les dades al domini.

**Polítiques de Grup (GPOs)**

Els GPOs permeten aplicar configuracions i regles comunes a grups d'usuaris o dispositius dins del domini, com limitacions d'accés o configuracions de seguretat.



---

1. En la màquina server ubuntu desktop 24 haurem de canviar la interifície a NatNetwork. 
![ldap](./fotos/ldap1.png)

2. Seguidament, revisarem la ip i la farem estàtica, ja que, els servidors sempre han de tindre una ip fixa.
```
ip a
```
```
google.com
```
![ldap](./fotos/ldap2.png)
![ldap](./fotos/ldap3.png)
![ldap](./fotos/ldap4.png)

3. A continuació, farem un `apt update` i `apt upgrade`.
```
apt update
```
```
apt upgrade
```
![ldap](./fotos/ldap5.png)
![ldap](./fotos/ldap6.png)

4. Després anirem al moodle descarregarem el comprimit arxius.zip i el descomprimirem amb la comanda `unzip`, com podem observar té diferents arxius de configuració.
```
cd Baixades/
```
```
unzip arxius.zip
```
```
ls
```
![ldap](./fotos/ldap7.png)
![ldap](./fotos/ldap8.png)

5. Tot seguit, canviarem el hostname de la nostra vm (aquest pas és opcional). A més al fitxer /etc/hosts tornarem a canviar el hostname si ho hem fet previament i també afegirem una nova linia en la que indicarem la ip del server, el nostre hostname, el nom del domini en aquest cas "asix.cat" i per últim afegirem una altra vegada el hostname. 
```
nano /etc/hosts
```
```
nano /etc/hostname
```
![ldap](./fotos/ldap9.png)
![ldap](./fotos/ldap10.png)
![ldap](./fotos/ldap11.png)

6. Seguidament, reiniciarem la vm i una vegada encesa comprovem el hostname.
```
reboot
```
```
hostname
```
![ldap](./fotos/ldap12.png)
![ldap](./fotos/ldap13.png)

7. Ara instal·larem els paquets slapd i ldap-utils.
```
apt install slapd ldap-utils
```
![ldap](./fotos/ldap14.png)

8. Una vegada a inciada l'instal·lació assignarem una contrassenya a l'administrador.       
![ldap](./fotos/ldap15.png)
![ldap](./fotos/ldap16.png)

9. Després amb la comanda slapcat mirarem la informació del slapd, com podem comprovar no hi ha cap domini configurat.
```
slapcat
```
![ldap](./fotos/ldap17.png)

10. En aquest cas tornarem a configurar slapd. Una vegada dins clicarem en "No" per poder continuar, després escriurem el nom del domini dues vegades, a més tornarem a configurar la contrasenya i clicarem en "Sí" dues per afegir la configuració actual.        
![ldap](./fotos/ldap20.png)
![ldap](./fotos/ldap21.png)
![ldap](./fotos/ldap22.png)
![ldap](./fotos/ldap23.png)
![ldap](./fotos/ldap24.png)
![ldap](./fotos/ldap25.png)
![ldap](./fotos/ldap26.png)

11. Seguidament, si tornem a fer slapcat veurem que s'ha actulitzat la informació del domini.
```
slapcat
```
![ldap](./fotos/ldap27.png)

12. Ara el que farem és editar el fitxer de configuració "uo.ldif", aquí definirem les unitats organitzatives (OU) dins del directori LDAP, que serveixen per agrupar i organitzar objectes com usuaris, grups o altres unitats, mantenint una estructura jeràrquica clara i coherent.
```
nano uo.ldif
```
![ldap](./fotos/ldap28.png)
![ldap](./fotos/ldap29.png)

13. Tot seguit, editarem el fitxer "grup.ldif", la seva funció és crear i configurar grups dins del directori LDAP, permetent agrupar usuaris amb propòsits específics, com gestionar permisos i accessos de manera eficient.
```
nano grup.ldif
```
![ldap](./fotos/ldap30.png)
![ldap](./fotos/ldap31.png)

14. Per últim, configurarem fitxer "usu.ldif" on definirem els atributs dels usuaris (nom, UID, contrasenya i OU corresponent) per assegurar que cadascun tingui accés al sistema i als recursos necessaris.
```
nano usu.ldif
```
![ldap](./fotos/ldap32.png)
![ldap](./fotos/ldap33.png)
![ldap](./fotos/ldap34.png)

15. Seguidament, afegirem tots el fitxers de configuració i revisarem el slapcat.
```
ldapadd -c -x -D "con=admin,dc=asix,dc=cat" -W -f uo.ldif
```
```
ldapadd -c -x -D "con=admin,dc=asix,dc=cat" -W -f grup.ldif
```
```
ldapadd -c -x -D "con=admin,dc=asix,dc=cat" -W -f usu.ldif
```
```
slapcat
```

    * -x: Connexió simple.
    * -D: Usuari administrador que afegeix dades.
    * -W: Demana la contrasenya de l'usuari.
    * -f: Fitxer LDIF amb les dades a afegir.

    ![ldap](./fotos/ldap36.png)
    ![ldap](./fotos/ldap37.png)
    ![ldap](./fotos/ldap38.png)
    ![ldap](./fotos/ldap39.png)

---

## Unir un client al domini

1. El primer que haurem de fer és canviar l'adaptador de xarxa del Ubuntu Desktop 24 Client a NatNetwork, així estaràn a la mateixa xarxa i es podran comunicar.        
![ldap](./fotos/1u.png)

2. A més revisarem la ip des de terminal per comprovar que no coincideixen i seguidament farem ping al servidor.
```
ip a
```
```
ping 10.0.2.9
```
![ldap](./fotos/2u.png)
![ldap](./fotos/3u.png)

3. A continuació, descarregarem els paquets de ldap client i farem un reconfigure per posar a punt la configuració.
```
apt install libnss-ldap libpam-ldap nscd
```
```
depkg-reconfigure ldap-auth-config
```
![ldap](./fotos/4u.png)
![ldap](./fotos/5u.png)

4. En la primera i segona pantalla haurem de indicar "Sí", després escriurem el nom de domini i configurarem la contrasenya.        
![ldap](./fotos/6u.png)
![ldap](./fotos/7u.png)
![ldap](./fotos/8u.png)
![ldap](./fotos/9u.png)
![ldap](./fotos/10u.png)
![ldap](./fotos/11u.png)

5. Una vegada hem fet tota la configuració anterior en tornara a preguntar i li haurem de indicar "Sí". També escriurem la ip del server a la següent pantalla i tornarem a introduir el domini, després escollirem la versio i continuarem així fins arribar al tipus d'encriptacio que serà l'última pantalla de configuració.        
![ldap](./fotos/12u.png)
![ldap](./fotos/13u.png)
![ldap](./fotos/14u.png)
![ldap](./fotos/15u.png)
![ldap](./fotos/16u.png)
![ldap](./fotos/17u.png)
![ldap](./fotos/18u.png)
![ldap](./fotos/19u.png)
![ldap](./fotos/20u.png)
![ldap](./fotos/21u.png)
![ldap](./fotos/22u.png)
![ldap](./fotos/23u.png)

6. Al finalitzar la configuració haurem d'editar una seria de fitxers com /etc/nsswitch.conf en el que escriurem "ldap compat" davant de les 4 primeres linies, això indica que el sistema ha de buscar la informació en el servidor ldap. 
```
nano /etc/nsswitch.conf
```
![ldap](./fotos/24u.png)
![ldap](./fotos/25u.png)

7. El següent fitxer és /etc/pam.d/common-session en aquest li haurem d'escriure una nova linia. La línia configura que, durant l’autenticació, si l’usuari no té un directori home, aquest es creï automàticament utilitzant com a plantilla el contingut de /etc/skel i aplicant un umask=077 per garantir que els permisos siguin segurs (només accessibles pel propietari).
```
nano /etc/pam.d/common-session
```
![ldap](./fotos/27u.png)

8. Aquest últim fitxer de configuració, no és estrictament necessari en l'última versió d'ubuntu, encara que si estas en versions anteriors serà fundamental. Haurem d'afegir una nova linia, aquesta configura la sessió predeterminada com "ubuntu" i permet l'inici de sessió manual escrivint el nom d'usuari a LightDM.
```
nano /usr/share/lightdm/lightdm.conf.d/50-ubuntu.conf
```
![ldap](./fotos/28u.png)
![ldap](./fotos/29u.png)

9. Seguidament revisarem que l'usuari creat en el servidor està al llistat del client i si és així iniciarem sessió des de terminal. 
```
getent passwd | grep alu1
```
![ldap](./fotos/30u.png)
![ldap](./fotos/31u.png)

10. Per provar que funciona amb interficie grafica reiniciarem la vm i en la pantalla de bloqueig iniciarem sessio amb un usuari no llistat, aquí indicarem username i password. Si tot funciona bé quan obrim un terminal i escribim la comanda "whoami" ens ha de donar l'usuari ldap. 
```
reboot
```
```
whoami
```
![ldap](./fotos/32u.png)
![ldap](./fotos/33u.png)

---

## Canvis en un Ubuntu Server

1. El primer canvi és que el hostname del servidor ha de ser directament el propi nom del domini ldap.       
![ldap](./fotos/1s.png)

2. Seguidament com estem en un entorn sense GUI haurem de editar el fitxer de netplan per afegir una ip estàtica.       
![ldap](./fotos/2s.png)
![ldap](./fotos/3s.png)

3. Una vegada hem acabat comprovarem que la ip és la correcta i farem un ping al exterior per saber si tenim connexió a internet.       
![ldap](./fotos/4s.png)
![ldap](./fotos/5s.png)

---

## Gestió del domini

---

### LDAPSEARCH
1. El primer que farem és provar diferents opcions com buscar un usuari pel uid.
```
ldapsearch -xLLL -b "dc=asix,dc=cat" uid=miguel
```
![ldap](./fotos/g1.png)

2. Seguidament buscarem per uid, però concretant en els camps. Els camps que no existeixent com 'mail' no els mostra.
```
ldapsearch -xLLL -b "dc=asix,dc=cat" uid=miguel dn cn sn mail uid
```
![ldap](./fotos/g2.png)

3. Seguidament llistarem tots el posixGroup.
```
ldapsearch -xLLL -b "dc=asix,dc=cat" objectClass=posixGroup dn
```
![ldap](./fotos/g3.png)

4. A més, podem buscar el numero que hi ha de grups, tenint en compte que el sistema també conta el espais en blanc.
```
ldapsearch -xLLL -b "dc=asix,dc=cat" objectClass=posixGroup dn | wc -l
```
![ldap](./fotos/g4.png)

5. A continuació buscarem a partir de un uid major o igual a 1002.
```
ldapsearch -xLLL -b "dc=asix,dc=cat" "uidNumber>=1002" dn uidNumber
```
![ldap](./fotos/g5.png)

6. Ara buscarem a partir de un 'cn' que comence amb 'M' o qualsevol registre de mail. A més també tenim l'opció de que les dues opcions s'han de complir amb '&' en comptes de '|'.
```
ldapsearch -xLLL -b "dc=asix,dc=cat" "(|(cn=M*)(mail=*))"
```
```
ldapsearch -xLLL -b "dc=asix,dc=cat" "(&(cn=M*)(mail=*))"
```
![ldap](./fotos/g6.png)
![ldap](./fotos/g30.png)

---

### LDAPADD 

#### OPCIÓ 1
Per poder afegir un fitxer ho podem fer d'aquesta manera, la qual només involucra una comanda.
```
ldapadd -x -D "cn=admin,dc=asix,dc=cat" -W -f dades_prova.ldif
```
![ldap](./fotos/g24.png)

#### OPCIÓ 2
La segona opció és afegir una nova linia al fitxer i després executar ldapmodify. 
```
ldapmodify -x -D "cn=admin,dc=asix,dc=cat" -W -f grups.ldif
```
![ldap](./fotos/g25.png)
![ldap](./fotos/g26.png)

---

### LDAPDELETE 

#### OPCIÓ 1
La primera opció per eliminar és només amb la comanda ldapdelete. 
```
ldapdelete -x -D "cn=admin,dc=asix,dc=cat" -W "cn=persones,ou=users,dc=asix,dc=cat"
```
![ldap](./fotos/g27.png)

#### OPCIÓ 2
Com a alternativa, també podem utilitzar ldapmodify.
```
ldapmodify -x -D "cn=admin,dc=asix,dc=cat" -W -f grups.ldif
```
![ldap](./fotos/g28.png)
![ldap](./fotos/g29.png)

---

### LDAPMODIFY  

---

#### CHANGETYPE: MODIFY
1. El primer que farem és afegir les dues ultimes linies al fitxer de configuració i després executar la comanda.
```
ldapmodify -x -D "cn=asix,dc=asix,dc=cat" -W -f proves.ldif
```
![ldap](./fotos/g13.png)
![ldap](./fotos/g14.png)
![ldap](./fotos/g15.png)

2. Seguidament eliminarem d'aquesta manera el camp mail.
```
ldapmodify -x -D "cn=asix,dc=asix,dc=cat" -W -f proves.ldif
```
![ldap](./fotos/g16.png)
![ldap](./fotos/g17.png)

3. També podem optar per una opció així.
```
ldapmodify -x -D "cn=asix,dc=asix,dc=cat" -W -f proves.ldif
```
![ldap](./fotos/g18.png)
![ldap](./fotos/g19.png)

---

#### CHANGETYPE: MODRDN
1. En aquest cas podem també podem utilitzar modrdn amb deleteoldrdn.
```
ldapmodify -x -D "cn=asix,dc=asix,dc=cat" -W -f proves.ldif
```
![ldap](./fotos/g20.png)
![ldap](./fotos/g21.png)

---

## Entorns gràfics

---

## Server NFS

---

### Instal·lació

#### SERVIDOR 

1. Instal·larem el servei nfs-kernel-server i una vegada fet revisarem l'estat del servei.
```
apt update
```
```
apt install nfs-kernel-server
```
```
systemctl status nfs-server
```
![ldap](./fotos/o15.png)
![ldap](./fotos/o14.png)
![ldap](./fotos/o13.png)

#### CLIENT UBUNTU
1. En ubuntu client instal·larem el paquet "nfs-common rpcbind".
![ldap](./fotos/o15.png)
![ldap](./fotos/o19.png)

#### CLIENT WINDOWS 

1. Aquí entrarem dins del "control panel", clicarem en "iconos pequeños" i després en "Programas y caracteristicas"
![ldap](./fotos/o18.png)

2. Després farem clic en "Activar o desactivar las caracteristicas de Windows" dins activarem tottes les caselles de NFS.
![ldap](./fotos/o17.png)

3. Quan acabem ens sortirà un missatge de que els canvis han estat aplicats.
![ldap](./fotos/o16.png)

---

### Compartición carpeta al server y pruebas

1. Primer, crearem la carpeta "compartida" en l'arrel, li ficarem els permissos de propetari nobody:nogroup i permissos total de lectura, escriptura i execució. 
```
cd /
```
```
mkdir compartida
```
```
ls -la | grep compartida
```
```
chown nobody:nogroup compartida/
```
```
chmod -R 777 compartida/
```
![ldap](./fotos/o12.png)

2. A més, entrarem dins del fitxer /etc/exports i afegirem una nova linia.
```
nano /etc/export
```
```
/compartida *(rw,sync,no_subtree_check)
```
![ldap](./fotos/o9.png)

3. Seguidament, entrarem dins de la carpeta i crearem un fitxer anomenat "hola".
```
cd compartida
```
```
touch hola
```
```
ls
```
![ldap](./fotos/o7.png)

4. En windows provarem connexió amb el server.
```
ipconfig
```
![ldap](./fotos/o6.png)

5. Tot seguit, entrarem en "Red" i afegirem la ip del server, de forma que ens sortirà la carpeta.      
![ldap](./fotos/o5.png)

6. A continuació, crearem una carpeta nova dins del recurs compartit.
![ldap](./fotos/o11.png)
![ldap](./fotos/o4.png)

7. Després, anirem al client ubuntu, crearem la carpeta "nfs" a /mnt, afegirem permissos 777 i muntarem la carpeta al servidor. Una vegada fet entrarem dins i crearem un fitxer.
```
cd /mnt
```
```
mkdir nfs
```
```
chmod -R 777 nfs/
```
```
ls nfs/
```
```
mount 10.0.2.9:/compartida /mnt/nfs/
```
```
touch provaubuntu
```
![ldap](./fotos/o3.png)

8. Per últim, revisarem la carpeta al servidor per comprovar que realment estàn els dos fitxers que hem creat amb els diferents clients.
```
cd compartida/
```
```
ls
```
![ldap](./fotos/o1.png)

---

### Perfil Movil (Ubuntu LDAP)

1. El primer que farem és fer un `ls` 


---

## Server SAMBA

---