# AEEN — Génération des PDF côté serveur (exécutable autonome)

Ce programme tourne sur le serveur **SRVAPPSAEEN**. Toutes les 5 minutes, il lit
les fichiers `*.json` déposés par les tablettes sur le FTP, génère le PDF de
chaque rapport (mise en page identique à l'ancien rendu tablette, **PDF non
modifiable**), redépose le PDF sur le FTP et archive le JSON traité.

**`aeen-pdf.exe` est autonome** : il embarque tout le nécessaire. **Aucune
installation de Python ni de bibliothèque n'est requise.** Il réutilise le canal
**SFTP déjà en place** (mêmes identifiants que les tablettes) — aucune nouvelle
ouverture réseau.

---

## 1. Installer

1. Créer le dossier **`C:\aeen`** sur le serveur.
2. Y copier **`aeen-pdf.exe`** et **`config.example.ini`**.

C'est tout. (L'exécutable est signé numériquement — éditeur : *Laurent
Castellan*.)

---

## 2. Configurer l'accès FTP

Ouvrir une invite de commandes dans `C:\aeen` et lancer :

```bat
aeen-pdf.exe init
```

Le programme pose quelques questions et **écrit `config.ini`** à côté de l'exe :

```
Hôte SFTP [SRVAPPSAEEN] :
Port [22] :
Utilisateur : <identifiant FTP des tablettes>
Mot de passe (laisser vide = inchangé) : <mot de passe FTP>
Dossier d'entrée [/aeen/a_traiter] :
Dossier de sortie [/aeen/transfere] :
Mode local (true/false) [false] :
```

À la fin, il **teste la connexion** et affiche `Connexion OK : …` ou un message
d'erreur. **Relancer `aeen-pdf.exe init` chaque fois que le mot de passe ou
l'emplacement FTP change** — c'est la seule manipulation dans ce cas.

---

## 3. Tester une passe manuellement

```bat
aeen-pdf.exe config.ini
```

Le programme se connecte au FTP, traite les JSON présents, et écrit un
compte-rendu dans **`pdfgen.log`** (à côté de l'exe). Vérifier la ligne
`Passe terminée : N PDF généré(s)`.

Test de bout en bout : déposer un `*.json` de test dans
`/aeen/a_traiter/<nom_tablette>/` sur le FTP, lancer la commande, puis vérifier
qu'un PDF est apparu dans `/aeen/transfere/<nom_tablette>/` et que le JSON a été
déplacé dans `/aeen/a_traiter/<nom_tablette>/traite/`.

---

## 4. Planifier l'exécution automatique

Importer la tâche fournie (invite de commandes **Administrateur**, dans `C:\aeen`) :

```bat
schtasks /create /xml aeen-pdf-task.xml /tn "AEEN PDF"
```

La tâche lance `C:\aeen\aeen-pdf.exe config.ini` **toutes les 5 minutes**.

- Changer la fréquence : modifier `<Interval>PT5M</Interval>` dans
  `aeen-pdf-task.xml` (`PT10M` = 10 min) avant l'import, ou via le Planificateur
  de tâches → *Déclencheurs*.
- Le compte qui exécute la tâche doit avoir accès au réseau FTP (les mêmes
  droits que les tablettes — déjà en place).

---

## 5. Arborescence FTP

```
/aeen/
├── a_traiter/
│   └── <nom_tablette>/
│       ├── 2026_05_07_ABCD.json   ← déposé par la tablette (entrée)
│       ├── traite/                ← JSON traités avec succès (archive auto)
│       └── erreur/                ← JSON en échec (à examiner)
└── transfere/
    └── <nom_tablette>/
        └── 2026_05_07_ABCD.pdf    ← PDF généré (sortie)
```

- 1 JSON = 1 PDF (même nom).
- Les fichiers `*.json.tmp` sont ignorés (écriture en cours).
- Les sous-dossiers `traite/` et `erreur/` sont créés automatiquement.

---

## 6. PDF non modifiable

Chaque PDF est chiffré (AES-256) avec un mot de passe propriétaire aléatoire,
**sans mot de passe utilisateur** : le destinataire l'ouvre normalement, peut le
lire et l'imprimer, mais **ne peut pas le modifier, l'annoter ni le remplir**.

---

## 7. Dépannage

| Symptôme | Solution |
|----------|----------|
| `Connexion KO` à l'init | Mauvais hôte/identifiants, ou réseau/VPN FTP indisponible. |
| JSON déplacé dans `erreur/` | JSON invalide ; consulter `pdfgen.log` (trace complète). |
| Aucun PDF généré | Vérifier `pdfgen.log` et que des `*.json` (pas `.json.tmp`) sont présents dans `a_traiter/<tablette>/`. |
| L'antivirus bloque l'exe | L'exe est signé (Laurent Castellan) ; autoriser l'éditeur si nécessaire. |

Journal : **`pdfgen.log`** dans `C:\aeen` (une ligne par fichier traité, trace
complète des erreurs).
