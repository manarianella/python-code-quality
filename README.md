# Python 2 — Qualité du code

## Présentation

Ce projet correspond au premier exercice du cours **Python 2 – Manipulation de données** à ESIEE Paris.

L'objectif est de reprendre le programme réalisé lors du test technique de Python 1 et d'améliorer la qualité du code en ajoutant des **annotations de type**.

Le programme utilisé travaille sur un fichier CSV contenant des données de population françaises. Il permet notamment de récupérer des communes, des départements et différentes informations sur leur population.

## Objectif de l'exercice

Le programme fonctionnait déjà, mais les fonctions ne précisaient pas les types des données utilisées.

Par exemple, une fonction était initialement définie de cette manière :

```python
def read_file(filename):
```

Elle a été modifiée ainsi :

```python
def read_file(filename: str) -> list[dict[str, str]]:
```

Cette nouvelle écriture permet de comprendre directement que :

- `filename` doit être une chaîne de caractères (`str`) ;
- la fonction retourne une liste ;
- chaque élément de cette liste est un dictionnaire ;
- les clés et les valeurs de ces dictionnaires sont des chaînes de caractères.

## Annotations de type utilisées

Plusieurs types ont été nécessaires au cours de l'exercice.

Par exemple :

```python
list[dict[str, str]]
```

représente une liste contenant des dictionnaires.

```python
list[tuple[str, str]]
```

représente une liste de tuples contenant deux chaînes de caractères.

```python
dict[str, tuple[int, int]]
```

représente un dictionnaire dont les clés sont des chaînes de caractères et les valeurs des tuples de deux entiers.

Certaines fonctions peuvent également ne retourner aucun résultat.

Par exemple :

```python
def get_pop_commune(
    data: list[dict[str, str]],
    code: str
) -> tuple[str, int, str] | None:
```

Le `| None` indique que la fonction peut retourner soit un tuple contenant les informations de la commune, soit `None` si aucune commune correspondante n'est trouvée.

## Vérification avec mypy

Pour vérifier les annotations de type, j'ai utilisé **mypy**.

Il a été ajouté au projet comme dépendance de développement avec :

```bash
uv add --dev mypy
```

Le programme a ensuite été vérifié en mode strict :

```bash
uv run mypy --strict python-13-test-population.py
```

Lors de la première vérification, **11 erreurs** étaient détectées.

Elles concernaient principalement l'absence d'annotations de type dans les fonctions.

Après avoir identifié les types des paramètres et des valeurs retournées par chaque fonction, les erreurs ont été corrigées.

Résultat final :

```text
Success: no issues found in 1 source file
```

## Ce que j'ai appris

Cet exercice m'a permis de comprendre qu'un programme qui fonctionne n'est pas forcément un programme de bonne qualité.

Les annotations de type permettent de rendre le code plus clair et de préciser les données attendues par chaque fonction.

J'ai également appris à utiliser `mypy` pour effectuer une vérification statique des types et détecter des incohérences avant même l'exécution du programme.

L'exercice m'a notamment permis de mieux comprendre les types composés comme :

```python
list[dict[str, str]]
list[tuple[str, str]]
tuple[str, int, str] | None
dict[str, tuple[int, int]]
```

## Outils utilisés

- Python 3.12
- uv
- mypy
- Visual Studio Code
- CSV

## Contexte

**ESIEE Paris — E4 DSIA**  
**Python 2 — Manipulation de données**  
Exercice : Qualité du code