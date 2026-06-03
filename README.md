# bXSS Discovery

Local-first, OPSEC-aware workbench for building scoped search queries to discover public intake surfaces during authorized bXSS assessments.

Languages: English, Chinese, French.

## English

### Overview

bXSS Discovery is a compact browser-based workbench for building scoped search queries that help identify public intake surfaces during authorized security assessments.

The tool focuses on discovery, triage, and repeatable notes. It does not submit payloads, run scans, or interact with target applications directly.

### Intended Use

Use this only for authorized work: internal assessments, client-approved testing, or bug bounty programs where the target scope explicitly permits discovery activity.

Generated queries narrow public search results. They are not proof of vulnerability and should not be treated as validation. Manual review is still required.

### Features

- Scoped query builder using a normalized domain or host
- English default UI with Chinese and French language switches
- Template library with category and keyword filtering
- Numbered workflow panels for scope, template, query, parameters, triage, and explanation
- Single search engine selection for Google, Bing, or DuckDuckGo
- Detailed query explanations for scope, template matching, search engine choice, and result filters
- Queue and history views for triage context
- Light theme by default, with a dark theme toggle
- Static single-file app that can be hosted anywhere

### Quick Start

Open `index.html` directly in a browser, or serve it locally:

```bash
python3 -m http.server 4173 --bind 127.0.0.1
```

Then open:

```text
http://127.0.0.1:4173/
```

### Workflow

1. Set the authorized target scope, for example `redteamnotes.com` or `app.redteamnotes.com`.
2. Confirm that you have testing authorization for that scope.
3. Filter or select a template from the template library.
4. Read the generated query and explanation before opening results.
5. Adjust query parameters, including one selected search engine and optional result filters.
6. Open the query only when scope and authorization are correct.
7. Queue promising queries with a short triage note.
8. Review results manually and keep evidence tied to the original scope and query.

### OPSEC Notes

- Keep searches scoped to domains or hosts that are explicitly authorized.
- Prefer exact hosts when authorization is narrow.
- Do not submit payloads from this discovery tool.
- Treat search engine history, browser history, screenshots, local storage, and notes as assessment artifacts.
- Do not paste private target data into public search engines unless the engagement rules allow it.
- Review redirects carefully; results may point to third-party help desks, hiring systems, or support portals.

For more operational guidance, see [OPSEC.md](./OPSEC.md).

### Customizing Templates

Templates are defined in the `dorks` array inside `index.html`. Each entry includes:

- `id`: stable template identifier
- `title`: English template name
- `category`: grouping used by the library
- `icon`: Font Awesome class used for the compact UI marker
- `intensity`: triage hint such as `Low noise`, `Targeted`, or `Broad`
- `operator`: internal syntax tag used for search/filtering; the UI presents this as title, URL, or page-text matching
- `description`: what the template is intended to find
- `query`: search query fragment appended after `site:{scope}`

Keep new templates specific, explainable, and easy to triage. Avoid broad terms that mostly return marketing, policy, or documentation pages.

### Deployment And Storage

This is a static app. You can host it through GitHub Pages, an internal static site, or any static file server.

For sensitive work, prefer a local-only instance and avoid analytics, remote error collection, or access logs that capture target names and query terms.

The app stores UI preferences and queue/history entries in browser `localStorage`. Clear local storage when required by engagement rules.

## 中文

### 概览

bXSS Discovery 是一个本地优先的浏览器工作台，用于生成带授权范围约束的搜索查询，帮助在授权安全评估中发现公开的用户输入入口。

工具关注发现、分诊和可复盘记录。它不会提交 payload，不会扫描目标，也不会直接与目标应用交互。

### 适用场景

仅用于已授权的工作：内部评估、客户批准的测试，或明确允许相关发现活动的漏洞赏金项目。

生成的查询只用于收窄公开搜索结果，不代表漏洞证明，也不能替代人工验证。

### 功能

- 使用规范化域名或主机构建带范围约束的查询
- 默认英语界面，可切换中文和法语
- 支持按分类和关键词筛选模板
- 用编号流程展示范围、模板、查询、参数、分诊和解析顺序
- 在 Google、Bing、DuckDuckGo 中单选一个搜索引擎
- 详细解释 scope、模板匹配、搜索引擎选择和结果过滤的影响
- 队列和历史视图用于保留分诊上下文
- 默认亮色主题，可切换暗色主题
- 单文件静态应用，可直接托管

### 快速开始

可以直接用浏览器打开 `index.html`，也可以本地启动服务：

```bash
python3 -m http.server 4173 --bind 127.0.0.1
```

然后访问：

```text
http://127.0.0.1:4173/
```

### 工作流程

1. 设置授权目标范围，例如 `redteamnotes.com` 或 `app.redteamnotes.com`。
2. 确认你对该范围拥有测试授权。
3. 在模板库中筛选或选择模板。
4. 打开结果前先阅读生成的查询语句和解析说明。
5. 调整查询参数，包括一个选定的搜索引擎和可选结果过滤。
6. 仅在范围和授权状态正确时打开查询。
7. 将值得跟进的查询加入队列，并写简短分诊备注。
8. 人工复核结果，并把证据和原始范围、查询语句关联起来。

### OPSEC 注意事项

- 搜索必须限制在明确授权的域名或主机内。
- 授权范围较窄时优先使用精确主机。
- 不要从这个发现工具提交 payload。
- 搜索引擎历史、浏览器历史、截图、本地存储和备注都应视为评估痕迹。
- 除非项目规则允许，不要把私有目标数据粘贴到公共搜索引擎。
- 仔细检查跳转；搜索结果可能指向第三方帮助台、招聘系统或支持门户。

