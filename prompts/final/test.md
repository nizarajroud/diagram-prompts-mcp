# AWS Architecture Diagram - Template V2 (Single Placeholder)


## PARAMÈTRES OBLIGATOIRES (NE PAS MODIFIER)

**Configuration Graphviz:**
- `graph_attr["fontsize"]`: "30-35" (taille police titre et étiquettes générales)
- `node_attr["fontsize"]`: "15-18" (taille police libellés des nœuds/services AWS)
- `edge_attr["fontsize"]`: "14-18" (taille police libellés des connexions)
- `graph_attr["dpi"]`: "96" (résolution optimisée pour affichage Word)
- `direction`: "LR" (Left to Right - gauche à droite pour format paysage)
- `node_attr["width"]`: "1.1" (largeur icônes optimisée)
- `node_attr["height"]`: "0.6" (hauteur icônes optimisée)
- `graph_attr["nodesep"]`: "0.6" (espacement vertical entre nœuds)
- `graph_attr["ranksep"]`: "0.8" (espacement horizontal entre couches)
- `graph_attr["pad"]`: "0.5" (marges du diagramme)

**RÈGLE CRITIQUE - TAILLE POLICE DES CLUSTERS:**
- Les titres des Clusters (frames) doivent utiliser `fontsize="15"` en GRAS
- Utiliser `style="bold"` dans les attributs de chaque Cluster
- Ajouter `margin="30"` pour éviter le chevauchement des icônes avec le cadre du Cluster
- Exemple: `with Cluster("AWS Ingestion", graph_attr={"fontsize": "15", "style": "bold", "margin": "30"}):`

**RÈGLE CRITIQUE - LABELS SUR UNE SEULE LIGNE:**
- Tous les labels de nœuds doivent être sur UNE SEULE LIGNE (pas de \n)
- Utiliser UNIQUEMENT le nom du service, sans détails techniques
- Exemples: "Lambda" au lieu de "Lambda validation (10 GB)", "Control-M" au lieu de "Control-M V21-201", "S3" au lieu de "S3 Raw Input"
- Les détails techniques (versions, capacités, configurations) doivent être documentés ailleurs, pas dans les labels

**EXIGENCES DE DIMENSIONNEMENT IMAGE PNG:**
- Ratio d'aspect: 297:210 (1.41:1 - format paysage)
- Résolution: 96 DPI minimum
- Disposition: HORIZONTALE (gauche → droite)
- Tous les composants visibles sans scroll dans Word à 100%

**EXIGENCES VISUELLES:**
- Structure du flux: GAUCHE → DROITE
- Couleurs distinctes par zone fonctionnelle (utiliser Cluster de diagrams)
- Flèches directionnelles pour flux de données
- Icônes AWS standards
- Conformité: AWS Well-Architected Framework

**RESSOURCES PERSONNALISÉES:**
- Vérifier le dossier `my_ressources` pour les icônes/ressources personnalisées
- Utiliser les ressources personnalisées si disponibles pour les services spécifiques
- Importer depuis `my_ressources` en priorité avant les icônes AWS standards

---

## DESCRIPTION DE L'ARCHITECTURE (MODIFIEZ UNIQUEMENT CETTE SECTION)

[COLLEZ ICI VOTRE DESCRIPTION D'ARCHITECTURE COMPLÈTE]

Incluez:
- Objectif du diagramme
- Liste des services AWS par couche/zone
- Flux de données entre les services
- Contraintes techniques (volumétrie, SLA, etc.)
- Toute information pertinente pour générer le diagramme

Exemple de format:

**Objectif**: Créer un diagramme pour [votre cas d'usage]

**Couche 1 - Sources**:
- Service1: description
- Service2: description

**Couche 2 - Ingestion**:
- S3: buckets pour données brutes
- EventBridge: déclenchement des pipelines

**Couche 3 - Traitement**:
- Lambda: traitement léger
- Glue: ETL

[etc...]

---
