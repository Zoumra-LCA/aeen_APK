# AEEN — Générateur PDF serveur · mise à jour pied de page

**Date :** 16/06/2026
**Composant :** `aeen-pdf.exe` (service de génération des PDF de rapport sur SRVAPPSAEEN)

## Objet

Mise à jour du **pied de page des rapports** suite au changement de **code APE**
(raison administrative), conformément au modèle `DEVIS GENERAL - OC - LOGO 2020 -
VERSION 2025.dotx` transmis par le client.

| | Avant | Après |
|---|---|---|
| Code APE | `4669 B` | **`43.21A`** |

Le reste du pied de page (raison sociale, adresse, RCS, SIRET, n° TVA, capital,
téléphones, site web) est **inchangé**.

## Vérifications effectuées

- Rendu HTML : pied de page affiche `APE 43.21A`.
- Tests de rendu : 13/13 OK.
- Test de bout en bout avec l'exe signé : PDF généré → `APE 43.21A`, plus aucune
  occurrence de `4669`.
- Exécutable **signé** (Laurent Castellan, horodatage Certum) — statut *Valid*.

## Déploiement

Procédure inchangée (voir `DEPLOIEMENT_EXE.md`) : remplacer
`C:\aeen\aeen-pdf.exe` par cette nouvelle version. Aucune reconfiguration FTP
nécessaire (le `config.ini` en place est conservé). La tâche planifiée reprend
automatiquement à la passe suivante.
