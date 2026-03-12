# 🐳 Unraid Docker Startup Orchestrator

<p align="center">
<img src="assets/interface.png" alt="Unraid Docker Startup Orchestrator Banner" width="800">
</p>

<p align="center">
<a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge" alt="License: MIT"></a>
<a href="https://unraid.net"><img src="https://img.shields.io/badge/Platform-Unraid-f4731c.svg?style=for-the-badge&logo=unraid&logoColor=white" alt="Unraid"></a>
<a href="https://www.docker.com/"><img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker"></a>
<a href="https://ko-fi.com/cbh17000"><img src="https://img.shields.io/badge/Support-Ko--fi-F16061?style=for-the-badge&logo=ko-fi&logoColor=white" alt="Support Ko-fi"></a>
</p>

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

##🚀 Redonnez le contrôle à votre démarrage Docker

Unraid Docker Startup Orchestrator est une solution web élégante pour remplacer le démarrage désordonné d'Unraid par une séquence intelligente, journalisée et hautement configurable.

Le problème : L'autostart natif d'Unraid lance tout en même temps. Résultat ? Vos apps de téléchargement démarrent sans VPN, et vos sites web plantent car la base de données n'est pas encore prête.

La solution : Une orchestration basée sur des vérifications d'état réelles (running) et une hiérarchie logique.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## ✨ Points Forts

Fonctionnalité et Description

🔍 wait_for --> Intelligent,Vérifie via l'API Docker si le conteneur est réellement opérationnel avant de continuer.

🛡️ Idempotence --> Détection automatique des conteneurs déjà actifs pour éviter les erreurs de doublons.

📋 Logs de Production --> Suivi en temps réel et historique dans /tmp/docker_start_order.log.

🌐 Intégration AppFeed --> Récupère les icônes et infos directement depuis Community Applications.

🔒 100% Privé --> Traitement local dans votre navigateur. Aucune donnée ne quitte votre réseau.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 🏗️ Logique de Démarrage

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

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 🛠️ Installation Rapide
1. Générer le script

    Rendez-vous sur L'interface Web.

    Importez vos conteneurs, organisez-les par glisser-déposer.

    Cliquez sur Générer le script et copiez le code.

   -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    # <p align="center">⚠️ Important : Désactivez l'auto-start natif dans l'onglet Docker d'Unraid pour les conteneurs gérés par ce script.</p>

   -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 📊 Monitoring & Debug

Vous pouvez surveiller le bon déroulement du script directement depuis votre terminal Unraid :
Bash

    # Pour voir le démarrage en temps réel
    tail -f /tmp/docker_start_order.log

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 💾 Structure de Sauvegarde (JSON)

L'outil vous permet d'exporter votre configuration. Voici à quoi ressemble un bloc de configuration type :
JSON

    {
      "name": "Bases de données",
      "pause": 10,
      "containers": [
        { "id": "mariadb", "waitFor": true, "timeout": 45 }
      ]
    }

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 🤝 Contribution & Support

Les idées sont les bienvenues ! N'hésitez pas à ouvrir une Issue ou une Pull Request.

    🛠️ Développement : HTML5, CSS3 (variables modernes), JS Vanilla.

☕ Soutien : Si cet outil vous simplifie la vie, vous pouvez [payer un café sur Ko-fi](https://ko-fi.com/cbh17000) !.

<p align="center">
<i>Développé avec ❤️ pour la communauté Unraid.</i>
