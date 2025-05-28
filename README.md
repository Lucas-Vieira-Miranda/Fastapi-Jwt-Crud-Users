# FastAPI JWT CRUD Users

Projet backend développé avec **FastAPI**, offrant une API REST sécurisée par **JWT** pour gérer une base d'utilisateurs avec les opérations CRUD classiques (Create, Read, Update, Delete).  
La base de données utilisée est **PostgreSQL**. Le projet est entièrement **dockerisé** avec Docker et Docker Compose.

---

## 🚀 Fonctionnalités

- Authentification sécurisée par JWT (JSON Web Tokens)
- CRUD complet sur les utilisateurs (création, lecture, mise à jour, suppression)
- Stockage des utilisateurs dans une base PostgreSQL
- Hashage des mots de passe avec `bcrypt`
- Documentation interactive automatique via Swagger UI (`/docs`)
- Dockerisation complète pour un déploiement facile
- Variables d’environnement configurables via `.env`

---

## 📦 Stack technique

- Python 3.11
- FastAPI
- PostgreSQL
- SQLAlchemy (ORM)
- JWT avec `python-jose`
- `passlib` pour le hashage des mots de passe
- Docker & Docker Compose

---

## 📋 Prérequis

- Docker et Docker Compose installés sur ta machine
- (Optionnel) un client HTTP comme Postman ou curl pour tester l’API

---

## ⚙️ Installation et lancement

1. **Cloner le dépôt**  
```bash
git clone https://github.com/tonpseudo/fastapi-jwt-crud-users.git
cd fastapi-jwt-crud-users
```

2. **Configurer les variables d’environnement**  
Copie `.env.example` en `.env` et modifie si besoin (ex: clé secrète JWT)  
```bash
cp .env.example .env
```

3. **Lancer la stack Docker**  
```bash
docker-compose up --build
```

4. L’API est maintenant disponible à l’adresse :  
```
http://localhost:8000
```

5. Tu peux accéder à la documentation interactive Swagger UI ici :  
```
http://localhost:8000/docs
```

---

## 🔐 Authentification

### Obtenir un token d’accès

- Endpoint : `POST /token`  
- Paramètres (form data) :  
  - `username`  
  - `password`

**Exemple curl** :  
```bash
curl -X POST "http://localhost:8000/token" -d "username=tonuser&password=tonmdp"
```

Réponse :  
```json
{
  "access_token": "<ton_token_jwt>",
  "token_type": "bearer"
}
```

---

## 📚 Endpoints utilisateurs (protégés par JWT)

Tu dois inclure dans l’en-tête HTTP `Authorization: Bearer <token>` pour y accéder.

| Méthode | URL              | Description                  |
|---------|------------------|------------------------------|
| POST    | `/users/`        | Créer un nouvel utilisateur  |
| GET     | `/users/`        | Lister tous les utilisateurs |
| GET     | `/users/{id}`    | Récupérer un utilisateur par ID |
| PUT     | `/users/{id}`    | Mettre à jour un utilisateur |
| DELETE  | `/users/{id}`    | Supprimer un utilisateur     |

---

## 🧪 Exemple de requêtes

### Créer un utilisateur
```bash
curl -X POST "http://localhost:8000/users/" -H "Content-Type: application/json" -d '{"username":"user1","email":"user1@example.com","password":"password123"}'
```

### Se connecter (obtenir token)
```bash
curl -X POST "http://localhost:8000/token" -d "username=user1&password=password123"
```

### Accéder à la liste des utilisateurs
```bash
curl -H "Authorization: Bearer <token>" http://localhost:8000/users/
```

---

## 📖 Documentation interactive

FastAPI génère automatiquement la doc Swagger ici :  
```
http://localhost:8000/docs
```

Tu peux tester toutes les routes et l’authentification directement depuis cette interface.

---

## 🧩 Personnalisation

- Change la clé secrète dans `.env` (`SECRET_KEY`) pour plus de sécurité
- Modifie la durée de validité du token (`ACCESS_TOKEN_EXPIRE_MINUTES`)
- Ajuste la config de la base de données dans `DATABASE_URL`

---

## 📜 Licence

Ce projet est sous licence MIT — fais-en bon usage !
