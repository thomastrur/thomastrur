# OmniAI Platform - TODO

## Phase 1 : Recherche & Architecture
- [x] Analyser 100 sites d'IA et identifier les catégories dominantes
- [x] Synthétiser les meilleures pratiques et modèles économiques
- [x] Concevoir l'architecture système et les workflows

## Phase 2 : Structure de Données & Modèle
- [x] Définir le schéma de base de données (utilisateurs, créations, historique)
- [x] Planifier l'intégration des API d'IA gratuites/open-source
- [x] Concevoir les endpoints tRPC pour chaque outil

## Phase 3 : Frontend - Layout & Navigation
- [x] Choisir la direction stylistique (design system, couleurs, typographie)
- [x] Créer le layout principal avec navigation multimodale
- [x] Implémenter la page d'accueil avec présentation des outils
- [x] Créer le système de navigation entre les outils

## Phase 4 : Outils d'IA - Implémentation
- [x] Chat conversationnel avec LLM (texte, code, traduction)
- [x] Génération d'images à partir de descriptions
- [ ] Édition d'images (face swap, suppression de fond, amélioration)
- [x] Génération et édition de vidéos
- [ ] Conversion audio (speech-to-text, text-to-speech)
- [x] Traduction multilingue
- [ ] OCR
- [ ] Interface multimodale pour combiner les outils

## Phase 5 : Galerie & Dashboard
- [x] Système de sauvegarde des créations en base de données
- [x] Galerie personnelle avec filtrage et recherche
- [x] Dashboard utilisateur avec statistiques d'utilisation
- [x] Historique des créations et accès rapide

## Phase 6 : Tests & Déploiement
- [ ] Tests unitaires (vitest) pour les procédures tRPC
- [ ] Tests d'intégration des outils d'IA
- [ ] Optimisations de performance
- [ ] Déploiement et publication


## Changements Demandés
- [ ] Renommer le site en "Tom's IA" partout (titre, navigation, pages)
- [ ] Ajouter le crédit "Créé par Thomas TRUR et généré par Manus IA" dans le footer
- [ ] Mettre à jour les variables d'environnement (VITE_APP_TITLE)

## Interface Admin (Thomas TRUR - m.trurthomas@gmail.com)
- [x] Créer les pages admin avec protection par rôle
- [x] Dashboard admin avec statistiques globales
- [x] Gestion des utilisateurs (liste, modification, suppression)
- [x] Outils d'optimisation de la BDD (nettoyage, archivage)
- [ ] Logs et monitoring des activités
- [x] Gestion des créations (modération, suppression)
- [ ] Configuration système et paramètres


## Bugs à Corriger
- [x] Erreur dans le chat : "Une erreur s'est produite. Veuillez réessayer." (Correction : initialisation Drizzle avec mysql2)
- [ ] Les vidéos ne sont pas générées (endpoint utilise URL placeholder)


## Galerie Personnelle
- [x] Créer la page `/gallery` avec affichage des créations
- [x] Ajouter filtrage par type (chat, image, vidéo, audio, ocr, traduction)
- [x] Ajouter recherche par titre/contenu
- [x] Ajouter système de favoris
- [x] Ajouter suppression de créations
- [ ] Ajouter partage de créations


## Pages à Créer
- [ ] Page Audio (/audio) : Speech-to-text et text-to-speech
- [ ] Page OCR (/ocr) : Extraction de texte depuis images/PDF
