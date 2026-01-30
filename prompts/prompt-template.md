# AWS Architecture Diagram - Template

**Objectif**: [DÉCRIVEZ VOTRE OBJECTIF ICI - Ex: Créer un diagramme d'architecture AWS pour...]

---

## PARAMÈTRES OBLIGATOIRES

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

---

## ARCHITECTURE À CRÉER

[DÉCRIVEZ VOTRE ARCHITECTURE ICI - Remplacez les sections suivantes par votre contenu]

### COUCHE 1 - [NOM DE LA COUCHE]

[Décrivez les composants de cette couche]

Exemples:
- Service AWS 1: [description et détails]
- Service AWS 2: [description et détails]
- Connectivité: [détails de connexion]

### COUCHE 2 - [NOM DE LA COUCHE]

[Décrivez les composants de cette couche]

### COUCHE 3 - [NOM DE LA COUCHE]

[Décrivez les composants de cette couche]

[Ajoutez autant de couches que nécessaire...]

---

## CONTRAINTES TECHNIQUES (Optionnel)

[Ajoutez vos contraintes spécifiques si applicable]

Exemples:
- Volumétrie: [détails]
- Fenêtres de traitement: [détails]
- Environnements: [détails]
- Performance: [détails]
- SLA: [détails]

---

## EXIGENCES DE DIMENSIONNEMENT IMAGE PNG

Contraintes pour format A4 paysage à 100% zoom dans Word:
- Ratio d'aspect: 297:210 (1.41:1 - format paysage)
- Résolution: 96 DPI minimum
- Disposition: HORIZONTALE (gauche → droite)
- Tous les composants visibles sans scroll

---

## EXIGENCES VISUELLES

Structure du flux (GAUCHE → DROITE):
- Zone 1 (GAUCHE): [Décrivez la zone source/entrée]
- Zone 2: [Décrivez la zone d'ingestion]
- Zone 3 (CENTRE): [Décrivez la zone de traitement/transformation]
- Zone 4: [Décrivez la zone de stockage]
- Zone 5 (DROITE): [Décrivez la zone de sortie/distribution]
- Zones transversales: [Sécurité, Observabilité, IaC, etc.]

Éléments visuels:
- Couleurs distinctes par zone fonctionnelle (utiliser Cluster de diagrams)
- Flèches directionnelles pour flux de données
- Icônes AWS standards
- Annotations pour éléments critiques (si nécessaire)

---

## CONFORMITÉ

AWS Well-Architected Framework

---

## INSTRUCTIONS D'UTILISATION

1. Remplacez `[DÉCRIVEZ VOTRE OBJECTIF ICI]` par votre objectif spécifique
2. Remplacez les sections `[NOM DE LA COUCHE]` par vos couches d'architecture
3. Décrivez chaque composant AWS et ses interactions dans chaque couche
4. Ajoutez vos contraintes techniques spécifiques dans la section appropriée
5. Adaptez la structure du flux selon votre architecture
6. Conservez TOUS les paramètres de configuration (tailles de police, DPI, espacements, etc.)
7. Respectez les règles critiques pour les labels et les clusters
