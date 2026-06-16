# AEEN — Service de génération des fichiers CSV (clients / moteurs)

Ce programme tourne sur le serveur. Il lit la base **HFSQL** (fichiers `.FIC`) et
génère les fichiers **`clients.csv`** et **`moteurs.csv`** déposés sur le **FTP**,
qui servent ensuite à l'import sur les tablettes.

`AEEN_Service.exe` est livré avec les bibliothèques WINDEV (`wd290*.dll`)
nécessaires à son exécution.

---

## 1. Installer

1. Décompresser **`AEEN_Service.zip`** dans un dossier sur le serveur (ex. `C:\aeen_service`).
2. Le dossier contient :
   - `AEEN_Service.exe` + les DLL `wd290*.dll` (moteur WINDEV) ;
   - `ref.ini` — fichier de configuration ;
   - `initial/` — modèles `clients.csv` / `moteurs.csv` vides.

---

## 2. Configurer — `ref.ini`

Ouvrir **`ref.ini`** et renseigner la section `[repData]`. La clé `rep` doit
contenir le **répertoire des fichiers `.FIC`** de la base HFSQL (les données
clients et moteurs à exporter) :

```ini
[repData]
rep = C:\chemin\vers\les\fichiers\FIC
```

> ⚠️ Indiquer le **dossier** qui contient les `.FIC`, pas un fichier en particulier.

---

## 3. Lancer

Exécuter `AEEN_Service.exe`. Le programme lit les `.FIC` du répertoire configuré
et (re)génère `clients.csv` et `moteurs.csv` sur le FTP.

Pour une exécution automatique régulière, planifier l'exe via le **Planificateur
de tâches Windows**.
