# Wellmum – Infrastructure AWS Automatisée

[![Terraform](https://img.shields.io/badge/Terraform-~1.9-623CE4?logo=terraform)](https://www.terraform.io/)
[![AWS](https://img.shields.io/badge/AWS-Cloud-FF9900?logo=amazon-aws)](https://aws.amazon.com/)
[![GitHub Actions](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-2088FF?logo=github-actions)](https://github.com/features/actions)
[![YouTube](https://img.shields.io/badge/Demo-YouTube-FF0000?logo=youtube)](https://www.youtube.com/watch?v=9DtVrCLJL_M&list=PLWL9Oy30PVmVUCJ74cRK57wmRrugK1-VI)

Automatisation complète d'une infrastructure AWS pour le client Wellmum via **Terraform Cloud** et **GitHub Actions**. Ce repository partage l'expérience et l'implémentation d'un projet d'infrastructure cloud de niveau production.

> 🎥 **[Regarder la playlist de démonstration sur YouTube](https://www.youtube.com/watch?v=9DtVrCLJL_M&list=PLWL9Oy30PVmVUCJ74cRK57wmRrugK1-VI)**

> 🇬🇧 **[English version available here](README.en.md)**

---

## 📋 Table des matières

- [Contexte du projet](#-contexte-du-projet)
- [Architecture](#-architecture)
- [Structure du repository](#-structure-du-repository)
- [Prérequis](#-prérequis)
- [Configuration initiale](#-configuration-initiale)
- [Déploiement de l'infrastructure](#-déploiement-de-linfrastructure)
- [Workflows CI/CD](#-workflows-cicd)
- [Mise à jour de l'infrastructure](#-mise-à-jour-de-linfrastructure)
- [Applications](#-applications)
- [Organisation de l'infrastructure](#-organisation-de-linfrastructure)
- [Bonnes pratiques](#-bonnes-pratiques)

---

## 🎯 Contexte du projet

### Le client : Wellmum

Wellmum avait besoin d'une infrastructure AWS de niveau production avec :

- ✅ **Haute disponibilité** : multi-AZ, load balancing, auto-scaling
- 🔒 **Sécurisée** : IAM, Security Groups, gestion des secrets
- 📈 **Évolutive** : architecture modulaire et scalable
- 🤖 **Entièrement codifiée** : Infrastructure as Code avec Terraform
- 🚀 **Déployée en continu** : CI/CD via GitHub Actions

### La mission

Concevoir, valider et implémenter une architecture AWS complète, puis automatiser son provisioning et le déploiement des applications via des pipelines CI/CD robustes.

### ⚠️ Note importante sur les applications

Les applications présentes dans ce repository (**wellmum-ai**, **wellmum-api**, **wellmum-landing**) sont des **clones simplifiés** basés sur les mêmes technologies que les applications originales du client. Le code source réel n'est pas inclus pour des raisons de **confidentialité**.

Ces clones permettent néanmoins de :
- Démontrer l'architecture complète
- Tester les pipelines de déploiement
- Illustrer l'organisation d'un projet multi-services réel

Cette expérience est partagée via l'initiative DevCloud Challenge à des fins pédagogiques. L'implémentation est abordée de façon plus approfondie dans le cours **[Projets Cloud, DevOps, DevSecOps, Data & AI — Indispensables pour Consultants Informatiques](https://eazytraining.fr/cours/projets-cloud-devops-devsecops-data-ai-indispensables-pour-consultants-informatiques/)** sur EAZYTraining.

---

## 🏗️ Architecture

### Architecture applicative

L'application Wellmum est composée de trois services principaux :

![Architecture applicative Wellmum](architecture%20applicative%20wellmum.drawio.png)

### Infrastructure déployée

L'infrastructure AWS est organisée en plusieurs couches :

#### **Frontend (Landing Page)**
![Infrastructure Frontend](image.png)

#### **Backend (API + Services IA)**
![Infrastructure Backend](image%20(1).png)

### Workflow de provisioning

Le processus de déploiement automatisé suit une séquence précise :

![Workflow provisioning](Worflow%20provisioning.png)

---

## 📁 Structure du repository

```
wellmum/
│
├── .github/
│   └── workflows/              # Pipelines CI/CD GitHub Actions
│       ├── rex-deploy-terraform.yml    # Déploiement infrastructure
│       ├── rex-deploy-api.yml          # Déploiement API
│       ├── rex-deploy-*.yml            # Déploiement services IA
│       └── rex-destroy-*.yml           # Destruction environnements
│
├── wellmum-infra/              # 🏗️ Infrastructure as Code (Terraform)
│   ├── wellmum-network/        # VPC, Subnets, NAT, Internet Gateway
│   ├── wellmum-security/       # IAM, Roles, Secrets Manager, KMS
│   ├── wellmum-stockage/       # EFS, S3, volumes persistants
│   ├── wellmum-cluster/        # ECS Cluster, ECR
│   ├── wellmum-landing/        # Infrastructure Amplify (Frontend)
│   │   ├── dev/                # Environnement développement
│   │   ├── prod/               # Environnement production
│   │   └── modules/            # Modules réutilisables
│   ├── wellmum-api/            # Infrastructure ECS + ALB + RDS (API)
│   │   ├── dev/
│   │   ├── prod/
│   │   └── modules/
│   └── wellmum-ai/             # Infrastructure ECS Services IA
│       ├── dev/
│       ├── prod/
│       └── modules/
│
├── wellmum-api/                # 🔧 Application API (NestJS clone)
│   ├── src/
│   ├── Dockerfile
│   └── docker-compose.yml
│
├── wellmum-ai/                 # 🤖 Microservices IA (FastAPI clones)
│   ├── chat/                   # Service chat IA
│   ├── food_detector/          # Détection aliments + calories
│   ├── nutrition/              # Plans nutritionnels personnalisés
│   ├── routines/               # Routines d'exercices
│   └── social/                 # Modération sociale IA
│
└── wellmum-landing/            # 🌐 Application Frontend (Next.js clone)
    ├── app/
    ├── components/
    └── next.config.ts
```

---

## 🔧 Prérequis

Avant de commencer, assurez-vous d'avoir :

- ✅ Un compte **AWS** avec les permissions nécessaires
- ✅ Un compte **Terraform Cloud** configuré
- ✅ Un compte **GitHub** avec accès au repository
- ✅ **Terraform CLI** version ~1.9 installé localement (optionnel)
- ✅ **Git** installé

### 📚 Cours & Formations recommandés

Pour bien comprendre l'ensemble des implémentations réalisées dans ce projet, les ressources suivantes sont recommandées :

**Cours & Tutos :**
- 🎓 [Devenez AWS Certified Associate Architect et SysOps](https://eazytraining.fr/cours/devenez-aws-certified-associate-architect-et-sysops/)
- 🏗️ [Terraform : les bases](https://eazytraining.fr/cours/terraform-les-bases-pour-devops/)
- 📜 [Terraform : Passez la certification Hashicorp Terraform Associate](https://eazytraining.fr/cours/terraform-passez-la-hashicorp-terraform-associate/)
- 🤖 [Découvrir GitHub Copilot, de l'installation à la productivité globale](https://www.youtube.com/playlist?list=PLWL9Oy30PVmWsA0EP-lRulNW4IUrYL0Hw)

**Bootcamp :**
- 🚀 [BOOTCAMP AWS CLOUD ENGINEER](https://eazytraining.fr/%C3%A9v%C3%A8nement/bootcamp-aws-cloud-engineer/)

---

## ⚙️ Configuration initiale

### Étape 1 : Configuration Terraform Cloud

1. **Créer une organisation** dans Terraform Cloud :
   - Nom suggéré : `REX-WELLMUM-Services-Infrastructure`

2. **Créer les workspaces** suivants :
   ```
   wellmum-network
   wellmum-security
   wellmum-stockage
   wellmum-cluster
   wellmum-landing-dev
   wellmum-landing-prod
   wellmum-api-dev
   wellmum-api-prod
   wellmum-ai-dev
   wellmum-ai-prod
   ```

3. **Générer un API Token** :
   - Aller dans User Settings → Tokens
   - Créer un nouveau token et le copier

### Étape 2 : Configuration des secrets GitHub

Dans votre repository GitHub, aller dans **Settings → Secrets and variables → Actions** et ajouter :

| Secret | Description | Exemple |
|--------|-------------|---------|
| `TF_API_TOKEN` | Token API Terraform Cloud | `xxxxxxxxxxxxx.atlasv1.xxxxx` |
| `AWS_ACCESS_KEY_ID` | Clé d'accès AWS (pour les workflows de déploiement applicatif) | `AKIAXXXXXXXXXXXXXXXX` |
| `AWS_SECRET_ACCESS_KEY` | Clé secrète AWS | `xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx` |

### Étape 3 : Configurer les variables Terraform Cloud

Pour chaque workspace, configurez les variables suivantes :

**Variables AWS (pour tous les workspaces) :**
- `AWS_ACCESS_KEY_ID` (Environment variable, sensitive)
- `AWS_SECRET_ACCESS_KEY` (Environment variable, sensitive)
- `AWS_DEFAULT_REGION` (Environment variable) = `us-east-1` (ou votre région)

**Variables spécifiques (selon le workspace) :**
- Variables de configuration réseau (CIDR, etc.)
- Variables de sécurité (noms de secrets, etc.)
- Variables d'application (tailles d'instance, etc.)

---

## 🚀 Déploiement de l'infrastructure

### Premier déploiement (Provisioning initial)

Le déploiement initial de l'infrastructure se fait automatiquement via **GitHub Actions** en suivant cet ordre :

1. **Déclenchement du workflow** :
   ```bash
   # Option 1 : Push sur la branche main (déploiement production)
   git push origin main
   
   # Option 2 : Push sur la branche test (déploiement dev avec auto-approve)
   git push origin test
   
   # Option 3 : Déclenchement manuel
   # Aller dans Actions → Terraform Infrastructure Deploy → Run workflow
   ```

2. **Séquence de déploiement automatique** :

   Le workflow [.github/workflows/rex-deploy-terraform.yml](.github/workflows/rex-deploy-terraform.yml) déploie l'infrastructure dans cet ordre :

   ```
   1️⃣ Network     (VPC, Subnets, NAT Gateway, Internet Gateway)
          ↓
   2️⃣ Security    (IAM Roles, Security Groups, Secrets Manager)
          ↓
   3️⃣ Stockage    (EFS, S3 Buckets)
          ↓
   4️⃣ Landing     (AWS Amplify pour le frontend)
          ↓
   5️⃣ Cluster     (ECS Cluster + ECR Repositories)
          ↓
   6️⃣ AI Services (ECS Services pour les microservices IA)
          ↓
   7️⃣ API         (ECS Service + ALB + RDS pour l'API)
   ```

3. **Environnements** :
   - **Branche `test`** → Déploiement automatique en environnement **dev**
   - **Branche `main`** → Déploiement en environnement **prod** (nécessite validation manuelle)

---

## 🔄 Workflows CI/CD

### Workflow principal : Infrastructure

**Fichier** : [.github/workflows/rex-deploy-terraform.yml](.github/workflows/rex-deploy-terraform.yml)

**Déclencheurs** :
- Push sur `main` ou `test` avec modifications dans `wellmum-infra/**`
- Pull Request vers `main` ou `test`
- Déclenchement manuel (`workflow_dispatch`)

**Fonctionnalités** :
- ✅ Détection intelligente des changements (déploie uniquement les modules modifiés)
- ✅ Déploiement séquentiel respectant les dépendances
- ✅ Auto-approve sur branche `test` (environnement dev)
- ✅ Validation manuelle sur branche `main` (environnement prod)
- ✅ Gestion d'environnements GitHub (production/testment)

### Workflows de déploiement applicatif

Chaque service dispose de son propre workflow pour le build et le déploiement des images Docker :

- `rex-deploy-api.yml` : Build et push de l'image API vers ECR
- `rex-deploy-chat.yml` : Service de chat IA
- `rex-deploy-food-detector.yml` : Service de détection alimentaire
- `rex-deploy-nutrition.yml` : Service de nutrition
- `rex-deploy-routines.yml` : Service de routines
- `rex-deploy-social.yml` : Service social

### Workflows de destruction

Pour supprimer les environnements :

- `rex-destroy-dev.yml` : Destruction complète de l'environnement dev
- `rex-destroy-prod.yml` : Destruction complète de l'environnement prod
- `rex-destroy-shared.yml` : Destruction de l'infrastructure partagée (network, security, etc.)

---

## 🔄 Mise à jour de l'infrastructure

### Modifications de l'infrastructure

1. **Modifier le code Terraform** dans le dossier concerné :
   ```bash
   # Exemple : modification du réseau
   cd wellmum-infra/wellmum-network
   # Éditer les fichiers .tf
   ```

2. **Commit et push** :
   ```bash
   git add .
   git commit -m "feat: update network configuration"
   git push origin test  # Pour tester en dev d'abord
   ```

3. **Le workflow détecte automatiquement les changements** et ne déploie que les modules modifiés.

4. **Après validation en dev**, merger vers `main` pour déployer en production.

### Pourquoi cette organisation modulaire ?

Consultez [wellmum-infra/structure-dossier.md](wellmum-infra/structure-dossier.md) pour comprendre en détail :

- ✅ **Séparation Core/Application** : Infrastructure de base vs infrastructure applicative
- ✅ **Réutilisabilité** : Les modules Core sont partagés entre les applications
- ✅ **Maintenance facilitée** : Modifications ciblées sans impact global
- ✅ **Scalabilité** : Ajout facile de nouveaux services
- ✅ **Environnements multiples** : Dev et Prod isolés avec la même base de code

---

## 📦 Applications

### Wellmum API

**Technologie** : NestJS (Node.js/TypeScript)  
**Port** : 3000  
**Services** : API REST + Swagger UI  

```bash
cd wellmum-api
docker-compose up --build
```

Endpoints :
- Health Check : `GET /api/healthcheck`
- Documentation : `/api/docs`

### Wellmum AI Services

**Technologie** : FastAPI (Python 3.11)  
**Services** :

| Service | Port | Description |
|---------|------|-------------|
| Chat | 8002 | Interactions chat avec IA |
| Food Detector | 8003 | Détection d'aliments et estimation calorique |
| Nutrition | 8004 | Plans nutritionnels personnalisés |
| Routines | 8005 | Génération de routines d'exercices |
| Social | 8006 | Modération des interactions sociales |

Chaque service expose un endpoint `/healthz` pour le health check.

```bash
cd wellmum-ai/chat
docker-compose up --build
```

### Wellmum Landing

**Technologie** : Next.js (React/TypeScript)  
**Port** : 3000  

```bash
cd wellmum-landing
npm install
npm run dev
```

---

## 🏗️ Organisation de l'infrastructure

### Infrastructure Core (Partagée)

Ces composants sont **indépendants des applications** et constituent la fondation :

| Module | Responsabilité |
|--------|----------------|
| **wellmum-network** | VPC, Subnets (publics/privés), NAT Gateway, Internet Gateway, Routes, ACL |
| **wellmum-security** | Rôles IAM, Politiques, Security Groups, Secrets Manager, KMS |
| **wellmum-stockage** | EFS (stockage partagé), S3 Buckets, configurations de volumes |
| **wellmum-cluster** | ECS Cluster, ECR Repositories, configuration du cluster |

### Infrastructure Application (Spécifique)

Ces modules **consomment le Core** et ajoutent l'infrastructure nécessaire à chaque application :

| Module | Structure | Responsabilité |
|--------|-----------|----------------|
| **wellmum-landing** | `dev/`, `prod/`, `modules/` | AWS Amplify, configuration frontend |
| **wellmum-api** | `dev/`, `prod/`, `modules/` | ECS Services, ALB, Target Groups, RDS (PostgreSQL) |
| **wellmum-ai** | `dev/`, `prod/`, `modules/` | ECS Services pour les 5 microservices IA |

### Flux de déploiement

```
Core Infrastructure (1-4)
         ↓
Application Infrastructure (5-7)
         ↓
Application Deployment (Docker Images)
```

---

## ✅ Bonnes pratiques

### Infrastructure as Code

- ✅ **Code modulaire** : Réutilisation maximale via modules Terraform
- ✅ **État distant** : Terraform Cloud pour la gestion de l'état
- ✅ **Workspaces** : Isolation dev/prod
- ✅ **Variables** : Configuration externalisée et sécurisée

### CI/CD

- ✅ **Déploiements incrémentaux** : Détection des changements pour optimiser les builds
- ✅ **Validation manuelle** : Protection de la production
- ✅ **Auto-approve** : Accélération en développement
- ✅ **Rollback** : Workflows de destruction pour nettoyer les environnements

### Sécurité

- ✅ **Secrets managés** : AWS Secrets Manager + GitHub Secrets
- ✅ **IAM Roles** : Moindre privilège
- ✅ **Security Groups** : Segmentation réseau stricte

### Observabilité

- ✅ **Health Checks** : Tous les services exposent des endpoints de santé
- ✅ **Logs** : CloudWatch Logs pour le monitoring
- ✅ **Métriques** : CloudWatch Metrics + Auto Scaling

---

## 🎓 Ce que vous apprendrez

En explorant ce repository, vous maîtriserez :

1. **Conception d'architecture cloud** adaptée aux besoins métier
2. **Infrastructure as Code** avec Terraform et bonnes pratiques
3. **Terraform Cloud** : workspaces, état distant, collaboration
4. **CI/CD** avec GitHub Actions pour infrastructure et applications
5. **Organisation projet** : séparation Core/Application, modules réutilisables
6. **Sécurité AWS** : IAM, Security Groups, Secrets Management
7. **Conteneurisation** : Docker, ECS, ECR
8. **Multi-environnements** : Gestion Dev/Prod avec le même code

---

## 🎥 Vidéos de démonstration

Regardez la playlist complète présentant le déploiement et l'architecture :

**[▶️ Playlist de démonstration Wellmum Infrastructure](https://www.youtube.com/watch?v=9DtVrCLJL_M&list=PLWL9Oy30PVmVUCJ74cRK57wmRrugK1-VI)**

---

## 📝 Licence

Ce projet est sous licence MIT. Voir le fichier [LICENSE](LICENSE) pour plus de détails.

---

## 🙏 Remerciements

Projet réel réalisé pour le client Wellmum. Cette expérience est partagée via l'initiative DevCloud Challenge à des fins éducatives et de partage de connaissances.

> 📚 **L'implémentation de ce projet est davantage détaillée dans le cadre du cours EAZYTraining** : **[Projets Cloud, DevOps, DevSecOps, Data & AI — Indispensables pour Consultants Informatiques](https://eazytraining.fr/cours/projets-cloud-devops-devsecops-data-ai-indispensables-pour-consultants-informatiques/)**

---

**⚠️ Rappel** : Les applications présentes sont des clones pédagogiques. Le code source réel du client n'est pas inclus pour des raisons de confidentialité.
