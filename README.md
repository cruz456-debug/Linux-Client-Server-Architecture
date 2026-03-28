# Linux-Client-Server-Architecture
Déploiement d'une architecture client-serveur 2-tiers sous Ubuntu. Intégration complète d'une stack LAMP (Apache, MySQL, PHP) avec services réseau critiques (DNS BIND9 et DHCP) pour un environnement de test isolé.


# Architecture Client-Serveur 2-Tiers sous Linux
**Projet Académique - Administration Système Linux**
**Etablissement : ISM Dakar (Licence 3 ETSE)**

## Présentation du projet
L'objectif de ce projet était de concevoir et déployer une architecture client-serveur à deux niveaux (2-Tiers) en utilisant exclusivement des environnements Linux (Ubuntu Server et Desktop). Cette infrastructure permet la communication fluide entre un serveur **LAMP** (Linux, Apache, MySQL, PHP) et un client à travers un réseau local isolé.

## Architecture et Composants
Le projet simule un environnement d'entreprise complet avec les services suivants :
* **Serveur Web :** Apache2 hébergeant une interface de saisie dynamique.
* **Base de Données :** MySQL/MariaDB pour le stockage persistant des données formulaires.
* **Serveur DNS (BIND9) :** Résolution du domaine personnalisé `oumou-simon-dylan.local`.
* **Serveur DHCP :** Attribution dynamique des adresses IP dans le sous-réseau `192.168.10.0/24`.

---

## Réalisation Technique

### 1. Configuration Réseau (Netplan & DHCP)
Le serveur possède une IP statique (`192.168.10.2`) tandis que le client reçoit son adresse via le service `isc-dhcp-server`.

```bash
# Extrait de la configuration DHCP (dhcpd.conf)
subnet 192.168.10.0 netmask 255.255.255.0 {
    range 192.168.10.100 192.168.10.150;
    option domain-name "oumou-simon-dylan.local";
    option domain-name-servers 192.168.10.2;
}
```

### 2. Implémentation du Serveur LAMP
Le cœur de l'application est un formulaire PHP traitant les inscriptions et les injectant directement dans la base de données MySQL.

```sql
-- Création de la structure de données
CREATE DATABASE formulaire_db;
USE formulaire_db;
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(50),
    email VARCHAR(100)
);
```

### 3. Résolution de Nom (DNS BIND9)
La mise en place d'un serveur DNS local a permis d'accéder à l'application via un nom de domaine explicite plutôt que par l'adresse IP, renforçant le professionnalisme de l'infrastructure.

---

## Bilan Technique
Ce projet a permis de valider la mise en œuvre méticuleuse de services essentiels interconnectés. Il démontre une capacité à monter une infrastructure complète de A à Z : de la couche réseau (DHCP/DNS) à la couche applicative (Apache/PHP/MySQL).

**Membres du projet :** Dylan Bassinga, Simon-Emmanuel Mbandzeng, Oumou Kaltom Sy.

---

## Document technique

[Cliquer ici pour télécharger le rapport complet du Projet Linux (PDF)](Projet_Linux_Dylan_Simon_Oumou.pdf.pdf)
