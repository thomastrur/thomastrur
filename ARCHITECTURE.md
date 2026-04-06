# Architecture OmniAI Platform

## Vue d'ensemble du système

OmniAI est une plateforme multimodale tout-en-un qui centralise les meilleurs outils d'IA gratuits. L'architecture suit un modèle client-serveur avec authentification OAuth, base de données persistante et intégration d'API externes.

## Stack Technique

**Frontend :**
- React 19 avec TypeScript
- Tailwind CSS 4 pour le design responsive
- tRPC pour la communication type-safe avec le backend
- Wouter pour le routage côté client

**Backend :**
- Express 4 avec Node.js
- tRPC 11 pour les procédures RPC
- Drizzle ORM pour l'accès à la base de données
- MySQL/TiDB pour la persistance

**Authentification :**
- OAuth Manus intégré
- Sessions basées sur cookies JWT

**Intégrations IA :**
- Llama 3 / Qwen 3 (LLM via API)
- Stable Diffusion (génération d'images)
- Whisper (transcription audio)
- Deepgram (text-to-speech)
- Replicate API (vidéo)

## Schéma de Base de Données

```sql
-- Utilisateurs (géré par OAuth)
users
├── id (PK)
├── openId (unique)
├── name
├── email
├── role (user | admin)
├── createdAt
├── updatedAt
└── lastSignedIn

-- Créations utilisateur
creations
├── id (PK)
├── userId (FK → users)
├── type (chat | image | video | audio | ocr | translation)
├── title
├── description
├── input (prompt ou contenu original)
├── output (résultat généré)
├── metadata (JSON: dimensions, durée, langue, etc.)
├── storageUrl (URL S3 si applicable)
├── createdAt
└── updatedAt

-- Historique de chat
chat_messages
├── id (PK)
├── userId (FK → users)
├── conversationId
├── role (user | assistant)
├── content
├── createdAt

-- Galerie personnelle
gallery_items
├── id (PK)
├── userId (FK → users)
├── creationId (FK → creations)
├── tags (JSON array)
├── isFavorite
├── viewCount
└── createdAt

-- Statistiques utilisateur
user_stats
├── id (PK)
├── userId (FK → users)
├── totalCreations
├── creationsByType (JSON)
├── lastActivityAt
└── updatedAt
```

## Architecture des Endpoints tRPC

```
/api/trpc/
├── auth/
│   ├── me (GET current user)
│   └── logout (POST)
├── chat/
│   ├── sendMessage (POST)
│   ├── getHistory (GET)
│   └── clearHistory (DELETE)
├── images/
│   ├── generate (POST)
│   ├── edit (POST)
│   └── getHistory (GET)
├── video/
│   ├── generate (POST)
│   ├── getStatus (GET)
│   └── getHistory (GET)
├── audio/
│   ├── transcribe (POST)
│   ├── textToSpeech (POST)
│   └── getHistory (GET)
├── ocr/
│   ├── extractText (POST)
│   └── getHistory (GET)
├── translation/
│   ├── translate (POST)
│   └── getHistory (GET)
├── gallery/
│   ├── listCreations (GET)
│   ├── getCreation (GET)
│   ├── saveCreation (POST)
│   ├── deleteCreation (DELETE)
│   ├── toggleFavorite (POST)
│   └── search (GET)
└── dashboard/
    ├── getStats (GET)
    ├── getRecentCreations (GET)
    └── getUsageChart (GET)
```

## Flux de Données

### 1. Chat Conversationnel
```
User Input → Frontend → tRPC (chat.sendMessage) 
→ Backend (invokeLLM) → LLM API → Response 
→ Save to DB → Return to Frontend → Display
```

### 2. Génération d'Images
```
Prompt → Frontend → tRPC (images.generate) 
→ Backend (Stable Diffusion API) → Image URL 
→ Upload to S3 → Save metadata to DB → Return URL
```

### 3. Transcription Audio
```
Audio File → Frontend → Upload to S3 
→ tRPC (audio.transcribe) → Whisper API 
→ Transcription Text → Save to DB → Return Text
```

### 4. Galerie Personnelle
```
User clicks "Save" → tRPC (gallery.saveCreation) 
→ Create entry in DB → Link to creation 
→ Update gallery view
```

## Sécurité

- **Authentification** : OAuth Manus avec sessions JWT
- **Autorisation** : Vérification userId pour chaque opération
- **Rate Limiting** : Limiter les appels API par utilisateur
- **CORS** : Configuration stricte pour les origines autorisées
- **Validation** : Zod pour valider les inputs utilisateur

## Performance

- **Caching** : Cache Redis pour les requêtes fréquentes
- **Lazy Loading** : Galerie avec pagination
- **Compression** : Gzip pour les réponses API
- **CDN** : S3 avec CloudFront pour les fichiers statiques

## Déploiement

- **Frontend** : Vite build → S3 + CloudFront
- **Backend** : Node.js sur serveur Manus
- **Base de Données** : MySQL managé (TiDB)
- **Stockage** : S3 pour les fichiers générés

## Roadmap des Fonctionnalités

### Phase 1 (MVP)
- ✓ Authentification OAuth
- ✓ Chat conversationnel
- ✓ Génération d'images basique
- ✓ Galerie simple

### Phase 2
- Édition d'images avancée (face swap, background removal)
- Génération de vidéos
- Transcription audio
- OCR

### Phase 3
- Traduction multilingue
- Text-to-speech
- Workflows multimodaux avancés
- Partage de créations

### Phase 4
- Modèles personnalisés
- Fine-tuning
- API publique pour intégrations tierces
- Monétisation premium
