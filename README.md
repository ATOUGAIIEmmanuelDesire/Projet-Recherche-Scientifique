# GeeMotion : Intelligent Gesture-Control HMI for Industrial Cobotics


## 📌 Présentation du Projet
**GeeMotion** est une Interface Homme-Machine (IHM) intelligente et sans contact conçue pour superviser et piloter des robots collaboratifs (cobots) industriels. Développé dans le cadre de notre projet de recherche scientifique à l'**UCAC-icam**, ce système utilise la vision artificielle monoculaire couplée au Deep Learning pour traduire les gestes de l'opérateur en commandes cinématiques, tout en assurant un retour d'information visuel en temps réel et un monitoring de performance (TRS, Éco-performance).

L'architecture logicielle est entièrement découplée pour garantir une latence de traitement ultra-faible ($<120\text{ ms}$), assurant une conformité stricte avec les normes de sécurité industrielles **ISO 10218** et **ISO/TS 15066**.

---

## 🚀 Fonctionnalités Clés (Basé sur notre Maquette IHM)

* **🔐 Authentification Sécurisée :** Pages d'enregistrement et de connexion des opérateurs adaptées aux profils d'usine.
* **📊 Dashboard de Supervision Centralisé :** Vue globale avec intégration multi-caméras (3 flux de surveillance de cellule en temps réel).
* **📈 Analyse Cinématique & Jumeau Numérique :** Graphiques dynamiques haute fréquence (Position, Vitesse, Accélération) et synchronisation avec les modèles 3D des robots.
* **🌱 Écran EcoMotion :** Monitoring de l'empreinte carbone (Objectif de score vert à 70%) et de l'efficience énergétique des actionneurs.
* **🏆 Métriques de Performance Industrielle :** Calcul automatique du Taux de Rendement Synthétique (TRS/OEE à 95%), statistiques de rebuts (1%) et diagrammes de Pareto.
* **🎮 Contrôle à Distance :** Console de secours avec Pads directionnels de jogging, curseurs de sensibilité et commutateurs de périphériques.

---

## 🛠️ Architecture Technique

L'application est divisée en deux sous-systèmes principaux :

### 1. Backend : Moteur IA & Robotique (`geemotion-backend`)
* **Langage :** Python 3.10
* **Framework Vision & IA :** MediaPipe Hands (Blaze Palm 21 points), Auto-encodeur Variationnel (VAE) pour la gestion des occlusions, classifieurs MLP & CNN-LSTM quantifiés en **INT8 via NVIDIA TensorRT**.
* **Middleware :** **ROS 2 (Humble Hawksbill)** pour le contrôle robotique décentralisé et l'application des filtres de Kalman.

### 2. Frontend : Interface Graphique Desktop (`geemotion-frontend`)
* **Framework :** React.js + Electron (compilation en application de bureau native).
* **Styles :** Tailwind CSS (Thème sombre industriel).
* **Graphiques :** ApexCharts / Chart.js pour le rendu fluide des métriques de production et de cinématique.

### 📡 Matrice des Protocoles Réseau
* **WebSockets ($60\text{ Hz}$) :** Flux continu des coordonnées articulaires de la main vers l'IHM.
* **ROS 2 Topics / DDS ($<10\text{ ms}$) :** Alertes de sécurité critiques et commandes machines directes.
* **MQTT ($1\text{ Hz}$) :** Télétransmission des indicateurs lents (OEE, logs, consommation EcoMotion).

---

## 📂 Structure des Dossiers

```text
geemotion-project/
├── geemotion-backend/     # Code source Python : IA, Vision, VAE, serveurs réseau et nœuds ROS 2
└── geemotion-frontend/    # Code source React + Electron : Écrans IHM, charts et services de communication
