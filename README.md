# AEEN — Application de maintenance électrique

Livraison de l'application AEEN (tablette) et des composants de la solution.
**Version courante : v1.2.0** — APK signé : [`AEEN_v1.2.0.apk`](AEEN_v1.2.0.apk).

> Livraison complète (APK + outils + notices d'exploitation) :
> **[Release v1.2.0](https://github.com/Zoumra-LCA/aeen_APK/releases/tag/v1.2.0)**

---

## Note de version v1.2.0 — Rapports en cours (multi-brouillons)

**Date :** 23 juin 2026 · versionCode 17

Il est désormais possible de conserver **plusieurs rapports en cours** dans la journée
et de les rouvrir plus tard pour les faire signer.

- Appui sur un type de rapport depuis l'accueil :
  - aucun brouillon de ce type → nouveau rapport créé directement ;
  - un ou plusieurs brouillons → fenêtre de **reprise** (date, client, site, n° GE) ou **Nouveau**.
- Nouveau bouton **« Rapports en cours »** (avec compteur) : liste de tous les brouillons,
  ouverture ou suppression.
- **Essai en charge** : deux visites sur deux sites distincts le même jour restent séparées.
- Mise à jour de la base **sans perte** : les rapports en cours sont conservés après installation.

---

## Composants de la solution

| Élément | Rôle |
|---------|------|
| `AEEN_v1.2.0.apk` | Application mobile (tablette) de saisie des rapports |
| `aeen_service/` | Outil de publication des données de référence (HFSQL → CSV → FTP) |
| `serveur_pdf/` | Service serveur de génération des PDF (rapports non modifiables) |

Les **notices d'exploitation** (PDF) de chaque composant sont jointes à la
[release v1.2.0](https://github.com/Zoumra-LCA/aeen_APK/releases/tag/v1.2.0).

---

## Installation de l'APK

```bash
adb install -r AEEN_v1.2.0.apk
```

ou en copiant le fichier APK sur la tablette et en l'ouvrant depuis l'explorateur de
fichiers pour installer par-dessus l'ancienne version. Les données et paramètres FTP
déjà saisis sont conservés.

**Tablette cible :** Samsung Galaxy Tab S9 FE 10,9" (2304×1440) · Android 13+ · paysage.

---

## Historique

| Version | Objet |
|---------|-------|
| **v1.2.0** | Rapports en cours (multi-brouillons) |
| v1.1.1 | Correctif libellé « Paramètres » |
| v1.1.0 | Génération des PDF côté serveur |
| v1.0.13 | Rotation du rendu PDF |
| v1.0.9 | Correctif synchronisation FTP en version release |
