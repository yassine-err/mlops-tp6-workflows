# Orchestrateur ou integration continue ? (TP06)

| Critere | Prefect (orchestrateur) | GitHub Actions (CI) |
|---|---|---|
| **Ce qui déclenche l'execution** | Une planification temporelle (cron le lundi à 6h) ou un lancement manuel (Quick run) depuis l'interface. | Un événement Git (git push) ou un lancement manuel via le bouton "Run workflow". |
| **Ou s'execute le traitement** | Sur la machine locale (via le serveur Prefect et le worker qui tourne sur le PC). | Sur les serveurs distants de GitHub (runners Ubuntu). |
| **Qui surveille, et ou** | L'équipe, via le tableau de bord web de Prefect (http://127.0.0.1:4200). | L'équipe, via l'onglet "Actions" du dépôt GitHub. |
| **Ce qui se passe en cas d'echec** | Le flow passe en état "Failed", la tâche fautive est identifiée en rouge et la tâche suivante (notifier) n'est pas exécutée. | Le job passe au rouge, le commit est marqué d'une croix sur GitHub, et un e-mail d'alerte peut être envoyé. |
| **Type de tache adapte** | Traitements longs, récurrents et planifiés (ex: réentraînement hebdomadaire, mise à jour de modèles). | Vérifications rapides à chaque modification du code (tests unitaires, validation de la qualité). |
| **Ce qui est versionne dans Git** | Le code des workflows (`flow_mlops.py`), le script de planification (`planifier.py`) et la config (`prefect.yaml`). | Le fichier de configuration de la CI (`.github/workflows/ci.yml`), les scripts de test (`verifier_qualite.py`) et `requirements-ci.txt`. |

## Conclusion (5 lignes)
L'intégration continue (CI) et l'orchestration sont deux approches complémentaires qui ne se remplacent pas. 
GitHub Actions valide le code à chaque modification (git push) sur un serveur distant pour s'assurer qu'il est sain avant d'être fusionné. 
Prefect exécute et surveille des traitements récurrents sur nos machines (ou serveurs) pour maintenir le modèle à jour dans le temps.
L'orchestrateur gère l'exécution opérationnelle, tandis que la CI sécurise le développement et la qualité du code.
Ensemble, ils forment une chaîne MLOps robuste où le code est vérifié avant de déclencher des workflows de production.