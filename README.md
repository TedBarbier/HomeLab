# 🏠 HomeLab - Infrastructure Réseau & Domotique

Ce projet est à but **éducatif** et personnel. Il a pour objectif de construire une infrastructure domestique **stable et performante** en tirant parti du matériel existant : un **Raspberry Pi 4** et un **NAS Synology**.

L'évolution du projet a mené à privilégier la **stabilité du réseau domotique** et la **gestion optimisée des ressources** plutôt que la multiplication de services de sécurité lourds.

---

## 🔧 Infrastructure actuelle

| Composant | Rôle principal | Services / Matériel |
| :--- | :--- | :--- |
| **Raspberry Pi 4 (Pimox)** | Cœur Domotique | Home Assistant, Zigbee (Dongle Haute Performance) |
| **NAS Synology** | Infrastructure & Réseau | WireGuard, AdGuard Home, DDNS |
| **Dongle Zigbee** | Communication IoT | Modèle haute capacité (échanges intensifs) |

---

## 📌 Optimisations et Arbitrages

### 🚀 Performance Domotique & Zigbee
L'utilisation d'un **nouveau dongle Zigbee performant** a considérablement augmenté le volume d'échanges de données. Pour garantir la stabilité de **Home Assistant** sous Pimox face à cette hausse d'activité, une configuration spécifique a été nécessaire :

* **Gestion de la RAM :** En raison de la saturation de la mémoire vive, un **Swap de 2 Go** a été configuré sur l'instance Pimox.
* **Stabilité :** Cette modification a permis d'éliminer les crashs système liés à l'utilisation intensive de la mémoire par le contrôleur Zigbee et les services associés.

### ⚖️ Choix de Sobriété (Sécurité vs Ressources)
Afin de ne pas surcharger le processeur du Raspberry Pi et de préserver les ressources du NAS, certains services initialement prévus ont été écartés :

* **OPNsense / pfSense :** Projet abandonné par manque de machine dédiée (nécessite plusieurs ports réseau physiques pour être pertinent).
* **Fail2Ban / Suricata :** Non déployés pour éviter une consommation CPU/RAM excessive qui nuirait à la réactivité de la domotique.
* **Optimisation NAS :** Les services sur le NAS sont limités au strict nécessaire pour ne pas impacter ses fonctions de stockage.

---

## 🌐 Accès & Filtrage

* **VPN :** [WireGuard](https://www.wireguard.com/) (Hébergé sur le NAS) pour un accès distant sécurisé, rapide et léger.
* **DNS :** [AdGuard Home](https://adguard.com/fr/adguard-home/overview.html) (Hébergé sur le NAS) pour le filtrage des publicités et la protection contre le phishing.
* **DDNS :** Configuration native Synology pour l'accès externe via un nom de domaine personnalisé.

---

## 🧰 Services déployés

| Service | Rôle | Statut | Hébergé sur |
| :--- | :--- | :--- | :--- |
| **WireGuard** | VPN Accès Distant | ✅ Opérationnel | NAS |
| **AdGuard Home** | DNS filtrant | ✅ Opérationnel | NAS |
| **Pimox** | Virtualisation (Proxmox pour RPi) | ✅ Opérationnel | RPi 4 |
| **Home Assistant** | Pilotage Domotique | ✅ Stable (avec Swap) | RPi 4 |
| **Zigbee** | Gestion du réseau Mesh IoT | ✅ Haute Performance | RPi 4 |

---

## 📊 Architecture réseau

![Légende de mon image](archi_homelab.svg)

## 🗓️ Roadmap & Suivi

* [x] Déploiement du VPN WireGuard
* [x] Mise en place de AdGuard Home sur le NAS
* [x] Installation de Pimox et Home Assistant
* [x] Migration vers le nouveau Dongle Zigbee (Haute Performance)
* [x] Optimisation de la RAM (Configuration Swap 2Go sur Pimox)
* [ ] Mise en place d'un monitoring léger des ressources (CPU/RAM/Temp)
* [ ] Documentation des automatisations Zigbee complexes

---

## 🛠️ Stack Technique

* **OS :** Raspberry Pi OS Lite 64-bit / Synology DSM.
* **Virtualisation :** Pimox (Proxmox on RPi).
* **Domotique :** Home Assistant.
* **Réseau :** WireGuard, AdGuard Home.

---

## ✍️ Auteur

**@TedBarbier**
Étudiant en cybersécurité, focalisé sur l'optimisation des ressources et la domotique fiable.
