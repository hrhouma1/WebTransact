# 🏁 Partie 1 : Déploiement d'une Application Flask avec PostgreSQL sur Amazon EC2

Ce guide vous expliquera comment déployer une application Flask avec PostgreSQL sur une instance Amazon EC2. Vous apprendrez à configurer votre instance, à installer les dépendances nécessaires, et à lancer votre application en utilisant Gunicorn et Nginx.

## 🚀 Étapes à suivre :

### 1️⃣ Créer et Configurer une Instance Amazon EC2

#### 1.1 **Se connecter à la console AWS**
- Accédez à [AWS Management Console](https://aws.amazon.com/console/).
- Connectez-vous à votre compte AWS.

#### 1.2 **Lancer une instance EC2**
- Allez dans le service **EC2**.
- Cliquez sur **Launch Instance**.
- **Nom de l'instance :** `FlaskAppInstance`.
- **AMI (Amazon Machine Image) :** Sélectionnez **Ubuntu Server 22.04 LTS** (éligible au niveau gratuit).
- **Type d'instance :** Sélectionnez `t2.micro` (éligible au niveau gratuit).
- **Configuration du stockage :** 8 Go par défaut suffisent.
- **Groupe de sécurité :** Créez un groupe de sécurité avec les règles suivantes :
  - **SSH :** Port 22, IP Source `0.0.0.0/0` (vous pouvez restreindre à votre IP).
  - **HTTP :** Port 80, IP Source `0.0.0.0/0`.
  - **HTTPS :** Port 443, IP Source `0.0.0.0/0`.

#### 1.3 **Télécharger la clé PEM**
- Lors de la création de l'instance, créez une nouvelle paire de clés, téléchargez le fichier `.pem`, et gardez-le en sécurité.

#### 1.4 **Se connecter à l'instance EC2**
- Donnez les permissions nécessaires au fichier `.pem` :
  ```bash
  chmod 400 votre_clé.pem
  ```
- Connectez-vous à votre instance :
  ```bash
  ssh -i "votre_clé.pem" ubuntu@<Public_IP_de_votre_instance>
  ```

---

### 2️⃣ Installer les Dépendances sur l'Instance EC2

#### 2.1 **Mettre à jour les packages**
```bash
sudo apt update && sudo apt upgrade -y
```

#### 2.2 **Installer Python 3 et pip**
```bash
sudo apt install python3-pip python3-dev python3-venv -y
```

#### 2.3 **Installer PostgreSQL**
```bash
sudo apt install postgresql postgresql-contrib libpq-dev -y
```

#### 2.4 **Installer Nginx**
```bash
sudo apt install nginx -y
```

---

### 3️⃣ Configurer PostgreSQL

#### 3.1 **Accéder à PostgreSQL**
- Connectez-vous à PostgreSQL en tant qu'utilisateur `postgres` :
  ```bash
  sudo -u postgres psql
  ```

#### 3.2 **Créer un utilisateur et une base de données**
- Créez un utilisateur pour votre application Flask :
  ```sql
  CREATE USER flaskuser WITH PASSWORD 'flaskpassword';
  CREATE DATABASE flaskdb;
  GRANT ALL PRIVILEGES ON DATABASE flaskdb TO flaskuser;
  \q
  ```

---

### 4️⃣ Configurer le Projet Flask

#### 4.1 **Créer la structure du projet sur l'instance**
```bash
mkdir flask_accounts
cd flask_accounts
```

#### 4.2 **Créer un environnement virtuel et l'activer**
```bash
python3 -m venv venv
source venv/bin/activate
```

#### 4.3 **Installer Flask et les autres dépendances**
```bash
pip install Flask SQLAlchemy psycopg2-binary Flask-Migrate gunicorn
```

#### 4.4 **Créer la structure du projet Flask**
```bash
mkdir app migrations
cd app
touch __init__.py models.py routes.py services.py config.py
cd ..
touch requirements.txt run.py
```

---

### 5️⃣ Configuration du Projet Flask

#### 5.1 **Ajouter la configuration de la base de données dans `config.py`**
```python
import os

class Config:
    SQLALCHEMY_DATABASE_URI = 'postgresql://flaskuser:flaskpassword@localhost:5432/flaskdb'
    SQLALCHEMY_TRACK_MODIFICATIONS = False
```

#### 5.2 **Définir les modèles dans `models.py`**
```python
from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()

class Customer(db.Model):
    __tablename__ = 'customer'
    customer_id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(50))
    email = db.Column(db.String(100))
    mobile_number = db.Column(db.String(15))
    create_dt = db.Column(db.DateTime)
    
    # Relation avec Account
    accounts = db.relationship('Account', backref='customer', lazy=True)

class Account(db.Model):
    __tablename__ = 'accounts'
    account_number = db.Column(db.Integer, primary_key=True)
    customer_id = db.Column(db.Integer, db.ForeignKey('customer.customer_id'))
    account_type = db.Column(db.String(20))
    branch_address = db.Column(db.String(100))
    create_dt = db.Column(db.DateTime)
```

#### 5.3 **Initialiser l'application dans `__init__.py`**
```python
from flask import Flask
from .config import Config
from .models import db

def create_app():
    app = Flask(__name__)
    app.config.from_object(Config)
    db.init_app(app)
    
    with app.app_context():
        db.create_all()

    return app
```

#### 5.4 **Définir les routes dans `routes.py`**
```python
from flask import request, jsonify
from .models import db, Customer, Account
from datetime import datetime
from . import create_app

app = create_app()

@app.route('/customers', methods=['GET'])
def get_customers():
    customers = Customer.query.all()
    return jsonify([customer.serialize() for customer in customers])

@app.route('/customer/<int:id>', methods=['GET'])
def get_customer_by_id(id):
    customer = Customer.query.get(id)
    if customer:
        return jsonify(customer.serialize())
    return jsonify({'error': 'Customer not found'}), 404

@app.route('/newCustomer', methods=['POST'])
def create_customer():
    data = request.get_json()
    new_customer = Customer(
        name=data['name'],
        email=data['email'],
        mobile_number=data['mobile_number'],
        create_dt=datetime.now()
    )
    db.session.add(new_customer)
    db.session.commit()

    if 'accounts' in data:
        for acc_data in data['accounts']:
            new_account = Account(
                account_number=acc_data['account_number'],
                customer_id=new_customer.customer_id,
                account_type=acc_data['account_type'],
                branch_address=acc_data['branch_address'],
                create_dt=datetime.now()
            )
            db.session.add(new_account)
    
    db.session.commit()
    return jsonify(new_customer.serialize()), 201

@app.route('/newAccount', methods=['POST'])
def create_account():
    data = request.get_json()
    new_account = Account(
        account_number=data['account_number'],
        customer_id=data['customer_id'],
        account_type=data['account_type'],
        branch_address=data['branch_address'],
        create_dt=datetime.now()
    )
    db.session.add(new_account)
    db.session.commit()
    return jsonify(new_account.serialize()), 201
```

#### 5.5 **Créer un fichier Gunicorn pour exécuter l'application**
- Créez un fichier `wsgi.py` dans le répertoire principal (flask_accounts) avec le contenu suivant :

```python
from app import create_app

app = create_app()

if __name__ == "__main__":
    app.run()
```

#### 5.6 **Tester l'application en local**
- Avant de configurer Nginx, assurez-vous que l'application fonctionne :
```bash
gunicorn --bind 0.0.0.0:5000 wsgi:app
```

---

### 6️⃣ Configurer Nginx pour Servir l'Application Flask

#### 6.1 **Configurer Nginx**
- Supprimez la configuration par défaut :
```bash
sudo rm /etc/nginx/sites-enabled/default
```
- Créez une nouvelle configuration pour votre application :
```bash
sudo nano /etc/nginx/sites-available/flask_accounts
```

- Ajoutez le contenu suivant :
```text
server {
    listen 80;
    server_name <votre_IP_publique>;

    location / {
        proxy_pass http://127.0.0.1:5000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

#### 6.2 **Activer la configuration**
```bash
sudo ln -s /etc/nginx/sites-available/flask_accounts /etc/nginx/sites-enabled
```

#### 6.3 **Redémarrer Nginx**
```bash
sudo systemctl restart nginx
```

---

### 7️⃣ Configurer Gunicorn en tant que Service

#### 7.1 **Créer un fichier de service pour Gunicorn**
- Créez un

 fichier de service pour Gunicorn :
```bash
sudo nano /etc/systemd/system/flask_accounts.service
```

- Ajoutez le contenu suivant :
```text
[Unit]
Description=Gunicorn instance to serve Flask application
After=network.target

[Service]
User=ubuntu
Group=www-data
WorkingDirectory=/home/ubuntu/flask_accounts
ExecStart=/home/ubuntu/flask_accounts/venv/bin/gunicorn --workers 3 --bind unix:flask_accounts.sock -m 007 wsgi:app

[Install]
WantedBy=multi-user.target
```

#### 7.2 **Démarrer et activer le service Gunicorn**
- Rechargez le système pour prendre en compte la nouvelle configuration du service :
```bash
sudo systemctl daemon-reload
```
- Démarrez le service Gunicorn :
```bash
sudo systemctl start flask_accounts
```
- Activez Gunicorn pour qu'il démarre automatiquement au démarrage du système :
```bash
sudo systemctl enable flask_accounts
```

#### 7.3 **Vérifier le statut du service**
- Pour vérifier que Gunicorn fonctionne correctement, exécutez :
```bash
sudo systemctl status flask_accounts
```
- Vous devriez voir un message indiquant que le service est actif (running).

---

### 8️⃣ Configuration des Points de Terminaison (Endpoints)

#### 8.1 **Accéder à l'application depuis le navigateur**
- Une fois que le service Gunicorn est en cours d'exécution et que Nginx est configuré, vous pouvez accéder à votre application Flask en visitant l'adresse IP publique de votre instance EC2 dans un navigateur :
```text
http://<votre_IP_publique>
```

#### 8.2 **Tester les endpoints définis dans `routes.py`**
- Pour voir la liste des clients : `http://<votre_IP_publique>/customers`
- Pour récupérer un client spécifique par ID : `http://<votre_IP_publique>/customer/<id>`
- Pour ajouter un nouveau client, vous pouvez utiliser un outil comme **Postman** ou **cURL** pour envoyer une requête POST à `http://<votre_IP_publique>/newCustomer` avec un corps JSON similaire à celui-ci :
```json
{
  "name": "John Doe",
  "email": "john.doe@example.com",
  "mobile_number": "1234567890"
}
```
- Pour ajouter un nouveau compte : `http://<votre_IP_publique>/newAccount` avec un corps JSON tel que :
```json
{
  "account_number": 1,
  "customer_id": 1,
  "account_type": "Checking",
  "branch_address": "123 Main St"
}
```

---

### 🚨 Résolution des Problèmes Courants

#### 1️⃣ **Gunicorn ne démarre pas correctement**
- Vérifiez les logs du service pour des erreurs spécifiques :
```bash
sudo journalctl -u flask_accounts.service
```

#### 2️⃣ **Nginx affiche une erreur 502 Bad Gateway**
- Assurez-vous que le service Gunicorn est en cours d'exécution et que le socket Unix est correctement configuré.

#### 3️⃣ **Erreur de connexion à PostgreSQL**
- Vérifiez que les informations d'identification dans `config.py` correspondent bien à celles de votre configuration PostgreSQL.

---

## 🛠️ Test et Vérification

### 1️⃣ **Vérification via GET**
- **Vérifiez les opérations via l'URL `http://localhost:8080/accounts` ou via POSTMAN GET `http://localhost:8080/accounts`**.

### 2️⃣ **Continuer à tester**
- **Répétez les opérations POST, PUT, DELETE pour chaque compte et chaque client jusqu'à ce que toutes les fonctionnalités soient validées**.

---

## 🎓 Prochains Défis

### 1️⃣ **Documentation via Swagger**
- Implémentez et testez la documentation de votre API avec Swagger.

### 2️⃣ **Optimisation et Sécurité**
- Envisagez de sécuriser votre application avec HTTPS en utilisant Certbot pour obtenir un certificat SSL gratuit.

### 3️⃣ **Déploiement CI/CD**
- Automatisez le déploiement de votre application avec des outils comme Jenkins ou GitHub Actions.

---

## ✍️ Évaluation Formative

### 1️⃣ **Insertion Multiple en Lots**
- **Objectif** : Créer plusieurs comptes via POST.
- **URL** : `http://localhost:8080/newAccounts`
- **Body** : Passez une liste d'objets JSON représentant les comptes à créer.

### 2️⃣ **Suppression en Masse**
- **Objectif** : Implémenter la suppression de tous les comptes d'un seul coup.
- **URL** : `http://localhost:8080/deleteAllAccounts`
- **Méthode** : DELETE (pas de body requis).

### 3️⃣ **Mise à Jour Multiple**
- **Objectif** : Mettre à jour plusieurs comptes en une seule opération.
- **URL** : `http://localhost:8080/updateAccounts`
- **Body** : Liste d'objets JSON représentant les comptes à mettre à jour.

---

## 📄 Annexe : Explication des Annotations de Mapping dans le Contrôleur Flask

| **Route**                        | **Méthode HTTP** | **URL**                    | **Description**                                                                                                                                         | **Exemple d'Utilisation**                                              |
|----------------------------------|------------------|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------|
| `/deleteAccount/<int:id>`        | DELETE           | `/deleteAccount/<id>`        | Cette route est utilisée pour supprimer un compte spécifique en utilisant son identifiant (`id`). Le `id` est passé en tant que paramètre de l'URL.      | Supprimer un compte : `DELETE /deleteAccount/1`                        |
| `/update/<int:id>`               | PUT              | `/update/<id>`               | Cette route permet de mettre à jour les détails d'un compte spécifique. Le `id` du compte à mettre à jour est passé en paramètre dans l'URL.            | Mettre à jour un compte : `PUT /update/1`                              |
| `/newAccount`                    | POST             | `/newAccount`                | Cette route est utilisée pour créer un nouveau compte. Les détails du compte sont passés dans le corps de la requête en format JSON.                    | Créer un nouveau compte : `POST /newAccount`                           |
| `/accounts`                      | GET              | `/accounts`                  | Cette route permet de récupérer la liste de tous les comptes disponibles.                                                                                | Récupérer tous les comptes : `GET /accounts`                           |
| `/myAccount/<int:id>`            | GET              | `/myAccount/<id>`            | Cette route permet de récupérer les détails d'un compte spécifique en utilisant son identifiant (`id`). Le `id` est passé en tant que paramètre de l'URL. | Récupérer un compte spécifique : `GET /myAccount/1`                    |

---

### 🔍 Détails des Annotations :

1. **DELETE** : Utilisée pour la suppression des ressources.
   - **Exemple** : `@app.route('/deleteAccount/<int:id>', methods=['DELETE'])`
   - **Description** : Supprime un compte en fonction de l'ID fourni dans l'URL.

2. **PUT** : Utilisée pour mettre à jour une ressource existante.
   - **Exemple** : `@app.route('/update/<int:id>', methods=['PUT'])`
   - **Description** : Met à jour les informations d'un compte existant en fonction de l'ID.

3. **POST** : Utilisée pour la création d'une nouvelle ressource.
   - **Exemple** : `@app.route('/newAccount', methods=['POST'])`
   - **Description** : Crée un nouveau compte avec les détails fournis dans le corps de la requête.

4. **GET** : Utilisée pour récupérer des ressources.
   - **Exemple** : `@app.route('/accounts', methods=['GET'])`
   - **Description** : Récupère la liste de tous les comptes disponibles.

---

## 💡 Remarque :
- Les méthodes HTTP DELETE, PUT, POST, et GET sont des standards pour interagir avec les ressources sur le serveur.
- Chaque méthode correspond à une opération spécifique : suppression, mise à jour, création, ou récupération de données.

---
