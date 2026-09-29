# Document de cadrage

## Automatisation du reporting e-commerce B2B

| Élément | Cadrage initial |
|---|---|
| Projet | Collecte, consolidation et diffusion de statistiques commerciales |
| Périmètre | Exports de la plateforme e-commerce B2B, fichiers Excel et présentation PowerPoint |
| Cadence cible | Hebdomadaire ou mensuelle, à confirmer |
| Version | V0.1 – base de discussion |

## 1. Objet du document

Ce document définit le périmètre, les objectifs et les principes de conception d’une chaîne automatisée de reporting pour une plateforme e-commerce B2B. La chaîne doit récupérer les fichiers disponibles, les compiler dans un référentiel exploitable, calculer les indicateurs retenus et générer une présentation PowerPoint prête à être revue et partagée.

Le cadrage sert de base de validation entre les équipes métier, les équipes techniques et les utilisateurs du reporting. Les éléments dépendant de la plateforme ou de règles métier non encore confirmées apparaissent comme hypothèses ou décisions à prendre.

## 2. Objectifs et résultats attendus

| Objectif | Résultat attendu |
|---|---|
| Réduire le travail manuel | Limiter les téléchargements, copier-coller et retraitements récurrents. |
| Fiabiliser les chiffres | Appliquer des règles communes de nettoyage, de calcul et de contrôle. |
| Accélérer la diffusion | Produire un fichier Excel consolidé et un PowerPoint selon une cadence définie. |
| Améliorer la lecture | Présenter les tendances, écarts et contributions par les axes utiles au pilotage. |
| Tracer les traitements | Conserver les sources, la date de traitement, les contrôles et les erreurs rencontrées. |

## 3. Périmètre

### 3.1 Inclus dans le périmètre

- Récupération des exports de la plateforme e-commerce ou d’un emplacement partagé.
- Archivage des fichiers sources par période de reporting.
- Contrôle du nommage, de la présence des colonnes et de la période couverte.
- Normalisation des formats de dates, montants, devises, statuts et identifiants.
- Consolidation dans un classeur de référence avec une vue de synthèse et des données détaillées.
- Calcul des KPI validés par le métier.
- Génération d’une présentation PowerPoint à partir d’un modèle ou d’une charte définie.
- Journalisation des succès, alertes et erreurs.

### 3.2 Hors périmètre initial

- Modification des données dans la plateforme e-commerce.
- Mise en place d’un data warehouse complet ou d’un outil BI d’entreprise.
- Prévision automatique ou recommandation commerciale avancée.
- Remplacement des règles de gestion non validées par les responsables métier.

## 4. Utilisateurs et usages

| Profil | Usage principal | Niveau de détail |
|---|---|---|
| Direction / comité de pilotage | Suivre la performance et les évolutions. | Synthèse, tendances et alertes |
| Équipe commerciale | Analyser clients, commandes et portefeuille. | Client, commercial, segment |
| Marketing / e-commerce | Comprendre produits, catégories et comportement d’achat. | Produit, catégorie, période |
| Finance / contrôle | Contrôler les montants et les rapprochements. | Détail transactionnel et contrôles |

## 5. Données et sources

Le dispositif devra commencer par un inventaire des exports réellement disponibles. Chaque source sera décrite par son propriétaire, sa fréquence, son format, sa granularité, ses clés et ses règles de qualité.

| Source à confirmer | Données probables | Points de contrôle |
|---|---|---|
| Commandes | Numéro, date, client, statut, montant, devise | Doublons, statuts exclus, période |
| Lignes de commande | Produit, quantité, prix, remise, catégorie | Clés de rattachement, unités, montants |
| Clients / comptes | Compte B2B, segment, région, commercial | Identifiants stables, clients actifs |
| Catalogue | SKU, libellé, catégorie, prix, disponibilité | SKU uniques, changements de référentiel |
| Trafic ou conversion | Sessions, demandes, conversions | Définition et couverture de la source |

