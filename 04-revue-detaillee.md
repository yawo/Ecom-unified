# Revue détaillée des livrables Marp

## Périmètre revu

- `00-synthese-marp.md`
- `01-cadrage-questions-marp.md`
- `02-architecture-cible-marp.md`
- `03-migration-deploiement-marp.md`
- Le brief de référence (`.docx`) et la cartographie macro (`.drawio`) ont été relus pour vérifier l’alignement.

## Résumé exécutif

Les livrables sont globalement solides pour un support de présentation de 30 minutes: structure claire, séparation synthèse/détails, orientation décisionnelle, bonnes bases d’architecture (API-first, event-driven, domaine, migration par vagues).

Les écarts principaux portent sur:

1. l’explicitation des frontières de responsabilité avec les briques existantes;
2. la traçabilité des hypothèses et des non-dits de cadrage;
3. la complétude de certaines exigences non fonctionnelles (sécurité, résilience, données, conformité) avec métriques opérationnelles;
4. le traitement plus concret de l’omnicanal international (variantes locales, gouvernance des dérogations, stratégie de données pays).

## Évaluation par directive

### 1) Rôle « directeur technique »: architecture + présentation

**Constat**
- Le niveau de hauteur est bon: vision cible, principes, arbitrages, migration, déploiement.
- Le format est adapté à un échange avec directeurs de projet (angles décisionnels présents).

**Amélioration recommandée**
- Ajouter une slide « décisions à prendre maintenant » avec 5 décisions irréversibles et leurs impacts.

### 2) Production attendue: un Marp synthèse + plusieurs Marp de détail

**Constat**
- Exigence respectée: 1 fichier de synthèse + 3 fichiers de détail.
- Cohérence globale de plan.

**Amélioration recommandée**
- Ajouter un plan de navigation inter-documents (référence croisée slide 1 de chaque deck).

### 3) Style éditorial

**Constat**
- Thème `marpcore` et format Marp correctement configurés.
- Ton globalement concis.
- Pas d’emoji dans les documents.
- Usage pertinent de diagrammes mermaid.

**Amélioration recommandée**
- Uniformiser la sentence-case dans quelques titres (ex. « KPI », « RACI », « Go/no-go » selon convention éditoriale décidée).

### 4) Appui sur Word et drawio

**Constat**
- Les grands axes du brief Word sont couverts (vision, questions, principes, macro-architecture, migration, déploiement).
- L’existant SI (API gateway, data platform, POS/e-commerce multiples, OMS, référentiels) est repris.

**Amélioration recommandée**
- Ajouter une table de correspondance « Exigence du brief -> slide de réponse » pour éviter toute contestation de couverture.

## Revue architecture

### Forces

- Vision architecture cohérente avec un contexte multi-pays et legacy hétérogène.
- Bonne séparation « edge / core / plateforme / SI cœur ».
- Stratégie de transition réaliste (strangler, anti-corruption, rollback explicite).
- Arbitrages buy vs build orientés valeur et risque.

### Zones à renforcer

1. **Frontières fonctionnelles avec OMS/logistique**
   - Le principe est posé, mais il manque la matrice d’autorité métier par processus (promesse, allocation, préparation, annulation, retour, remboursement).

2. **Mastership des données**
   - Le concept est présent, mais il faut une matrice formelle par objet métier (create/read/update/delete, publication d’événements, SLA de fraîcheur).

3. **Résilience omnicanale**
   - Le POS offline est mentionné dans le brief mais pas transformé en patterns techniques explicites (cache local, journal d’événements local, stratégie de réconciliation).

4. **Sécurité et conformité internationale**
   - Les principes sont cités mais pas déclinés en exigences vérifiables (chiffrement, IAM fédéré, séparation des données personnelles, stratégie de résidence des données par pays).

5. **Pilotage économique**
   - Le FinOps est mentionné; ajouter des garde-fous chiffrés (coût par transaction, coût par pays onboardé, coût de coexistence legacy).

## Revue migration et déploiement

### Forces

- Découpage en horizons clair et pilotable.
- KPI go/no-go utiles et actionnables.
- Bonne prise en compte de la coexistence legacy.

### Risques résiduels

1. **Risque de migration silencieuse longue**
   - Le plan donne des horizons, mais pas de date butoir de retrait par brique.

2. **Risque organisationnel pays**
   - Le RACI est utile; il manque la capacité minimale requise par pays (run, test, data, sécurité).

3. **Risque de dérive de standard**
   - Les variantes locales sont cadrées, mais sans mécanisme formel de « RFC + date d’expiration de dérogation ».

## Questions de cadrage à ajouter en priorité

1. Quel est le niveau de centralisation cible de la tarification en situation de contrainte réglementaire locale?
2. Quelle est l’autorité finale sur la promesse client en cas d’incohérence stock (OMS vs POS vs e-commerce)?
3. Quelles fonctions doivent continuer de fonctionner en mode dégradé magasin offline, et pendant combien de temps?
4. Quelle stratégie de résidence des données personnelles par zone géographique?
5. Quel budget et quelle deadline de décommissionnement pour chaque système legacy critique?

## Recommandations de finalisation des supports

### Recommandation 1: ajouter une matrice de responsabilités

Créer une slide unique « ownership par capacité » avec colonnes: domaine, owner produit, owner technique, système maître, SLA, pays autorisés à déroger.

### Recommandation 2: expliciter les NFR sous forme de contrats

Ajouter une slide « NFR contractuels »:
- performance (p95/p99, volumétrie);
- disponibilité par parcours;
- sécurité (contrôles obligatoires);
- résilience (RTO/RPO par domaine);
- qualité des données (fraîcheur, complétude, unicité).

### Recommandation 3: renforcer la stratégie internationale

Ajouter une slide « global template vs local extension » avec:
- ce qui est strictement global;
- ce qui est local paramétrable;
- le processus d’exception.

### Recommandation 4: solidifier la trajectoire de décommissionnement

Ajouter un tableau « retirement plan » par brique legacy: prérequis, jalon cible, coût de maintien, date de fin.

### Recommandation 5: préparer la discussion de comité

Ajouter une slide finale « 5 décisions à valider en séance » avec options A/B et impacts (délai, coût, risque, autonomie pays).

## Proposition de structure de présentation 30 minutes

- 5 min: contexte, enjeux, ambiguïtés.
- 8 min: vision cible et principes structurants.
- 7 min: architecture macro, buy vs build, responsabilités.
- 7 min: migration, déploiement, risques et parades.
- 3 min: décisions demandées au comité.

## Conclusion

Le matériau est crédible et déjà exploitable. Avec les compléments ci-dessus (ownership explicite, NFR contractuels, internationalisation gouvernée, plan de retrait legacy chiffré), la présentation passera d’un bon dossier d’architecture à un support de décision robuste pour un comité programme international.
