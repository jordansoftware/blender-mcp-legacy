# Blender MCP Server Add-on for Blender 4.2, 4.3, 4.4 & 4.5 (Intel Mac compatible)

**Run the Blender Lab MCP (Model Context Protocol) server add-on on Blender 4.x** — an
unofficial, minimally patched build of [Blender Lab MCP v1.0.3](https://www.blender.org/lab/mcp-server/)
for users who cannot upgrade to Blender 5.1, such as **macOS Intel (x86_64)** users stuck on Blender 4.5 LTS.

[![Download](https://img.shields.io/github/v/release/jordansoftware/blender-mcp-legacy?label=download)](https://github.com/jordansoftware/blender-mcp-legacy/releases/latest)
![Blender 4.2–4.5](https://img.shields.io/badge/Blender-4.2%E2%80%934.5-orange?logo=blender&logoColor=white)
![License GPL-3.0](https://img.shields.io/badge/license-GPL--3.0--or--later-blue)

**⬇️ [Download `mcp-1.0.3-blender4.5.zip`](https://github.com/jordansoftware/blender-mcp-legacy/releases/latest)**

[English](#english) · [Français](#français)

---

## English

### What is this?

This is a **modified, unofficial** version of the **MCP** add-on for Blender, made by
**Blender Lab** — <https://www.blender.org/lab/mcp-server/>. The add-on runs a local
MCP (Model Context Protocol) server inside Blender so that an LLM client can interact
with Blender.

The upstream add-on (v1.0.3) requires Blender 5.1+. This fork lowers that requirement so
it can be used on **Blender 4.2 to 4.5** — useful for example on Intel Macs, which cannot
run Blender versions newer than 4.5.

> **Not affiliated with or endorsed by the Blender Foundation / Blender Lab.**
> All credit for the add-on goes to its original authors. Please do not report issues
> with this build to Blender Lab.

### Changes from upstream v1.0.3

The first commit of this repository contains the untouched upstream files; the second
commit contains all modifications, so `git diff HEAD~1` shows them exactly.

1. **`blender_manifest.toml`** — `blender_version_min` changed from `"5.1.0"` to `"4.2.0"`.
2. **`weak_sandbox.py`** — the private hook `bpy.ops._op_create_function` is now read with
   `getattr`. If it does not exist (Blender 4.x), blocking of dangerous operators is
   skipped instead of crashing, and the matching restore step is skipped too.

### Tested versions

<!-- TODO: list the Blender versions / OS you tested on -->
- _To be completed._

### Installation

1. Download [`mcp-1.0.3-blender4.5.zip`](https://github.com/jordansoftware/blender-mcp-legacy/releases/latest) (or zip the `.py` files and
   `blender_manifest.toml` yourself).
2. In Blender: **Edit > Preferences > Get Extensions**, open the drop-down menu (top right)
   and choose **Install from Disk…**, then select the zip.
3. In **Edit > Preferences > System**, enable **Allow Online Access** (the add-on needs
   network permission to run its local server).

### Known limitation

On Blender 4.x the private hook used to block dangerous operators may not exist. In that
case **dangerous-operator blocking is likely inactive**: code executed through MCP is
less restricted than on Blender 5.1+. Only connect clients you trust.

### FAQ

**Can I use the Blender MCP add-on on an Intel Mac?**
Yes. Blender 5.x does not support Intel Macs, and the official add-on requires Blender 5.1+.
This build lowers the requirement to Blender 4.2 so it runs on Blender 4.5 LTS on macOS Intel.

**Does it work on Windows and Linux with Blender 4.x?**
The changes are not platform-specific, so it should work wherever Blender 4.2–4.5 runs.

**How does it connect?**
Like the original, the add-on starts a local TCP server (default `localhost:9876`, configurable
in the add-on preferences). It can also run headless:
`blender --background file.blend --command blender_mcp`.

**Should I use this on Blender 5.1+?**
No — use the [official add-on](https://www.blender.org/lab/mcp-server/) instead.

### License

GPL-3.0-or-later, same as the original add-on. See [LICENSE](LICENSE).

---

## Français

### De quoi s'agit-il ?

Ceci est une version **modifiée et non officielle** de l'add-on Blender **MCP**, créé par
**Blender Lab** — <https://www.blender.org/lab/mcp-server/>. L'add-on lance un serveur MCP
(Model Context Protocol) local dans Blender pour permettre à un client LLM d'interagir
avec Blender.

L'add-on original (v1.0.3) exige Blender 5.1 ou plus. Cette version abaisse ce prérequis
pour fonctionner sur **Blender 4.2 à 4.5** — utile par exemple sur les Mac Intel, limités
à Blender 4.5.

> **Ni affilié à la Blender Foundation / Blender Lab, ni approuvé par eux.**
> Tout le mérite de l'add-on revient à ses auteurs d'origine. Merci de ne pas signaler
> à Blender Lab les problèmes liés à cette version.

### Modifications par rapport à la v1.0.3 originale

Le premier commit de ce dépôt contient les fichiers originaux intacts ; le second contient
toutes les modifications, donc `git diff HEAD~1` les montre précisément.

1. **`blender_manifest.toml`** — `blender_version_min` passé de `"5.1.0"` à `"4.2.0"`.
2. **`weak_sandbox.py`** — le hook privé `bpy.ops._op_create_function` est lu avec
   `getattr`. S'il n'existe pas (Blender 4.x), le blocage des opérateurs dangereux est
   ignoré au lieu de planter, et la restauration correspondante est sautée.

### Versions testées

<!-- TODO : indiquer les versions de Blender / OS testés -->
- _À compléter._

### Installation

1. Téléchargez [`mcp-1.0.3-blender4.5.zip`](https://github.com/jordansoftware/blender-mcp-legacy/releases/latest) (ou zippez vous-même les fichiers `.py`
   et `blender_manifest.toml`).
2. Dans Blender : **Édition > Préférences > Get Extensions**, ouvrez le menu déroulant
   (en haut à droite) et choisissez **Install from Disk…**, puis sélectionnez le zip.
3. Dans **Édition > Préférences > System**, activez **Allow Online Access** (l'add-on a
   besoin de l'accès réseau pour lancer son serveur local).

### Limitation connue

Sous Blender 4.x, le hook privé servant à bloquer les opérateurs dangereux peut ne pas
exister. Dans ce cas, **le blocage des opérateurs dangereux est probablement inactif** :
le code exécuté via MCP est moins restreint que sous Blender 5.1+. Ne connectez que des
clients de confiance.

### FAQ

**Puis-je utiliser l'add-on MCP de Blender sur un Mac Intel ?**
Oui. Blender 5.x ne prend pas en charge les Mac Intel, et l'add-on officiel exige Blender 5.1+.
Cette version abaisse le prérequis à Blender 4.2, ce qui permet de l'utiliser avec Blender 4.5 LTS
sur macOS Intel.

**Fonctionne-t-il sous Windows et Linux avec Blender 4.x ?**
Les modifications ne dépendent pas de la plateforme : il devrait fonctionner partout où tourne
Blender 4.2–4.5.

**Comment se fait la connexion ?**
Comme l'original, l'add-on lance un serveur TCP local (par défaut `localhost:9876`, modifiable
dans les préférences de l'add-on). Il peut aussi tourner sans interface :
`blender --background file.blend --command blender_mcp`.

**Faut-il l'utiliser avec Blender 5.1+ ?**
Non, utilisez plutôt l'[add-on officiel](https://www.blender.org/lab/mcp-server/).

### Licence

GPL-3.0-or-later, comme l'add-on original. Voir [LICENSE](LICENSE).
