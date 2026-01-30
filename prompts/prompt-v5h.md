**Objectif**: Créer un diagramme d'architecture AWS pour la modernisation du système CDBAC de la Banque Nationale du Canada.


**Paramètres OBLIGATOIRES:**
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

**COUCHE 1 - SOURCES DE DONNÉES (On-Premise/Externe)**

Composants externes:
- AS400 (Mainframe) transmettant via MFT: fichiers Sidecar, Position Murex, Réconciliation DAS (volumétrie: 4.5+ GB par fichier)
- SIS OSS (Système source) envoyant fichiers TIF directement (SLA: 23h00)
- Control-M V21-201 (déjà sur AWS) orchestrant les traitements quotidiens (22h-03h et 06h-09h)

Connectivité: AWS Direct Connect ou VPN Site-to-Site entre on-premise et AWS

**COUCHE 2 - INGESTION (Landing Zone AWS)**

Amazon S3 avec buckets structurés:
- s3://cdbac-raw-input/ (zone d'atterrissage brute avec sous-dossiers /tif-files/ et /as400-files/, lifecycle vers S3 Intelligent-Tiering après 30 jours)
- s3://cdbac-processed/ (fichiers transformés)
- s3://cdbac-archive/ (archivage S3 Glacier)

AWS Transfer Family: endpoint SFTP pour réception AS400, intégration S3

Amazon EventBridge: déclenchement sur S3 PutObject, orchestration pipeline, intégration Control-M

**COUCHE 3 - TRANSFORMATION (ETL)**

AWS Glue:
- Glue Data Catalog (schémas TIF, métadonnées AS400)
- Glue Jobs PySpark/Python (6 jobs principaux: TIF-Loader, AS400-Sidecar-Processing, Murex-Position-Processing, DAS-Reconciliation, GL-Transactions-Generation, Balance-Calculations)
- Migration de 150 scripts Shell vers Python

AWS Lambda: validation fichiers, calculs légers, notifications (configuration: 10GB RAM, timeout 15 min)

AWS Step Functions: orchestration workflows complexes, gestion dépendances, retry logic

**COUCHE 4 - STOCKAGE DE DONNÉES**

Amazon RDS for SQL Server (option principale):
- Configuration Multi-AZ haute disponibilité
- Instance: db.r6i.4xlarge minimum
- Storage: 1TB initial (croissance 20%/an)
- Backups automatiques: rétention 7-35 jours
- Read Replicas pour reporting

OU Amazon Aurora PostgreSQL (alternative):
- Cluster avec autoscaling
- Aurora Serverless v2

AWS DMS: migration Sybase → RDS SQL Server avec CDC

AWS Secrets Manager: gestion credentials avec rotation automatique

**COUCHE 5 - DISTRIBUTION (Output)**

Amazon S3 - Buckets de sortie:
- s3://cdbac-output-midas/
- s3://cdbac-output-dwh/
- s3://cdbac-output-smartstream/
- s3://cdbac-output-geac/
- s3://cdbac-output-sap/

AWS Lambda: connecteurs par système consommateur avec conversion format

Amazon SNS: notifications succès/échec, alertes SLA

**COUCHE 6 - OBSERVABILITÉ**

Amazon CloudWatch:
- Logs centralisés (Glue, Lambda, RDS)
- Métriques custom SLA
- Dashboards: volume fichiers, durée traitements, erreurs, capacité RDS

AWS CloudTrail: audit trail complet, conformité bancaire

CloudWatch Alarms: SLA TIF (23h00), SLA AS400 (01h00), échecs fichiers 4.5GB+, capacité RDS >80%

**COUCHE 7 - SÉCURITÉ**

Amazon VPC: VPC dédié, subnets privés (RDS/Glue), subnets publics (endpoints), Security Groups par couche

AWS IAM: rôles par service, principe moindre privilège

AWS KMS: encryption at rest (S3, RDS, EBS) et in transit (TLS/SSL), clés managées client

AWS WAF (si API Gateway): protection endpoints, rate limiting

**COUCHE 8 - INFRASTRUCTURE AS CODE**

AWS CloudFormation ou Terraform: définition infrastructure complète, environnements DEV/TEST/PROD

AWS CodePipeline + CodeBuild: CI/CD Glue jobs, tests automatisés

**CONTRAINTES TECHNIQUES**

Volumétrie:
- 15 fichiers/jour (lundi-vendredi)
- Fichiers jusqu'à 4.5+ GB
- 25 GB/jour, 6.6 TB/an
- Croissance: 20% annuelle

Fenêtres traitement:
- 22h00-04h00 (SLA TIF 23h00)
- 06h00-11h00 (SLA AS400 01h00)

Environnements:
- Production: ~430 GB
- Test: 130-215 GB
- Développement: 43-86 GB

**EXIGENCES DE DIMENSIONNEMENT IMAGE PNG**

Contraintes pour format A4 paysage à 100% zoom dans Word:
- Ratio d'aspect: 297:210 (1.41:1 - format paysage)
- Résolution: 96 DPI minimum
- Disposition: HORIZONTALE (gauche → droite)
- Tous les composants visibles sans scroll

**EXIGENCES VISUELLES**

Structure du flux (GAUCHE → DROITE):
- Zone 1 (GAUCHE): Sources on-premise (AS400, SIS OSS, Control-M)
- Zone 2: Ingestion AWS (S3, Transfer Family, EventBridge)
- Zone 3 (CENTRE): Transformation (Glue, Lambda, Step Functions)
- Zone 4: Stockage (RDS/Aurora, DMS, Secrets Manager)
- Zone 5 (DROITE): Distribution (S3 outputs, Lambda, SNS)
- Zones transversales: Sécurité, Observabilité, IaC

Éléments visuels:
- Couleurs distinctes par zone fonctionnelle (utiliser Cluster de diagrams)
- Flèches directionnelles pour flux de données
- Icônes AWS standards
- Annotations capacités critiques (4.5GB, SLA)

**CONFORMITÉ**: AWS Well-Architected Framework

---
