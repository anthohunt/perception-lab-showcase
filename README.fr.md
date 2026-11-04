[English](README.md) · **Français**

> Dépôt vitrine : le code et les données de ce projet sont privés ; ce README le décrit.

# Perception Lab

Un banc d'essai qui enregistre ce qu'un casque Meta Quest voit, entend et mesure, et le transmet à un agent doté d'une mémoire temporelle.

## Le problème

Les travaux sur la mémoire des agents en réalité virtuelle partent souvent de données écrites à la main, faute de captation réelle. Ce banc fournit des données réelles, issues du casque, à des équipes de recherche d'une école d'ingénieurs. Le but est de savoir ce qu'un casque livre vraiment, flux par flux. C'est un outil de connaissance, pas un produit.

## Comment ça marche

- Le casque sert de capteur : un module Unity, intégrable dans une application VR, envoie la vidéo de la caméra passthrough, l'audio du micro, la tête, les mains, le corps, le regard et le visage.
- Le serveur reçoit les données en blocs par HTTPS et les relaie en direct par WebSocket.
- Un tableau de bord web démarre et arrête les enregistrements, règle la fréquence et rejoue les sessions.
- Le direct reste à la fréquence du casque ; à l'enregistrement, le serveur ne garde que la fréquence choisie (1 à 30 par seconde).
- Côté mémoire, une image prise toutes les 2 secondes est décrite par un modèle de vision, puis versée dans un graphe de connaissances horodaté.

## Ce qui est construit

En cours, phase d'exploration.

- Service de capture en service ; application diffusée sur neuf casques de test, installation confirmée sur trois.
- Direct mesuré à 72 mesures par seconde, retard vidéo affiché d'environ 1,9 s.
- Premier enregistrement sur Quest 3 : 30 s, 592 blocs, aucune perte.
- Stockage compressé sans perte : 4,6 Go ramenés à 0,73 Go ; espace disque plafonné à 25 Go.
- Service de mémoire déployé, 7 tests sur 7 au vert.
- Reste à faire : câbler la capture continue entre l'application VR et le service de mémoire, et tester sur casque l'intégration du module dans une application de formation.

## Ce qui est public

Cette vitrine est publique ; le code, le serveur et les données enregistrées restent privés.

## Pile technique

- Unity 6, Meta XR Core SDK, OpenXR
- Module Android en Java (Camera2, MediaProjection), vidéo H.264
- Serveur Node.js, WebSocket, ffmpeg, compression gzip et brotli
- Service de mémoire en Python : FastAPI, Graphiti, FalkorDB
- Groq (modèle de vision qwen3.6-27b)
- Embeddings locaux sentence-transformers (all-MiniLM-L6-v2)
- Docker ; diffusion sur les casques par Meta Horizon Managed Services
