# Template Compte Rendu de TP — ENSIASD

Template LaTeX pour rédiger un **compte rendu de travaux pratiques (TP)** avec
**coloration syntaxique** du code. Il est adapté du template de rapport de
stage ENSIASD et compile avec **XeLaTeX**.

## Aperçu

- Page de garde propre (module, numéro et titre du TP, étudiant, groupe, enseignant).
- Sommaire automatique.
- Boîtes de code avec **coloration syntaxique** et titre (nom du fichier).
- Boîtes de terminal (fond sombre) pour les sorties console.
- Boîtes « Remarque / Consigne » pour les énoncés.
- Figures, tableaux et renvois (`Figure I.1`, `Tableau I.1`, `\ref{...}`).
- Numérotation des parties en chiffres romains (Partie I, II, …) et sections
  en `I.1`, `I.2`, …

## Structure du projet

```
.
├── main.tex                 Fichier principal (configuration + préambule)
├── front/cover.tex          Page de garde
├── chapters/
│   ├── introduction.tex     Introduction, objectifs et environnement
│   ├── partie1.tex          Partie I  (exemple Python)
│   ├── partie2.tex          Partie II (exemple C + SQL + figure)
│   └── conclusion.tex       Conclusion
├── images/                  Logo et captures d'écran
└── README.md
```

## Prérequis

- **MiKTeX** (Windows) ou **TeX Live** (Linux/macOS).
- Compilateur **XeLaTeX** (obligatoire à cause de `fontspec`).
- Un éditeur : TeXstudio, VS Code + LaTeX Workshop, ou le terminal.

Sur MiKTeX, les packages manquants (`tcolorbox`, `listings`, …) sont
téléchargés automatiquement au premier lancement (connexion Internet requise).

## Compilation

Compilez **2 à 3 fois** (le sommaire et les renvois ont besoin de plusieurs
passes) :

```bash
xelatex -interaction=nonstopmode main.tex
xelatex -interaction=nonstopmode main.tex
xelatex -interaction=nonstopmode main.tex
```

Ou, avec `latexmk` :

```bash
latexmk -xelatex main.tex
```

### Overleaf

1. Uploadez le dossier (ou importez le dépôt GitHub).
2. Menu → Compilateur → **XeLaTeX**.
3. Recompilez 2 à 3 fois.

## Personnalisation

Toutes les informations personnelles sont regroupées en haut de `main.tex`,
section **1. INFORMATIONS PERSONNALISABLES** :

```latex
\newcommand{\moduleNom}{Programmation Python}
\newcommand{\tpNumero}{TP N\textsuperscript{o}~1}
\newcommand{\tpTitre}{Titre du compte rendu de TP}
\newcommand{\etudiantNom}{Prénom Nom}
\newcommand{\etudiantGroupe}{Groupe 3}
\newcommand{\enseignantNom}{Pr. Nom de l'enseignant}
```

Le logo se place dans `images/` sous le nom `logo_ensiasd.png` (modifiable via
`\logoEcole`).

## Écrire du code

### Boîte de code

```latex
\begin{code}[language=Python]{fichier.py}
def bonjour(nom):
    print(f"Bonjour, {nom} !")
\end{code}
```

- Le titre entre accolades (`fichier.py`) apparaît dans l'en-tête de la boîte.
- L'option facultative `[...]` accepte **toutes les options de `listings`**,
  par exemple : `language=C`, `numbers=none`, `firstnumber=10`, `frame=none`.

### Sortie terminal

```latex
\begin{terminal}
$ python fichier.py
Bonjour, ENSIASD !
\end{terminal}
```

### Code en ligne

```latex
La fonction \codeinline{moyenne} renvoie une valeur flottante.
```

### Encadré « Consigne »

```latex
\begin{remarque}[Consigne]
Écrire un programme qui ...
\end{remarque}
```

## Langages de coloration supportés

`listings` intègre nativement, entre autres :
`Python`, `C`, `C++`, `Java`, `SQL`, `HTML`, `XML`, `PHP`, `bash`/`sh`,
`Matlab`, `R` (via `language=R`), `Pascal`, `Lisp`, `Perl`, `Ruby`.

Pour un langage non listé, il suffit de définir un style `lstdefinelanguage`
(voir la documentation de `listings`).

## Astuces

- **Plusieurs passes** : si le sommaire affiche `??`, recompilez.
- **Liste des figures** : décommentez le bloc correspondant dans `main.tex`.
- **Lignes longues** : elles sont automatiquement coupées (option
  `breaklines=true`), avec un symbole `↪` en fin de ligne.
- **Polices** : `TeX Gyre Termes` (texte) et `TeX Gyre Cursor` (code). Pour en
  changer, modifiez `\setmainfont` / `\setmonofont` dans `main.tex`.
