# 🖥️ Lab Active Directory – NovaTech

## 📌 Présentation

Ce projet consiste à mettre en place un environnement Active Directory pour une entreprise fictive nommée **NovaTech**.

L'objectif de cette première partie était de créer un domaine Windows, organiser les utilisateurs par service et mettre en place un contrôle d'accès à un dossier partagé en fonction de l'appartenance à un groupe Active Directory.

---

## 🏗️ Infrastructure

L'environnement a été réalisé sous **VirtualBox** avec :

- **Windows Server 2025** : contrôleur de domaine `DC01`
- **Windows 11 Pro** : poste client membre du domaine
- Domaine : `novatech.local`
- Adresse IP de DC01 : `192.168.10.10`
- Adresse IP du poste client : `192.168.10.20`
- Réseau interne VirtualBox dédié au lab

---

## 🔐 Mise en place d'Active Directory

Installation et configuration des rôles :

- Active Directory Domain Services (AD DS)
- DNS
- Création de la forêt `novatech.local`
- Promotion de `DC01` en contrôleur de domaine

Une structure d'unités d'organisation (OU) a ensuite été créée afin de représenter les différents services de NovaTech :

- Direction
- Ressources humaines
- Commercial
- Marketing
- Informatique

---

## 👥 Gestion des utilisateurs et des groupes

Création de plusieurs comptes utilisateurs, notamment :

- **Sophie Martin** → Ressources humaines
- **Lucas Bernard** → Marketing

Création de groupes de sécurité :

- `GG_RH`
- `GG_Marketing`

Les utilisateurs ont ensuite été ajoutés au groupe correspondant à leur service.

Cette organisation permet d'attribuer les autorisations aux **groupes** plutôt que directement aux utilisateurs.

---

## 📁 Partage réseau et permissions NTFS

Un dossier destiné au service RH a été créé sur DC01 :

`C:\Partages\RH`

Il est accessible sur le réseau via :

`\\DC01\RH`

Les permissions NTFS ont été configurées afin que le groupe **GG_RH** dispose des droits nécessaires sur le dossier.

L'objectif est d'obtenir le fonctionnement suivant :

Utilisateur → Groupe AD → Permission sur la ressource

---

## 🧪 Tests réalisés

Le poste Windows 11 Pro a été intégré au domaine `novatech.local`.

### Test avec Sophie Martin

Connexion avec le compte Active Directory de Sophie :

`NOVATECH\Sophie`

Sophie étant membre de `GG_RH`, elle peut accéder au partage :

`\\DC01\RH`

✅ **Accès autorisé**

Elle peut consulter le document confidentiel présent dans le dossier RH.

### Test avec Lucas Bernard

Connexion avec le compte Active Directory de Lucas.

Lucas appartient à `GG_Marketing` et ne possède aucun droit sur le dossier RH.

Tentative d'accès à :

`\\DC01\RH`

❌ **Accès refusé**

Le cloisonnement des ressources entre les services fonctionne donc correctement.

---

## 🎯 Compétences mises en pratique

Ce lab m'a permis de pratiquer :

- Installation et configuration d'Active Directory
- Promotion d'un serveur en contrôleur de domaine
- Configuration DNS
- Adressage IPv4 statique
- Intégration d'un poste Windows à un domaine
- Création et organisation d'OU
- Gestion des utilisateurs Active Directory
- Gestion des groupes de sécurité
- Gestion des permissions NTFS
- Création de partages SMB
- Contrôle d'accès basé sur les groupes
- Tests d'authentification et d'autorisation
- Diagnostic réseau avec `ping`, `nslookup` et `arp`

---

## ➡️ Suite du projet

La prochaine étape du lab sera consacrée aux **GPO (Group Policy Objects)** afin d'appliquer automatiquement des stratégies aux utilisateurs et aux ordinateurs du domaine NovaTech.