## 6. Indicateurs proposés

La liste ci-dessous constitue une base de discussion. Un KPI ne sera retenu que si sa définition, sa source, sa période et son mode d’agrégation sont validés.

| Famille | Indicateurs de base | Axes d’analyse |
|---|---|---|
| Ventes | CA HT, commandes, unités, panier moyen | Période, client, région, commercial |
| Clients | Clients actifs, nouveaux, récurrents, réactivation | Segment, compte, période |
| Produits | CA, unités, prix moyen, contribution | SKU, catégorie, marque |
| Performance | Variation vs période précédente, contribution à la variation | Période, segment, produit |
| Qualité opérationnelle | Annulations, lignes indisponibles, commandes incomplètes | Statut, produit, client |
| Conversion | Taux de conversion ou demandes transformées, si disponible | Canal, période, segment |

## 7. Processus cible

Le processus cible suit une chaîne contrôlée, de la source jusqu’au support de présentation :

| Étape | Traitement | Sortie |
|---|---|---|
| 1. Déclenchement | Lancement planifié ou manuel avec une période de référence. | Identifiant de traitement |
| 2. Collecte | Téléchargement ou lecture des fichiers sources. | Fichiers bruts archivés |
| 3. Contrôles d’entrée | Présence des fichiers, structure, période et taille minimale. | Statut de contrôle |
| 4. Préparation | Nettoyage, typage, dédoublonnage et mapping des référentiels. | Tables normalisées |
| 5. Calcul | Agrégations KPI et comparaisons temporelles. | Dataset de reporting |
| 6. Production | Génération du classeur et du PowerPoint. | Fichiers livrables |
| 7. Diffusion | Dépôt dans un emplacement défini et notification. | Rapport disponible |

## 8. Architecture fonctionnelle cible

L’architecture doit séparer les données brutes, les règles de transformation, les résultats et les supports de diffusion. Cette séparation facilite les contrôles, le dépannage et l’évolution des KPI.

- **Zone Sources** : fichiers reçus, horodatés et conservés sans modification.
- **Zone Préparation** : données nettoyées, référentiels et règles de mapping.
- **Zone Reporting** : tables consolidées, KPI et contrôles de cohérence.
- **Zone Présentation** : génération du PowerPoint à partir des résultats validés.
- **Zone Journal** : exécutions, durées, anomalies, fichiers produits et statut final.

## 9. Contrôles et règles de qualité

| Contrôle | Exemple de règle | Action en cas d’échec |
|---|---|---|
| Complétude | Tous les fichiers attendus sont présents. | Bloquer la production et alerter. |
| Structure | Les colonnes obligatoires existent et portent le bon type. | Mettre le fichier en quarantaine. |
| Unicité | Un numéro de commande respecte la clé attendue. | Signaler les doublons et exclure selon règle validée. |
| Période | Les dates couvrent la période demandée. | Marquer le rapport incomplet. |
| Rapprochement | Le total consolidé rejoint le total source à tolérance définie. | Afficher l’écart et demander une revue. |

## 10. Livrables

| Livrable | Contenu attendu | Fréquence |
|---|---|---|
| Classeur consolidé | Synthèse, données préparées, contrôles et sources référencées. | À chaque exécution |
| Présentation PowerPoint | Vue exécutive, tendances, contributions, alertes et annexes utiles. | À chaque exécution |
| Journal de traitement | Date, période, statut, anomalies, volumes et liens vers les fichiers. | À chaque exécution |
| Documentation d’exploitation | Procédure de lancement, règles KPI, reprise sur erreur et contacts. | À la mise en service |

## 11. Organisation et responsabilités

