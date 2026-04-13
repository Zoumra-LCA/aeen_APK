# AEEN — Note de version v1.0.1

**Date :** 13 avril 2026
**APK :** `AEEN_v1.0.1.apk`

## Nouveautés depuis la v1.0.0

### Rapports Essais en Charge — Multi-moteurs ✅
- Possibilité de saisir plusieurs groupes électrogènes dans un même rapport EC
- Tableau de sélection des moteurs sous l'onglet Technique (auto-rempli depuis la base contrat)
- Bouton "Nouveau moteur" pour ajouter un moteur absent de la base
- Combo de sélection moteur dans Observations et Données EC
- Propagation automatique des champs communs (Contrat, Client, Temps de travail, Signatures) sur tous les moteurs du lot
- Génération d'un PDF par moteur, envoi groupé par mail (ACTION_SEND_MULTIPLE)
- Garde-fou : sections de saisie désactivées tant qu'aucun moteur n'a été ajouté

### Signature et finalisation
- Pré-remplissage du nom signataire technicien depuis le champ "Technicien" du contrat
- Overlay "Traitement en cours..." pendant la génération PDF (plus de doute sur l'état)
- Boutons désactivés pendant le traitement pour éviter les double-clics

### Temps de travail
- "Mise en automatique de la centrale" passe par défaut à **Oui**
- Tous les champs heure (Arrivée, Départ, Travail matin/aprèm, Voyage matin/aprèm) utilisent un sélecteur d'heure Material3 au format `HH:mm`

### Synchronisation FTP automatique
- Envoi automatique des rapports finalisés vers le FTP dès que la connexion réseau est disponible
- Reprise automatique de l'envoi quand la connexion réseau revient (callback réseau enregistré au démarrage de l'app)
- Plus besoin de cliquer "Synchroniser" manuellement après une finalisation

## ⚠️ Correction en cours

### Génération PDF multi-pages
Le rendu PDF en mode paysage A4 fonctionne correctement pour la **page 1** (en-tête + checklist 2 colonnes), mais les pages 2 et 3 peuvent apparaître blanches lorsque le contenu déborde sur plusieurs pages. Une correction est en cours sur la pagination de la WebView Android (problème de re-paint de Chromium au-delà du viewport initial). Le contenu des pages suivantes est bien présent en base de données, mais n'est pas dessiné dans le PDF.

**Impact terrain :** rapports d'une seule page = OK. Rapports multi-pages = page 1 lisible, pages suivantes vides. Les données ne sont pas perdues, c'est purement un problème de rendu visuel.

**Workaround temporaire :** la version JSON exportée sur le FTP contient l'intégralité des données.

---

## Compatibilité

- **Tablette cible :** Samsung Galaxy Tab S9 FE 10.9" (2304×1440)
- **Android :** 13+
- **Orientation :** Paysage uniquement

## Installation

```bash
adb install -r AEEN_v1.0.1.apk
```

ou via le fichier APK directement sur la tablette.