更多操作安全建议见 [OPSEC.md](./OPSEC.md)。

### 自定义模板

模板定义在 `index.html` 的 `dorks` 数组中。每个条目包含：

- `id`：稳定的模板标识
- `title`：英文模板名称
- `category`：模板库中的分类
- `icon`：紧凑 UI 标记使用的 Font Awesome 类
- `intensity`：分诊提示，例如 `Low noise`、`Targeted`、`Broad`
- `operator`：内部搜索/筛选标签；界面会呈现为标题、路径或正文匹配
- `description`：模板要发现的内容
- `query`：追加在 `site:{scope}` 后面的查询片段

新增模板应保持具体、可解释、便于分诊。避免加入过宽、主要返回营销页、政策页或文档页的关键词。

### 部署和存储

这是一个静态应用，可通过 GitHub Pages、内部静态站点或任意静态文件服务器托管。

敏感评估中建议只在本地运行，并避免 analytics、远程错误收集或会记录目标名称和查询词的访问日志。

应用会在浏览器 `localStorage` 中保存界面偏好、队列和历史。必要时按项目规则清理本地存储。

## Français

### Aperçu

bXSS Discovery est un atelier local-first dans le navigateur pour créer des requêtes de recherche limitées au périmètre autorisé et repérer des surfaces publiques de saisie utilisateur pendant des évaluations autorisées.

L'outil se concentre sur la découverte, le triage et les notes reproductibles. Il ne soumet pas de payload, ne lance pas de scan et n'interagit pas directement avec les applications cibles.

### Usage Prévu

À utiliser uniquement dans un cadre autorisé : évaluations internes, tests approuvés par un client ou programmes de bug bounty dont le périmètre permet cette activité de découverte.

Les requêtes générées réduisent les résultats de recherche publics. Elles ne prouvent pas une vulnérabilité et ne remplacent pas la validation manuelle.

### Fonctionnalités

- Générateur de requêtes avec domaine ou hôte normalisé
- Interface anglaise par défaut, avec bascule chinoise et française
- Bibliothèque de modèles avec filtrage par catégorie et mots-clés
- Panneaux numérotés pour le périmètre, le modèle, la requête, les paramètres, le triage et l'explication
- Sélection d'un seul moteur parmi Google, Bing ou DuckDuckGo
- Explications détaillées du périmètre, des correspondances, du moteur choisi et des filtres
- File et historique pour conserver le contexte de triage
- Thème clair par défaut, avec bascule sombre
- Application statique en un seul fichier, hébergeable partout

### Démarrage Rapide

Ouvrez `index.html` directement dans un navigateur, ou servez-le localement :

```bash
python3 -m http.server 4173 --bind 127.0.0.1
```

Puis ouvrez :

```text
http://127.0.0.1:4173/
```

### Flux De Travail

1. Définir le périmètre cible autorisé, par exemple `redteamnotes.com` ou `app.redteamnotes.com`.
2. Confirmer l'autorisation de test pour ce périmètre.
3. Filtrer ou choisir un modèle dans la bibliothèque.
4. Lire la requête générée et son explication avant d'ouvrir les résultats.
5. Ajuster les paramètres, dont un moteur sélectionné et les filtres optionnels.
6. Ouvrir la requête seulement si le périmètre et l'autorisation sont corrects.
7. Mettre les requêtes utiles en file avec une courte note de triage.
8. Examiner les résultats manuellement et relier les preuves au périmètre et à la requête d'origine.

### Notes OPSEC

- Garder les recherches dans les domaines ou hôtes explicitement autorisés.
- Utiliser l'hôte exact lorsque l'autorisation est étroite.
- Ne pas soumettre de payload depuis cet outil de découverte.
- Traiter l'historique de recherche, l'historique navigateur, les captures, le stockage local et les notes comme des artefacts d'évaluation.
- Ne pas coller de données privées de cible dans des moteurs publics sauf si les règles l'autorisent.
- Vérifier les redirections ; les résultats peuvent pointer vers des help desks, ATS ou portails support tiers.

Pour plus de conseils opérationnels, voir [OPSEC.md](./OPSEC.md).

### Personnalisation Des Modèles

Les modèles sont définis dans le tableau `dorks` de `index.html`. Chaque entrée contient :

- `id` : identifiant stable
- `title` : nom anglais du modèle
- `category` : groupe utilisé par la bibliothèque
- `icon` : classe Font Awesome utilisée par le repère compact
- `intensity` : indice de triage comme `Low noise`, `Targeted` ou `Broad`
- `operator` : étiquette interne de recherche/filtrage ; l'interface l'affiche comme correspondance de titre, URL ou texte
- `description` : intention du modèle
- `query` : fragment ajouté après `site:{scope}`

Gardez les nouveaux modèles spécifiques, explicables et faciles à trier. Évitez les termes trop larges qui retournent surtout des pages marketing, politiques ou documentaires.

### Déploiement Et Stockage

C'est une application statique. Elle peut être hébergée via GitHub Pages, un site statique interne ou n'importe quel serveur de fichiers statiques.

Pour les évaluations sensibles, privilégiez une instance locale et évitez analytics, collecte d'erreurs distante ou journaux d'accès capturant les noms de cibles et les termes de requête.

L'application stocke les préférences d'interface, la file et l'historique dans le `localStorage` du navigateur. Effacez ce stockage lorsque les règles d'engagement l'exigent.

## License

Copyright © RedteamNotes. All rights reserved.
