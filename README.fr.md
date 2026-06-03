# bXSS Discovery

[English](./README.md) | [中文](./README.zh-CN.md) | **Français**

Atelier local-first et attentif à l'OPSEC pour créer des requêtes de recherche limitées au périmètre et découvrir des surfaces publiques de saisie pendant des évaluations bXSS autorisées.

## Aperçu

bXSS Discovery est un atelier local-first dans le navigateur pour créer des requêtes de recherche limitées au périmètre autorisé et repérer des surfaces publiques de saisie utilisateur pendant des évaluations autorisées.

L'outil se concentre sur la découverte, le triage et les notes reproductibles. Il ne soumet pas de payload, ne lance pas de scan et n'interagit pas directement avec les applications cibles.

## Usage Prévu

À utiliser uniquement dans un cadre autorisé : évaluations internes, tests approuvés par un client ou programmes de bug bounty dont le périmètre permet cette activité de découverte.

Les requêtes générées réduisent les résultats de recherche publics. Elles ne prouvent pas une vulnérabilité et ne remplacent pas la validation manuelle.

## Fonctionnalités

- Générateur de requêtes avec domaine ou hôte normalisé
- Interface anglaise par défaut, avec bascule chinoise et française
- 36 modèles de découverte revus, avec filtrage par catégorie et mots-clés
- Panneaux numérotés pour le périmètre, le modèle, la requête, les paramètres, le triage et l'explication
- Sélection d'un seul moteur parmi Google, Bing, DuckDuckGo ou Baidu
- Génération de requêtes adaptée au moteur, sans réutiliser aveuglément une syntaxe Google générique
- Explications détaillées du périmètre, des correspondances, du moteur choisi, des dégradations syntaxiques et des filtres
- File et historique pour conserver le contexte de triage
- Thème clair par défaut, avec bascule sombre
- Application statique en un seul fichier, hébergeable partout

## Démarrage Rapide

Ouvrez `index.html` directement dans un navigateur, ou servez-le localement :

```bash
python3 -m http.server 4173 --bind 127.0.0.1
```

Puis ouvrez :

```text
http://127.0.0.1:4173/
```

## Flux De Travail

1. Définir le périmètre cible autorisé, par exemple `redteamnotes.com` ou `app.redteamnotes.com`.
2. Confirmer l'autorisation de test pour ce périmètre.
3. Filtrer ou choisir un modèle dans la bibliothèque.
4. Lire la requête générée et son explication avant d'ouvrir les résultats.
5. Ajuster les paramètres, dont un moteur sélectionné et les filtres optionnels. La commande générée change selon le moteur afin d'éviter les opérateurs non compatibles.
6. Ouvrir la requête seulement si le périmètre et l'autorisation sont corrects.
7. Mettre les requêtes utiles en file avec une courte note de triage.
8. Examiner les résultats manuellement et relier les preuves au périmètre et à la requête d'origine.

## Notes OPSEC

- Garder les recherches dans les domaines ou hôtes explicitement autorisés.
- Utiliser l'hôte exact lorsque l'autorisation est étroite.
- Ne pas soumettre de payload depuis cet outil de découverte.
- Traiter l'historique de recherche, l'historique navigateur, les captures, le stockage local et les notes comme des artefacts d'évaluation.
- Ne pas coller de données privées de cible dans des moteurs publics sauf si les règles l'autorisent.
- Vérifier les redirections ; les résultats peuvent pointer vers des help desks, ATS ou portails support tiers.

Pour plus de conseils opérationnels, voir [OPSEC.md](./OPSEC.md).

## Personnalisation Des Modèles

Les modèles sont définis dans le tableau `dorks` de `index.html`. Chaque entrée contient :

- `id` : identifiant stable
- `title` : nom anglais du modèle
- `category` : groupe utilisé par la bibliothèque
- `icon` : classe Font Awesome utilisée par le repère compact
- `intensity` : indice de triage comme `Low noise`, `Targeted` ou `Broad`
- `operator` : étiquette interne de recherche/filtrage ; l'interface l'affiche comme correspondance de titre, URL ou texte
- `description` : intention du modèle
- `query` : fragment ajouté après `site:{scope}`

La bibliothèque actuelle contient 36 modèles revus couvrant les surfaces d'entrée, feedback, support, confiance/sûreté, carrières, marketing, ventes, identité et opérations.

Les moteurs de recherche ne partagent pas une syntaxe dork identique. L'application conserve la forme Google la plus riche lorsque c'est pertinent, utilise `intitle`, `inbody`, `OR` et `NOT` pour Bing, garde DuckDuckGo sur des opérateurs de champ et d'exclusion plus focalisés, et génère des requêtes Baidu prudentes avec `intitle`, `inurl` et `site`.

Gardez les nouveaux modèles spécifiques, explicables et faciles à trier. Évitez les termes trop larges qui retournent surtout des pages marketing, politiques ou documentaires.

## Déploiement Et Stockage

C'est une application statique. Elle peut être hébergée via GitHub Pages, un site statique interne ou n'importe quel serveur de fichiers statiques.

Pour les évaluations sensibles, privilégiez une instance locale et évitez analytics, collecte d'erreurs distante ou journaux d'accès capturant les noms de cibles et les termes de requête.

L'application stocke les préférences d'interface, la file et l'historique dans le `localStorage` du navigateur. Effacez ce stockage lorsque les règles d'engagement l'exigent.

## Licence

Copyright © RedteamNotes. All rights reserved.
