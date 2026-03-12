# 🐳 Unraid Docker Startup Orchestrator

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Unraid](https://img.shields.io/badge/Platform-Unraid-f4731c.svg)](https://unraid.net)

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
