# AEEN — Note de version v1.0.8

**Date :** 14 avril 2026
**APK :** `AEEN_v1.0.8.apk`
**Objet :** Corrections suite au retour de débogage ind. 03

---

## Corrections apportées

### Écran d'accueil
- Image de fond remplacée par une version haute définition (2304×1440, ratio natif de la tablette)
- Affichage sans déformation ni étirement, couvre tout l'écran

### Maintenance Électrique — Batteries chargeurs démarrage
- Ajout de la ligne « Date / État des cosses - serrage n°2 » qui était manquante à l'écran
- Les deux batteries disposent désormais des 4 lignes de contrôle attendues

### Maintenance Électrique — Automatisme
- L'item « Noter type d'automatisme » dispose maintenant d'un champ de saisie texte libre dans la colonne Valeur

### Mise en auto et temps de travail
- Cases Durée / V / Hz / A agrandies et uniformisées (le libellé « Durée » ne se casse plus sur deux lignes)

### Rapport travaux
- L'onglet « Mise en auto et temps de travail » est renommé « Mise en auto » dans le menu de gauche pour ce type de rapport
- Les zones de saisie « Travail » et « Voyage » ont été retirées ; seule la question « Mise en automatique de la centrale » reste affichée

### Signature technicien — Compteur horaire
- Le bouton « Sauver » de la signature technicien est désormais grisé tant que le compteur horaire n'est pas renseigné
- Un message rouge « Compteur horaire obligatoire (onglet Contrat) » apparaît sous le bouton
- Le client ne peut plus finaliser un rapport sans avoir renseigné le compteur

### Messages d'erreur FTP
- Les erreurs de connexion FTP sont désormais traduites en français avec un message clair :
  - « Authentification FTP échouée — vérifier User et mot de passe »
  - « Serveur FTP introuvable — vérifier l'adresse »
  - « Délai dépassé — serveur injoignable, vérifier le Wi-Fi »
  - « Connexion refusée par le serveur (port 22 fermé ?) »
  - « Permission refusée sur le serveur »
  - « Fichier ou dossier introuvable sur le serveur »
- Remplace l'ancien message générique « Echec connexion FTP »

### Écran Paramètre
- Contenu rendu défilable pour éviter que certains éléments ne soient cachés en bas d'écran

---

## Compatibilité

- **Tablette cible :** Samsung Galaxy Tab S9 FE 10.9" (2304×1440)
- **Android :** 13+
- **Orientation :** Paysage uniquement

## Installation

```bash
adb install -r AEEN_v1.0.8.apk
```

ou en copiant le fichier APK sur la tablette et en l'ouvrant depuis l'explorateur de fichiers.

> **Important :** à la première ouverture après installation, si les paramètres FTP apparaissent vides, aller dans *Paramètre → Saisir un code → 1234 → Information FTP* et saisir à nouveau l'adresse, le user et le mot de passe, puis valider. Ensuite lancer une Synchronisation pour récupérer les clients et moteurs.
