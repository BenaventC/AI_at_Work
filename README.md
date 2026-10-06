# AI at Work

Ce dépôt sert à analyser des entretiens sur la place de l’intelligence artificielle dans le travail de scientifiques, de professionnels et de créatifs.

## Sources des données

Les entretiens proviennent du jeu de données public [Anthropic Interviewer](https://huggingface.co/datasets/Anthropic/AnthropicInterviewer), décrit dans [l’article d’Anthropic](https://www.anthropic.com/research/anthropic-interviewer). Les entretiens ont été publiés avec le consentement des participants. Le jeu de données est sous licence CC-BY.

Les trois fichiers sources sont dans `Mistral4/` :

- `scientists_transcripts.csv`
- `workforce_transcripts.csv`
- `creatives_transcripts.csv`

## Étapes d’analyse

1. **Préparer les données** : exécuter `Mistral4/prepare_creatives_transcripts.ipynb`. Le notebook rassemble les trois fichiers dans `transcripts.csv`, puis conserve les réponses `User:` dans `transcripts_responses.csv`.
2. **Configurer les GPU** : suivre les modalités d’accès aux ressources de calcul de l’[Institut ACSS-PSL](https://acss-dig.psl.eu/en/plateforme). Le notebook d’annotation utilise trois GPU, en masquant le GPU 1 déjà réservé sur la machine (`CUDA_VISIBLE_DEVICES=0,2,3`). Il s’appuie sur [Mistral Small 4](https://huggingface.co/mistralai/Mistral-Small-4-119B-2603) avec [Transformers](https://huggingface.co/docs/transformers/model_doc/mistral4).
3. **Détecter les professions** : dans `Mistral4/mistral4_transformers_test.ipynb`, exécuter la section « Analyse des réponses : type de métier ». Elle crée `transcripts_job_types_full.csv`.
4. **Repérer les aspects vécus** : exécuter la section « Analyse des aspects principaux de l’expérience vécue ». Elle extrait jusqu’à sept aspects par entretien et crée `transcripts_experience_aspects_top7_full.csv`.
5. **Comparer professions et aspects** : exécuter la section AFC. Elle produit le tableau croisé, les coordonnées et l’inertie dans `Mistral4/data/results/`, ainsi que le graphique dans `Mistral4/images/`.

Les CSV d’analyse et rapports sont générés à l’exécution et ne sont pas inclus dans le dépôt. Le graphique actuellement présent dans `Mistral4/images/` correspond à une analyse antérieure du seul corpus créatif ; relancer les étapes d’annotation et l’AFC produit les résultats du corpus combiné.
