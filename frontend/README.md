# KLIPZ Frontend

Application mobile/web construite avec React Native et Expo.

## 🚀 Installation et démarrage

### Prérequis
- Node.js 18+
- Expo CLI
- Compte Supabase (gratuit)
- Compte Stripe (pour les paiements)

### Installation

```bash
cd frontend
npm install
```

### Configuration

1. **Configuration Supabase**
   - Créez un projet sur [supabase.com](https://supabase.com)
   - Récupérez vos clés API dans Settings > API
   - Modifiez `src/config/supabase.ts` avec vos clés

2. **Configuration Stripe** (optionnel)
   - Créez un compte sur [stripe.com](https://stripe.com)
   - Récupérez vos clés API
   - Modifiez `src/config/stripe.ts` avec vos clés

### Démarrage

```bash
npm run start
```

Scannez le QR code avec Expo Go sur votre téléphone.

## 📱 Fonctionnalités

### **Pour les Streamers**
- ✅ Création de campagnes avec budget et critères
- ✅ Gestion des soumissions de clips
- ✅ Suivi des performances et dépenses
- ✅ Paiements sécurisés via Stripe

### **Pour les Clippers**
- ✅ Découverte de campagnes actives
- ✅ Soumission de clips TikTok
- ✅ Suivi des gains et paiements
- ✅ Validation automatique des vues

## 🏗️ Architecture

### **Structure des dossiers**
```
src/
├── components/          # Composants réutilisables
├── config/             # Configuration (Supabase, Stripe)
├── constants/          # Constantes (couleurs, tailles)
├── navigation/         # Navigation React Navigation
├── screens/            # Écrans de l'application
├── services/           # Services (auth, campaigns, payments)
└── types/              # Types TypeScript
```

### **Services principaux**
- `authService` - Authentification Supabase
- `campaignService` - Gestion des campagnes
- `stripeService` - Paiements Stripe

## 🔧 Scripts disponibles

```bash
npm start          # Lancer l'application
npm run android    # Lancer sur Android
npm run ios        # Lancer sur iOS
npm run web        # Lancer en mode web
```

## 📄 Documentation

Voir les fichiers de documentation dans le dossier `backend/` pour la configuration des services. 