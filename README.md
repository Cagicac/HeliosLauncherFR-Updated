<p align="center"><img src="./app/assets/images/SealCircle.png" width="150px" height="150px" alt="aventium softworks"></p>

<h1 align="center">Helios Launcher</h1>

<em><h5 align="center">(anciennement Electron Launcher)</h5></em>

[<p align="center"><img src="https://img.shields.io/github/actions/workflow/status/dscalzi/HeliosLauncher/build.yml?branch=master&style=for-the-badge" alt="gh actions">](https://github.com/dscalzi/HeliosLauncher/actions) [<img src="https://img.shields.io/github/downloads/dscalzi/HeliosLauncher/total.svg?style=for-the-badge" alt="downloads">](https://github.com/dscalzi/HeliosLauncher/releases) <img src="https://forthebadge.com/images/badges/winter-is-coming.svg"  height="28px" alt="winter-is-coming"></p>

<p align="center">Rejoins des serveurs moddés sans te soucier d’installer Java, Forge ou d’autres mods. On s’en occupe pour toi.</p>

![Capture d’écran 1](https://i.imgur.com/6o7SmH6.png)
![Capture d’écran 2](https://i.imgur.com/x3B34n1.png)

## Fonctionnalités

* 🔒 Gestion complète des comptes.
  * Ajoute plusieurs comptes et bascule facilement entre eux.
  * Authentification Microsoft (OAuth 2.0) + Mojang (Yggdrasil) entièrement prise en charge.
  * Les identifiants ne sont jamais stockés et sont transmis directement à Mojang.
* 📂 Gestion efficace des ressources.
  * Reçois les mises à jour du client dès leur publication.
  * Les fichiers sont vérifiés avant le lancement. Les fichiers corrompus ou incorrects seront retéléchargés.
* ☕ **Validation automatique de Java.**
  * Si tu as une version incompatible de Java installée, nous installerons la bonne *pour toi*.
  * Tu n’as pas besoin d’avoir Java installé pour lancer le launcher.
* 📰 Fil d’actualités intégré nativement au launcher.
* ⚙️ Gestion intuitive des paramètres, incluant un panneau de contrôle Java.
* Prend en charge tous nos serveurs.
  * Passe facilement d’une configuration de serveur à une autre.
  * Consulte le nombre de joueurs du serveur sélectionné.
* Mises à jour automatiques. Oui, le launcher se met à jour tout seul.
* Affiche l’état des services Mojang.

Cette liste n’est pas exhaustive. Télécharge et installe le launcher pour découvrir tout ce qu’il peut faire !

#### Besoin d’aide ? [Consulte le wiki.][wiki]

#### Tu aimes le projet ? Laisse une ⭐ sur le dépôt !

## Téléchargements

Tu peux télécharger depuis les [Releases GitHub](https://github.com/dscalzi/HeliosLauncher/releases)

#### Dernière version

[![](https://img.shields.io/github/release/dscalzi/HeliosLauncher.svg?style=flat-square)](https://github.com/dscalzi/HeliosLauncher/releases/latest)

#### Dernière pré-version
[![](https://img.shields.io/github/release/dscalzi/HeliosLauncher/all.svg?style=flat-square)](https://github.com/dscalzi/HeliosLauncher/releases)

**Plateformes prises en charge**

Si tu télécharges depuis l’onglet [Releases](https://github.com/dscalzi/HeliosLauncher/releases), sélectionne l’installateur correspondant à ton système.

| Plateforme | Fichier |
| -------- | ---- |
| Windows x64 | `Helios-Launcher-setup-VERSION.exe` |
| macOS x64 | `Helios-Launcher-setup-VERSION-x64.dmg` |
| macOS arm64 | `Helios-Launcher-setup-VERSION-arm64.dmg` |
| Linux x64 | `Helios-Launcher-setup-VERSION.AppImage` |

## Console

Pour ouvrir la console, utilise le raccourci clavier suivant.

```console
ctrl + shift + i
```

Assure-toi que l’onglet console est sélectionné. Ne colle rien dans la console sauf si tu es sûr à 100 % de ce que cela va faire. Coller la mauvaise chose peut exposer des informations sensibles.

Exporter la sortie dans un fichier
Si tu veux exporter la sortie de la console, fais simplement un clic droit n’importe où dans la console et clique sur Enregistrer sous..

Développement

Cette section détaille la mise en place d’un environnement de développement de base.

Bien démarrer

Configuration requise
	•	Node.js￼ v22

**Cloner et installer les dépendances**
```
> git clone https://github.com/dscalzi/HeliosLauncher.git
> cd HeliosLauncher
> npm install
```

**Lancer l’application**
```> npm start
```

**Construire les installateurs**

Pour construire pour ta plateforme actuelle.
> npm run dist

| Platforme   | Commande             |
| ----------- | -------------------- |
| Windows x64 | `npm run dist:win`   |
| macOS       | `npm run dist:mac`   |
| Linux x64   | `npm run dist:linux` |

Les builds pour macOS peuvent ne pas fonctionner sur Windows/Linux et inversement.

⸻

Visual Studio Code

Tout le développement du launcher doit être fait avec Visual Studio Code￼.

Colle ce qui suit dans .vscode/launch.json
```
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Déboguer le processus principal",
      "type": "node",
      "request": "launch",
      "cwd": "${workspaceFolder}",
      "program": "${workspaceFolder}/node_modules/electron/cli.js",
      "args" : ["."],
      "outputCapture": "std"
    },
    {
      "name": "Déboguer le processus renderer",
      "type": "chrome",
      "request": "launch",
      "runtimeExecutable": "${workspaceFolder}/node_modules/.bin/electron",
      "windows": {
        "runtimeExecutable": "${workspaceFolder}/node_modules/.bin/electron.cmd"
      },
      "runtimeArgs": [
        "${workspaceFolder}/.",
        "--remote-debugging-port=9222"
      ],
      "webRoot": "${workspaceFolder}"
    }
  ]
}
```
Cela ajoute deux configurations de débogage.

Déboguer le processus principal
Cela te permet de déboguer le processus principal￼ d’Electron. Tu peux déboguer les scripts du processus renderer￼ en ouvrant la fenêtre DevTools.

Déboguer le processus renderer
Cela te permet de déboguer le processus renderer￼ d’Electron. Cela nécessite d’installer l’extension Debugger for Chrome￼.

Note que tu ne peux pas ouvrir la fenêtre DevTools en utilisant cette configuration de débogage. Chromium n’autorise qu’un seul débogueur, en ouvrir un autre fera planter le programme.

⸻

Note sur l’utilisation de tiers

Merci de créditer l’auteur original et de fournir un lien vers la source originale. C’est un logiciel libre, fais au moins cela.

Pour les instructions concernant la configuration de l’authentification Microsoft, voir https://github.com/dscalzi/HeliosLauncher/blob/master/docs/MicrosoftAuth.md.

⸻

Ressources
	•	Wiki￼
	•	Nebula (Créer Distribution.json)￼
	•	Branche v2 Rewrite (Inactive)￼

Le meilleur moyen de contacter les développeurs est via Discord.


⸻

À bientôt en jeu.
