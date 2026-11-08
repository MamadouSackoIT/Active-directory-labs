# 🖥️ Lab Active Directory — NovaTech

## 📌 Présentation

Ce laboratoire reproduit une petite infrastructure d'entreprise avec **Windows Server 2025 et Active Directory**.

L'objectif était de mettre en pratique l'administration d'un domaine Windows : utilisateurs, groupes, partages réseau, permissions et stratégies de groupe (GPO).

## 🏗️ Environnement

- **Windows Server 2025** — Contrôleur de domaine DC01
- **Windows 11 Pro** — Poste client
- Domaine : `novatech.local`
- Serveur : `192.168.10.10`
- Client : `192.168.10.20`
- Virtualisation : **VirtualBox**

## 👥 Active Directory

J'ai créé plusieurs unités d'organisation pour représenter les services de l'entreprise :

- Direction
- Ressources humaines
- Commercial
- Marketing
- Informatique

Des utilisateurs et groupes de sécurité ont ensuite été créés, notamment :

- **Sophie Martin** → Ressources humaines → `GG_RH`
- **Lucas Bernard** → Marketing → `GG_Marketing`

## 📂 Partage réseau

Création d'un dossier partagé pour les Ressources humaines :

`\\DC01\RH`

Les permissions NTFS permettent aux membres de `GG_RH` d'accéder au dossier.

Le test avec Lucas Bernard permet également de vérifier qu'un utilisateur Marketing ne disposant pas des autorisations nécessaires ne peut pas accéder à la ressource.

## 🔐 Stratégies de groupe — GPO

Deux GPO ont été mises en place.

### GPO Ressources humaines

`GPO_RH_Restriction_PanneauConfiguration`

Cette stratégie empêche les utilisateurs RH d'accéder au **Panneau de configuration et aux Paramètres Windows**.

Le fonctionnement a été testé avec le compte de **Sophie Martin**.

### GPO Marketing

`GPO_Marketing_VerrouillageSession`

Cette stratégie applique aux utilisateurs Marketing :

- activation de l'écran de veille ;
- protection par mot de passe ;
- verrouillage après **5 minutes d'inactivité**.

La GPO a été testée avec **Lucas Bernard**.

La commande `gpresult /r` confirme son application et le verrouillage automatique de la session a été vérifié.

## 🛠️ Compétences travaillées

- Active Directory Domain Services
- Windows Server
- DNS
- Utilisateurs et groupes
- Unités d'organisation (OU)
- Permissions NTFS
- Partages réseau
- Intégration d'un poste au domaine
- GPO
- `gpupdate /force`
- `gpresult /r`
- VirtualBox

## 🎯 Résultat

Ce laboratoire m'a permis de construire et administrer un **petit environnement Active Directory fonctionnel**, puis de mettre en place des règles d'accès et de sécurité différentes selon les services de l'entreprise.