| Rôle | Responsabilités |
|---|---|
| Sponsor métier | Valider les objectifs, arbitrer les priorités et accepter le résultat. |
| Référent reporting | Définir les KPI, valider les chiffres et la structure du PowerPoint. |
| Référent plateforme | Documenter les exports, accès et changements de format. |
| Réalisation technique | Développer le pipeline, les contrôles, la génération et la supervision. |
| Utilisateurs clés | Tester les résultats sur des cas réels et signaler les écarts. |

## 12. Planning indicatif

| Phase | Contenu | Jalon |
|---|---|---|
| Cadrage détaillé | Sources, KPI, règles, modèle PowerPoint et critères de recette. | Cadrage validé |
| Prototype | Un périmètre source, quelques KPI et une première slide de synthèse. | Prototype revu |
| Construction | Consolidation, contrôles, génération complète et journalisation. | Version testable |
| Recette | Comparaison avec le reporting manuel sur plusieurs périodes. | Recette signée |
| Mise en service | Planification, documentation, transfert et suivi renforcé. | Première exécution récurrente |

## 13. Risques et mesures de maîtrise

| Risque | Impact | Mesure de maîtrise |
|---|---|---|
| Format d’export modifié | Échec ou chiffres incomplets. | Contrôles de schéma et alerte explicite. |
| Définitions KPI ambiguës | Résultats contestés. | Fiche de définition avec exemple et propriétaire. |
| Identifiants clients ou produits instables | Rupture des historiques. | Référentiel de correspondance et suivi des changements. |
| Données tardives ou corrigées | Rapport différent après diffusion. | Date de fraîcheur, versionnement et procédure de retraitement. |
| Accès ou secrets expirés | Collecte impossible. | Gestion sécurisée des accès et test périodique. |

## 14. Décisions à prendre

- Quelle est la plateforme e-commerce et quel mode d’accès est autorisé : API, export, SFTP, dossier partagé ou téléchargement automatisé ?
- Quelle est la cadence de publication et quelle période doit servir de comparaison ?
- Quels KPI sont obligatoires pour la première version ?
- Quel est le modèle PowerPoint, le public cible et le nombre de slides attendu ?
- Où les fichiers sources et livrables doivent-ils être stockés ?
- Qui valide les chiffres et qui reçoit les alertes ?
- Quelle tolérance de rapprochement est acceptable pour les contrôles ?

## 15. Critères de réussite

- Le traitement se lance selon la cadence définie sans manipulation récurrente non documentée.
- Les fichiers attendus sont collectés, archivés et contrôlés.
- Les KPI du rapport sont reproductibles et rapprochés des sources.
- Le PowerPoint est généré avec une mise en page stable et des données à jour.
- Les erreurs sont visibles, compréhensibles et actionnables.
- Un utilisateur habilité peut relancer le traitement et retrouver les fichiers produits.

## 16. Actions complémentaires recommandées

### 16.1 Mettre en place un dictionnaire de données

Documenter chaque champ source avec son type, sa définition métier, son propriétaire, ses règles de qualité et son historique de modification. Ce dictionnaire facilitera les évolutions de format et évitera les interprétations différentes entre les équipes.

### 16.2 Prévoir la gestion des exceptions

Définir un workflow pour les fichiers manquants, les erreurs de format, les écarts de rapprochement et les relances. Chaque exception devra avoir un responsable, un délai de traitement, un niveau de criticité et une règle claire pour bloquer ou poursuivre la production du rapport.

### 16.3 Tester le reporting sur l’historique

Exécuter le prototype sur plusieurs périodes passées et comparer les résultats automatisés au reporting manuel. Cette recette permettra de mesurer les écarts, de vérifier les règles métier et de valider la fiabilité des KPI avant la mise en service récurrente.

## Annexe A – Fiche de définition KPI à compléter

| Champ | À renseigner |
|---|---|
| Nom du KPI | |
| Définition métier | |
| Formule | |
| Source et colonnes | |
| Période et grain | |
| Filtres et statuts exclus | |
| Unité et devise | |
| Propriétaire de la définition | |
| Tolérance / contrôle | |
