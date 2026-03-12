🐳 Unraid Docker Startup Orchestrator

<p align="center">
<img src="assets/interface.png" alt="Unraid Docker Startup Orchestrator Banner" width="800">
</p>

<p align="center">
<a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge" alt="License: MIT"></a>
<a href="https://unraid.net"><img src="https://img.shields.io/badge/Platform-Unraid-f4731c.svg?style=for-the-badge&logo=unraid&logoColor=white" alt="Unraid"></a>
<a href="https://www.docker.com/"><img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker"></a>
<a href="https://ko-fi.com/cbh17000"><img src="https://img.shields.io/badge/Support-Ko--fi-F16061?style=for-the-badge&logo=ko-fi&logoColor=white" alt="Support Ko-fi"></a>
</p>
🚀 Redonnez le contrôle à votre démarrage Docker

Unraid Docker Startup Orchestrator est une solution web élégante pour remplacer le démarrage désordonné d'Unraid par une séquence intelligente, journalisée et hautement configurable.

    Le problème : L'autostart natif d'Unraid lance tout en même temps. Résultat ? Vos apps de téléchargement démarrent sans VPN, et vos sites web plantent car la base de données n'est pas encore prête.

    La solution : Une orchestration basée sur des vérifications d'état réelles (running) et une hiérarchie logique.

✨ Points Forts
Fonctionnalité	Description
🔍 wait_for Intelligent	Vérifie via l'API Docker si le conteneur est réellement opérationnel avant de continuer.
🛡️ Idempotence	Détection automatique des conteneurs déjà actifs pour éviter les erreurs de doublons.
📋 Logs de Production	Suivi en temps réel et historique dans /tmp/docker_start_order.log.
🌐 Intégration AppFeed	Récupère les icônes et infos directement depuis Community Applications.
🔒 100% Privé	Traitement local dans votre navigateur. Aucune donnée ne quitte votre réseau.
🏗️ Logique de Démarrage

Voici comment le script organise la survie de vos services après un redémarrage :
Extrait de code

graph TD
    A[Démarrage Array Unraid] --> B{Groupe 1: Réseau}
    B -->|OK| C[VPN / DNS / AdGuard]
    C --> D{Groupe 2: Data}
    D -->|Wait for Running| E[MariaDB / Postgres / Redis]
    E --> F{Groupe 3: Proxy}
    F -->|OK| G[Nginx Proxy Manager]
    G --> H[Groupe 4: Applications Web]
    H --> I[Groupe 5: Médias & Téléchargement]
    I --> J[✅ Système Opérationnel]

🛠️ Installation Rapide
1. Générer le script

    Rendez-vous sur L'interface Web.

    Importez vos conteneurs, organisez-les par glisser-déposer.

    Cliquez sur Générer le script et copiez le code.

2. Configuration dans Unraid

    Installez le plugin User Scripts via l'onglet Apps.

    Créez un nouveau script nommé Docker_Orchestrator.

    Collez le code et réglez le déclencheur sur "At Startup of Array".

    ⚠️ Important : Désactivez l'auto-start natif dans l'onglet Docker d'Unraid pour les conteneurs gérés par ce script.

📊 Monitoring & Debug

Vous pouvez surveiller le bon déroulement du script directement depuis votre terminal Unraid :
Bash

# Pour voir le démarrage en temps réel
tail -f /tmp/docker_start_order.log

💾 Structure de Sauvegarde (JSON)

L'outil vous permet d'exporter votre configuration. Voici à quoi ressemble un bloc de configuration type :
JSON

{
  "name": "Bases de données",
  "pause": 10,
  "containers": [
    { "id": "mariadb", "waitFor": true, "timeout": 45 }
  ]
}

🤝 Contribution & Support

Les idées sont les bienvenues ! N'hésitez pas à ouvrir une Issue ou une Pull Request.

    🛠️ Développement : HTML5, CSS3 (variables modernes), JS Vanilla.

    ☕ Soutien : Si cet outil vous simplifie la vie, vous pouvez m'offrir un café sur Ko-fi.

