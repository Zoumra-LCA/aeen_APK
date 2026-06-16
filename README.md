# AEEN — Note de version v1.0.9

**Date :** 15 avril 2026
**APK :** `AEEN_v1.0.9.apk`
**Objet :** Correctif synchronisation FTP en version release

---

## Correction apportée

### Synchronisation FTP / SFTP
- Correction de l'erreur `ClassNotFoundException: com.jcraft.jsch.jce.Random` qui empêchait toute connexion SFTP depuis l'APK installé sur la tablette
- La bibliothèque SFTP charge certaines classes (algorithmes de chiffrement, générateur aléatoire) par réflexion ; l'optimiseur d'APK les supprimait à tort lors de la génération finale
- Les règles d'optimisation ont été ajustées pour conserver l'intégralité des classes nécessaires

### Impact utilisateur
- Les boutons **Synchronisation** et **Test FTP** de l'écran Paramètre fonctionnent à nouveau
- L'import des clients/moteurs et l'export des rapports JSON vers le serveur SFTP sont de nouveau opérationnels

---

## Compatibilité

- **Tablette cible :** Samsung Galaxy Tab S9 FE 10.9" (2304×1440)
- **Android :** 13+
- **Orientation :** Paysage uniquement

## Installation

```bash
adb install -r AEEN_v1.0.9.apk
```

ou en copiant le fichier APK sur la tablette et en l'ouvrant depuis l'explorateur de fichiers pour installer par-dessus l'ancienne version. Les données et paramètres FTP déjà saisis sont conservés.
