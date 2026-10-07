# AI at Work

![AI at Work](Mistral4/images/Mistral_at_work_gemini_092026.jpg)

Ce dépôt sert à analyser des entretiens sur la place de l’intelligence artificielle dans le travail de scientifiques, de professionnels et de créatifs.

## Sources des données

Les entretiens proviennent du jeu de données public [Anthropic Interviewer](https://huggingface.co/datasets/Anthropic/AnthropicInterviewer), décrit dans [l’article d’Anthropic](https://www.anthropic.com/research/anthropic-interviewer). Les entretiens ont été publiés avec le consentement des participants. Le jeu de données est sous licence CC-BY.

Les trois fichiers sources sont dans `Mistral4/`. Ensemble, ils contiennent 1 250 entretiens :

- `scientists_transcripts.csv`
- `workforce_transcripts.csv`
- `creatives_transcripts.csv`

## Étapes d’analyse

1. **Préparer les données** : exécuter `Mistral4/prepare_creatives_transcripts.ipynb`. Le notebook rassemble les trois fichiers dans `transcripts.csv`, puis conserve les réponses `User:` dans `transcripts_responses.csv`.
2. **Configurer les GPU** : suivre les modalités d’accès aux ressources de calcul de l’[Institut ACSS-PSL](https://acss-dig.psl.eu/en/plateforme). Le notebook d’annotation utilise trois GPU, en masquant le GPU 1 déjà réservé sur la machine (`CUDA_VISIBLE_DEVICES=0,2,3`). Il s’appuie sur [Mistral Small 4](https://huggingface.co/mistralai/Mistral-Small-4-119B-2603) avec [Transformers](https://huggingface.co/docs/transformers/model_doc/mistral4).
3. **Détecter les professions** : dans `Mistral4/mistral4_transformers_test.ipynb`, exécuter la section « Analyse des réponses : type de métier ». Elle crée `transcripts_job_types_full.csv`.
4. **Repérer les aspects vécus** : exécuter la section « Analyse des aspects principaux de l’expérience vécue ». Elle extrait jusqu’à sept aspects par entretien et crée `transcripts_experience_aspects_top7_full.csv`.
5. **Regrouper les modalités** : exécuter `Mistral4/bacasable.ipynb`. Le notebook regroupe les intitulés détaillés en 20 catégories de professions et 20 catégories d’aspects, puis contrôle les effectifs, les fréquences et la catégorie « Autres ».
6. **Comparer professions et aspects** : exécuter la section AFCM de `Mistral4/bacasable.ipynb`. Elle croise uniquement les nouvelles modalités regroupées et produit le tableau de contingence, les coordonnées et l’inertie dans `Mistral4/data/results/`, ainsi que la carte factorielle dans `Mistral4/images/`.

Les fichiers d’annotation sont générés à l’exécution à partir des 1 250 entretiens. Le notebook `bacasable.ipynb` utilise ces résultats complets pour construire les catégories regroupées et l’AFCM ; ses tableaux, coordonnées, mesures d’inertie et figures sont exportés dans les dossiers `Mistral4/data/results/` et `Mistral4/images/`.