<p align="center">
<i>Développé avec ❤️ pour la communauté Unraid.</i>
</p># 🐳 Unraid Docker Startup Orchestrator

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Unraid](https://img.shields.io/badge/Platform-Unraid-f4731c.svg)](https://unraid.net)

![Aperçu de l'interface](assets/interface.png)

**Unraid Docker Startup Orchestrator** est un outil web ultra-léger et intelligent conçu pour remplacer le démarrage basique des conteneurs Docker dans Unraid par une séquence de démarrage robuste, journalisée et ordonnée.

Fini les délais (`sleep`) arbitraires. Assurez-vous que votre base de données ou votre VPN est **réellement opérationnel** avant de lancer vos applications dépendantes.


## 📋 Prérequis

- Unraid 6.x ou supérieur.
- Plugin **User Scripts** (indispensable).
- Les conteneurs doivent être nommés correctement (le script utilise les noms Docker standard).

---

## ✨ Points Forts

- **🚀 Orchestration Intelligente** : Utilisez la fonction `wait_for` pour vérifier le statut réel d'un conteneur avant de poursuivre la séquence.
- **🛡️ Idempotence** : Le script vérifie si un conteneur tourne déjà pour éviter des redémarrages inutiles.
- **📊 Logs de Production** : Génère un journal détaillé dans `/tmp/docker_start_order.log` pour débugger facilement vos démarrages.
- **🔍 Auto-détection (AppFeed)** : Intégration directe avec l'API Community Applications pour récupérer automatiquement les icônes et les types d'applications.
- **📂 Gestion de Configuration** : Exportez et importez votre structure au format JSON pour des modifications ultérieures rapides.
- **🔒 Confidentialité Totale** : Fonctionne à 100% côté client (Client-side). Aucune donnée de votre serveur ne quitte votre navigateur.

---

## 🛠️ Installation et Utilisation

### 1. Générer votre script
1. Accédez à l'interface via [GitHub Pages](https://cbh17000.github.io/unraid-docker-startup-orchestrator/). Ou télécharger le fichier index.html.
2. Organisez vos conteneurs par groupes (Réseau, BDD, Apps, etc.).
3. Configurez les options `Wait for` et les délais de pause.
4. Cliquez sur **Générer le script**.

### 2. Mise en place dans Unraid
1. Assurez-vous que le plugin **User Scripts** est installé sur votre serveur Unraid.
2. Créez un nouveau script nommé `Docker_Startup_Order`.
3. Collez le code généré dans l'éditeur.
4. Réglez la fréquence de déclenchement sur **"At Startup of Array"**.
5. Désactivez l'auto-start natif dans l'onglet "Docker" d'Unraid pour les conteneurs gérés par le script afin d'éviter les conflits.

---

## ⚙️ Structure de la Configuration (JSON)

L'outil permet de sauvegarder votre travail. Le fichier `config.json` suit une structure versionnée :
- `groups`: Définit l'ordre des sections.
- `pause`: Temps d'attente après chaque groupe.
- `waitFor`: Si activé, le script attend que le conteneur soit en état `running`.
- `timeout`: Temps maximum d'attente pour la fonction `wait_for`.

---


## 🤝 Contribution

Les contributions sont les bienvenues ! Si vous avez des suggestions pour améliorer la logique de détection des dépendances ou l'interface :
1. Forkez le projet.
2. Créez votre branche de fonctionnalité (`git checkout -b feature/AmazingFeature`).
3. Commitez vos changements (`git commit -m 'Add some AmazingFeature'`).
4. Pushez la branche (`git push origin feature/AmazingFeature`).
5. Ouvrez une Pull Request.

---

## 📄 Licence

Ce projet est distribué sous licence **MIT**. Voir le fichier `LICENSE` pour plus de détails.

---

## 🙏 Remerciements

- La communauté **Unraid** pour son inspiration constante.
- **Squid** pour l'accès à l'AppFeed de Community Applications.
- Tous les utilisateurs qui testent et améliorent la stabilité du déploiement Docker.

---
*Développé avec ❤️ pour simplifier la vie des administrateurs Unraid.*# unraid-docker-startup-orchestrator
Unraid Docker Startup Orchestrator

---
☕ **Si cet outil vous fait gagner du temps, n'hésitez pas à me [payer un café sur Ko-fi](https://ko-fi.com/cbh17000) !**
