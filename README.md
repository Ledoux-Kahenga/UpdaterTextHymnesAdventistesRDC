# Mises à jour de textes (GitHub)

## Publication

1. Créez un **repo GitHub public** (ex. `sda-hymnes-updates`).
2. Copiez ce dossier à la racine du repo (ou dans `remote_text_updates/`).
3. Dans l’app, réglez l’URL dans `AppConstants.textUpdatesBaseUrl` :

```
https://raw.githubusercontent.com/VOTRE_USER/sda-hymnes-updates/main/
```

(avec le `/` final)

## Fichiers

| Fichier | Rôle |
|---------|------|
| `version.txt` | Entier (ex. `2`). L’app ne télécharge le JSON que si plus grand que la version locale. |
| `text_updates.json` | Liste des corrections (`patches`). |

## Workflow correction

1. Incrémentez `version` dans **les deux** fichiers (`version.txt` et `"version"` du JSON).
2. Ajoutez un patch :

```json
{
  "table": "HLTb",
  "number": 42,
  "title": "Nouveau titre",
  "lyric": "Paroles corrigées..."
}
```

3. `git commit` + `git push`.
4. Au prochain démarrage (avec Internet), l’app applique les patches.

## Champs d’un patch

| Champ | Effet |
|-------|--------|
| `table` | Nom SQLite (`HLTb`, `NZKristoTb`, `SDAH`…) |
| `number` | Numéro du chant |
| `title` | Titre local |
| `title_en` | Titre anglais (si la table en a un) |
| `lyric` | Paroles / strophes |
| `fields` | Optionnel : colonnes SQL exactes `{ "titleLyric": "..." }` |

Les champs à `null` ou absents sont ignorés.
