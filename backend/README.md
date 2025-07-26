# KLIPZ Backend

API et base de données gérées avec Supabase.

## 🗄️ Configuration Supabase

### **Tables créées**
- `users` - Profils utilisateurs (streamers/clippers)
- `campaigns` - Campagnes de clips
- `submissions` - Soumissions de clips
- `payments` - Historique des paiements

### **Sécurité**
- ✅ Row Level Security (RLS) activé
- ✅ Politiques d'accès définies
- ✅ Authentification par email
- ✅ Validation des données

### **Fonctions automatiques**
- ✅ Mise à jour des timestamps
- ✅ Calcul automatique des gains
- ✅ Création de profils utilisateurs

## 📊 Base de données

### **Schéma principal**
```sql
-- Utilisateurs
users (
  id UUID PRIMARY KEY,
  email TEXT NOT NULL,
  role TEXT CHECK (role IN ('streamer', 'clipper')),
  twitch_url TEXT,
  tiktok_username TEXT,
  balance DECIMAL(10,2) DEFAULT 0.00
)

-- Campagnes
campaigns (
  id UUID PRIMARY KEY,
  streamer_id UUID REFERENCES users(id),
  title TEXT NOT NULL,
  description TEXT NOT NULL,
  criteria JSONB NOT NULL,
  budget DECIMAL(10,2) NOT NULL,
  cpm DECIMAL(10,4) NOT NULL,
  status TEXT DEFAULT 'active'
)

-- Soumissions
submissions (
  id UUID PRIMARY KEY,
  campaign_id UUID REFERENCES campaigns(id),
  clipper_id UUID REFERENCES users(id),
  tiktok_url TEXT NOT NULL,
  status TEXT DEFAULT 'pending',
  views INTEGER DEFAULT 0,
  earnings DECIMAL(10,2) DEFAULT 0.00
)
```

## 💳 Intégration Stripe

### **Fonctionnalités**
- ✅ Paiements par carte
- ✅ Apple Pay / Google Pay
- ✅ Gestion des comptes utilisateurs
- ✅ Webhooks pour les notifications

### **Sécurité**
- ✅ Clés API sécurisées
- ✅ Validation côté serveur
- ✅ Gestion des erreurs
- ✅ Conformité PCI

## 📁 Structure des fichiers

```
backend/
├── supabase/                    # Configuration Supabase
│   ├── config.toml             # Configuration du projet
│   ├── functions/              # Edge Functions
│   │   ├── stripe-create-account/
│   │   ├── stripe-onboarding-link/
│   │   └── stripe-payout/
│   └── migrations/             # Migrations de base de données
├── stripe-database-setup.sql   # Script de configuration Stripe
├── clean-all-test-data.sql     # Nettoyage des données de test
└── clean-database-simple.sql   # Nettoyage simple de la base
```

## 🔧 Configuration

### **1. Configuration Supabase**
1. Créez un projet sur [supabase.com](https://supabase.com)
2. Récupérez vos clés API dans Settings > API
3. Dans Supabase SQL Editor, exécutez les scripts de migration
4. Activez l'authentification par email dans Authentication > Settings

### **2. Configuration Stripe**
1. Créez un compte sur [stripe.com](https://stripe.com)
2. Récupérez vos clés API
3. Exécutez le script `stripe-database-setup.sql`
4. Configurez les webhooks Stripe

## 📄 Documentation

- `STRIPE_SETUP.md` - Guide complet de configuration Stripe
- `SUPABASE_SETUP.md` - Guide de configuration Supabase
- `TIKTOK_SETUP.md` - Configuration TikTok
- `TWITCH_SETUP.md` - Configuration Twitch
- `STRIPE_DEPLOYMENT_GUIDE.md` - Guide de déploiement Stripe

## 🚨 Dépannage

### **Erreurs communes**

1. **"Invalid API key"**
   - Vérifiez vos clés Supabase
   - Assurez-vous que l'URL du projet est correcte

2. **"Row Level Security policy violation"**
   - Vérifiez que l'utilisateur est authentifié
   - Vérifiez les politiques RLS dans Supabase

3. **"Network request failed"**
   - Vérifiez votre connexion internet
   - Vérifiez que Supabase est accessible 