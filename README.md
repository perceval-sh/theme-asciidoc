# Themes PERCEVAL — Asciidoctor PDF

Thèmes et gabarit pour la génération de documents PDF professionnels avec Asciidoctor.

## Prérequis

```bash
gem install asciidoctor-pdf rouge
```

## Structure du dépôt

```
theme-asciidoc/
├── demo.adoc                  # Document de référence (charte graphique complète)
├── demo.pdf                   # Rendu PDF de référence
├── img/                       # Images utilisées dans demo.adoc
└── themes/
    ├── PERCEVAL-A4-theme.yml  # Thème principal (couleurs, typographie, mise en page)
    ├── fonts/                 # Polices embarquées
    │   ├── JetBrains_Mono/    # Code et blocs source
    │   ├── League_Spartan/    # Titres
    │   └── Sofia_Sans/        # Corps de texte
    └── img/                   # Images du thème (couverture, logo, fonds)
        ├── cover-perceval.svg
        ├── logo-perceval.jpg
        └── bg-perceval-portrait.png
```

## Générer un PDF

```bash
asciidoctor-pdf \
    -a pdf-themesdir=themes \
    -a pdf-fontsdir=themes/fonts \
    mon-document.adoc
```

- `-a pdf-themesdir=themes` — indique le dossier contenant le fichier `.yml` du thème
- `-a pdf-fontsdir=themes/fonts` — indique le dossier contenant les polices

## Créer un nouveau document

1. Copier `demo.adoc` comme point de départ
2. Adapter l'en-tête du document :

```asciidoc
= Titre du Document
Prénom NOM <email@perceval.sh>
:pdf-page-size: A4
:pdf-theme: PERCEVAL-A4-theme.yml
:icons: font
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
