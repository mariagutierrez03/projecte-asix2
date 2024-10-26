# Gestió d'usuaris i serveis

Per a la documentació completa visita [mkdocs.org](https://www.mkdocs.org).

---
## Introducció

Iniciarem el projecte amb la instal·lació d’Ubuntu Linux en un entorn de màquina virtual, assegurant que el sistema operatiu es configura correctament per gestionar usuaris, grups i polítiques de contrasenyes. En aquesta fase, ens centrarem en la creació i gestió de comptes d'usuari locals, l'assignació de permisos a grups, així com la definició de polítiques de seguretat per a contrasenyes i accessos.

Un cop completada la configuració inicial, avançarem amb la instal·lació i gestió de serveis essencials que són crucials per al funcionament òptim del sistema. Això inclou la configuració de serveis i processos, l'optimització de l'ús de recursos i l'administració de serveis actius d'acord amb les necessitats del sistema.

A continuació, ens ocuparem de la creació i gestió de particions i sistemes de fitxers, garantint una distribució adequada de l'espai, així com l'aplicació de quotes de disc i la implementació de còpies de seguretat automàtiques per assegurar la integritat de les dades.

Finalment, realitzarem proves exhaustives per verificar el correcte funcionament del sistema, incloent la gestió d'usuaris, grups i serveis, així com la integritat dels fitxers, sistemes de particions i quotes de disc. Documentarem detalladament cada pas del procés, que inclourà la creació de comptes d'usuari, la configuració de serveis, l'administració de particions, i el procés de recuperació en cas de desastres, acompanyant-ho de captures de pantalla per il·lustrar les configuracions i ajustaments realitzats durant el procés.

![intro](./fotos/intro4.jpg)

---
## Gestió de processos

---
## Gestió d'usuaris i grups
### Els fitxers més importants
- etc/passwd
- etc/shadow (si al fitxer surt ! es que usuari bloquejat)
- etc/gshadow (la difirencia entre etc/groups es que es veu l’admin)
- etc/groups
---

### Crear i eliminar usuaris
#### USERADD
1. 
![useradd](./fotos/s1.png)
![useradd](./fotos/s2.png)

#### ADDUSER
#### USERDEL
1. 
![useradd](./fotos/s3.png)
![useradd](./fotos/s4.png)
![useradd](./fotos/s5.png)
![useradd](./fotos/s6.png)

---

#### Afegir usuaris per GUI
![useradd](./fotos/s7.png)
![useradd](./fotos/s8.png)

---

### Log usuari per GUI i terminal
![useradd](./fotos/s9.png)
![useradd](./fotos/s10.png)
![useradd](./fotos/s11.png)
![useradd](./fotos/s12.png)

---

### Bloquejar i desbloquejar usuaris
![useradd](./fotos/s13.png)
![useradd](./fotos/s14.png)
![useradd](./fotos/s15.png)
![useradd](./fotos/s16.png)
![useradd](./fotos/s17.png)
![useradd](./fotos/s19.png)


---

### Modificar nom d’un usuari
![useradd](./fotos/s20.png)
![useradd](./fotos/s21.png)
![useradd](./fotos/s22.png)
![useradd](./fotos/s23.png)
![useradd](./fotos/s24.png)
![useradd](./fotos/s25.png)

---

### Crear i eliminar grups
#### GROUPADD
![useradd](./fotos/s26.png)
![useradd](./fotos/s27.png)
![useradd](./fotos/s30.png)
![useradd](./fotos/s31.png)

#### ADDGROUP
![useradd](./fotos/s34.png)
![useradd](./fotos/s35.png)


#### GROUPDEL
![useradd](./fotos/s32.png)
![useradd](./fotos/s31.png)

#### DELGROUP
![useradd](./fotos/s37.png)
![useradd](./fotos/s36.png)

---

### Afegir i treure usuaris de grups
#### USERMOD
![useradd](./fotos/s38.png)
![useradd](./fotos/s39.png)
![useradd](./fotos/s50.png)
![useradd](./fotos/s51.png)

#### GPASSWD
![useradd](./fotos/s40.png)
![useradd](./fotos/s41.png)
![useradd](./fotos/s45.png)
![useradd](./fotos/s46.png)

#### ADDUSER
![useradd](./fotos/s42.png)
![useradd](./fotos/s43.png)
![useradd](./fotos/s47.png)
![useradd](./fotos/s48.png)

---

### Modificar grup principal d’un usuari

![useradd](./fotos/s52.png)

---
## Gestió de permisos

---
## Sistemas de fitxers i particions

---
## Còpia de seguretat i automatització de tasques

---
## Quotes de disc



---
