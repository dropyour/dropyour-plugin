---
name: dropyour-reparer
description: Diagnose and fix a Dropyour app that broke: read its log, list versions, roll back. Use when a published app returns an error, stopped working, or an update went wrong.
---

# Réparer une app Dropyour

Le chemin de retour existe et il est complet. **Ne republie pas à l'aveugle** : lis d'abord.

## 1. Lis, ne devine pas

- `dropyour_status` — l'état du drop, son palier, sa version courante.
- `dropyour_logs` — le journal de l'app : les erreurs du code serveur y tombent seules, avec l'heure.
  200 lignes gardées, du plus récent au plus ancien.

## 2. Reviens en arrière, c'est gratuit et immédiat

- `dropyour_list_versions` — jusqu'à 20 versions gardées.
- `dropyour_rollback` — remet la version choisie en ligne. **L'URL ne bouge pas, les données restent.**

Revenir en arrière n'est pas un aveu d'échec : c'est le chemin prévu. Fais-le AVANT de chercher le
bug, pour que l'utilisateur retrouve une app qui marche pendant que tu corriges.

## 3. Ensuite seulement, corrige et republie

`dropyour_replace` remplace le contenu. Ce n'est pas destructif : la version d'avant reste dans la
liste, donc tu peux tenter un correctif sans rien risquer.

## Si un appel réseau échoue depuis le code serveur

La sortie réseau est **fermée par défaut** et s'ouvre par déclaration, dérivée du code publié. Écris
l'URL littéralement dans ton code plutôt que de l'assembler à partir de morceaux — sinon la
déclaration ne peut pas la voir.
