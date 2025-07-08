# 🏠 HomeLab - Projet Personnel de Sécurisation Réseau

Ce projet est à but **éducatif** et personnel. Il a pour objectif de construire un **HomeLab sécurisé** en tirant parti du matériel que j’ai déjà à la maison : un **Raspberry Pi 4** et un **NAS Synology**.

L’idée principale est de dépasser la simple utilisation d’une box Internet, en déployant une **infrastructure réseau locale fiable, sécurisée et documentée**.

---

## 🔧 Infrastructure actuelle

| Composant     | Rôle principal                                      | Services hébergés                          |
|---------------|-----------------------------------------------------|--------------------------------------------|
| Raspberry Pi 4 (Pimox) | Sécurité réseau et domotique                        | Home Assistant, Fail2Ban, Suricata*        |
| NAS Synology  | Infrastructure réseau + services réseau             | WireGuard, Pi-hole, DDNS (OPENSENSE)       |

> \* *Suricata sera hébergé sur le RPi sauf si je peux le faire tourner comme plugin via OPNsense/PFsense sur le NAS.*

---

## 📌 Objectifs

### 1. 🧠 Expérimentation & Apprentissage
- Apprendre à configurer des services de sécurité réseau dans un environnement contraint.
- Gérer plusieurs machines interconnectées, avec des responsabilités réparties.

### 2. 🔐 Sécurité
- Mise en place d’un VPN pour un accès distant sécurisé.
- Pare-feu avec filtrage intelligent.
- Protection contre les publicités, malwares, phishing et connexions abusives.

### 3. 🧱 Modularité
- Utilisation de conteneurs Docker sur le NAS (via Container Manager Synology).
- Structure pensée pour être évolutive selon les ressources matérielles.

---

## 🌐 Accès à distance

- **VPN choisi :** [WireGuard](https://www.wireguard.com/)
  - Choisi pour sa légèreté et sa simplicité de configuration.
  - Déjà utilisé avec succès lors d’un ancien projet de domotisation familiale.
- **DDNS :** Configuration native Synology en place pour permettre un accès simple via un domaine personnalisé.

---

## 🧰 Services déployés

| Service         | Rôle | Statut | Hébergé sur |
|----------------|------|--------|-------------|
| WireGuard       | VPN | ✅ Fonctionnel | NAS         |
| Pi-hole         | DNS filtrant, anti-pub | ✅ Fonctionnel | NAS         |
| Pimox           | Virtualiser différents système en parallèles sur le raspberry | ✅ Fonctionnel  | RPi    |
| Home Assistant  | Domotique | ⏳ En cours | RPi         |
| Fail2Ban        | Blocage IP brute-force | ❌ pas commencé (nécessite pimox) | RPi         |
| Suricata        | IDS/IPS réseau | ❓ En évaluation | RPi ou NAS   |
| OPNsense / pfSense | Pare-feu complet | ❓ En évaluation (Docker) | NAS         |

---

## 📊 Architecture réseau (vue simplifiée)

```
                    ┌───────────────────────┐
                    │       Internet        │
                    └──────────┬────────────┘
                               │
                        [ Box FAI / Routeur ]
                               │
         ┌─────────────────────┴─────────────────────┐
         │                                           │
 ┌───────▼────────┐                          ┌───────▼─────────┐
 │      NAS       │                          │  Raspberry Pi   │
 │   (Synology)   │                          │  4 (Pimox)      │
 │                │                          │                 │
 │ - WireGuard    │                          │ - Home Assistant│
 │ - Pi-hole      │                          │ - Fail2Ban      │
 │ - DDNS         │                          │ - Suricata (*)  │
 │ - (OPNsense ?) │                          │                 │
 └────────────────┘                          └─────────────────┘
```


> *Remarque : si Suricata est plus pertinent en plugin via OPNsense, il migrera sur le NAS.*

---

## 📅 Roadmap

- [x] Déploiement du VPN WireGuard
- [x] Mise en place de Pi-hole sur le NAS
- [ ] Installation de pimox
- [ ] Réinstallation de Home Assistant
- [ ] Configuration de Fail2Ban sur le RPi
- [ ] Test Suricata en local et en plugin via OPNsense
- [ ] Évaluation et déploiement d’OPNsense sur le NAS (Docker)
- [ ] Documentation complète de chaque service

---

## 🤔 Pourquoi ne pas utiliser Wazuh ?

Wazuh a été envisagé comme solution de sécurité plus complète. Cependant :
- Il est trop lourd pour les capacités du Raspberry Pi 4.
- Les agents ne sont pas pertinents pour des appareils comme des téléphones ou télé connectées.
- Les ressources disponibles sont mieux allouées à des services légers et ciblés.

---

## 🧠 Réflexion future

- Comparaison Pi-hole vs [AdGuard Home](https://adguard.com/fr/adguard-home/overview.html)
- Intégration d’un reverse proxy (NGINX ou Traefik) ?
- Monitoring réseau plus avancé (Grafana, Netdata ?)

---

## 🎯 Conclusion

Ce projet me permet de :
- Progresser dans la compréhension des réseaux et de la cybersécurité,
- Tester des solutions concrètes de sécurisation domestique,
- Mieux exploiter mon matériel existant.

---

## 🛠️ Made with
- Raspberry Pi OS Lite 64-bit (Bookworm)
- Synology DSM + Container Manager
- WireGuard, Pi-hole, Fail2Ban, Suricata
- (Possiblement) OPNsense, Home Assistant

---

## ✍️ Auteur

**@TedBarbier**  
Étudiant en cybersécurité passionné de réseau et d'infrastructure.
