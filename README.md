# Themes PERCEVAL : Asciidoctor PDF

Thèmes et gabarit pour la génération de documents PDF professionnels avec Asciidoctor.

## Prérequis

```bash
gem install asciidoctor-pdf rouge
```

## Charte

Le thème applique la charte graphique de Perceval (direction « Plan ») :
- **Couleurs** : papier `#EFEEEC` (fond des pages), blanc cassé `#F8F8F6` (code, encadrés, lignes de tableau), encre `#121014` (texte), pourpre nuit `#2A1834` (couverture, en-têtes de tableau), pourpre `#A2457F` (liens), or `#E2BD3C` (filets, puces, cadres ; jamais en texte sur fond clair), gris clair `#BDBDBD` (filets).
- **Polices** : Jost (300, 400, 500) pour les titres et le texte, DM Mono pour le code, les commandes et les chiffres.
- **Signes** : filet or sous les titres de niveau 1, puces en croix or, angles de 2 pt, couverture minuit avec croisillons et frise à points or, logo isolé en bas à gauche de la couverture et du pied de page.
- Couleurs TLP 2.0 (FIRST) et échelle de criticité des vulnérabilités hors charte, assombries pour rester lisibles sur papier (contraste ≥ 4,5:1).

## Structure du dépôt

```
theme-asciidoc/
├── demo.adoc                     # Document de référence (tous les éléments du thème)
├── demo.pdf                      # Rendu PDF de référence
└── themes/
    ├── PERCEVAL-A4-theme.yml     # Thème (couleurs, typographie, mise en page)
    ├── icones/                   # Pictos des encadrés (charte : info, ampoule, cible, alerte, bouclier)
    ├── fonts/
    │   ├── Jost/                 # Titres et texte (OFL)
    │   ├── DM_Mono/              # Code, commandes, chiffres (OFL)
    │   └── Perceval_Croix/       # Croix du logo, pour les puces et cases à cocher
    └── img/
        ├── couverture-perceval.svg           # Fond de couverture (logo inclus)
        ├── perceval-logo-horizontal.svg      # Pied de page
        └── perceval-logo-horizontal-sombre.svg
```

## Générer un PDF

```bash
asciidoctor-pdf \
    -a pdf-themesdir=themes \
    -a pdf-fontsdir=themes/fonts \
    -a icons=image \
    mon-document.adoc
```

- `-a pdf-themesdir=themes` : indique le dossier contenant le fichier `.yml` du thème
- `-a pdf-fontsdir=themes/fonts` : indique le dossier contenant les polices
- `-a icons=image` : encadrés (NOTE, TIP, IMPORTANT, WARNING, CAUTION) illustrés avec les pictos de la charte ; sans cette option ou avec `:icons: font`, icônes Font Awesome au trait

## Créer un nouveau document

1. Copier `demo.adoc` comme point de départ
2. Adapter l'en-tête du document :

```asciidoc
= Titre du Document
Prénom NOM <email@perceval.sh>
:pdf-page-size: A4
:pdf-theme: PERCEVAL-A4-theme.yml
:icons: image
:source-highlighter: rouge
:toc: macro
:toclevels: 4
:toc-title: Sommaire
:sectnums:
:appendix-caption: Annexe
:client: NOM DU CLIENT
:website: www.perceval.sh
:title-page: Titre affiché en en-tête
:tlp: clear
:doc-version: 1.0.0
:doc-date: 2026-01-01
:imagesdir: img/
:hide-uri-scheme:
:encoding: UTF-8
```

### Attributs clés

| Attribut | Description | Valeurs possibles |
|---|---|---|
| `:tlp:` | Classification TLP (apparaît sur la couverture et en en-tête) | `clear`, `green`, `amber`, `red` |
| `:doc-version:` | Version du document | `1.0.0`, `2.3.1`, … |
| `:doc-date:` | Date du document | `2026-05-10` |
| `:client:` | Nom du client (apparaît en en-tête) | texte libre |
| `:title-page:` | Titre court affiché dans l'en-tête des pages intérieures | texte libre |

3. Lancer la génération depuis le dossier contenant votre `.adoc` :

```bash
asciidoctor-pdf \
    -a pdf-themesdir=/chemin/vers/themes \
    -a pdf-fontsdir=/chemin/vers/themes/fonts \
    mon-document.adoc
```

## Rôles disponibles

| Rôle | Rendu |
|---|---|
| `[.pourpre]#…#` | accent pourpre |
| `[.encre]#…#`, `[.papier]#…#` | encre ; papier (sur fond sombre) |
| `[.or]#…#` | or, uniquement sur fond sombre |
| `[.chiffre]#…#` | chiffres et valeurs en DM Mono |
| `[.color-vuln-informational]`, `-low`, `-medium`, `-high`, `-critical` | criticité des vulnérabilités |
| `[.tlpclear]`, `[.tlpgreen]`, `[.tlpamber]`, `[.tlpred]` | étiquettes TLP |
| `[.red]`, `[.orange]`, `[.green]`, `[.blue]` (et `u…` en capitales) | couleurs sémantiques |
| `[.gold]`, `[.marron]` | anciens rôles conservés : rendus en pourpre et en encre |
