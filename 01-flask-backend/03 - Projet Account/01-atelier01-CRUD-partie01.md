### 🏁 Partie 1 : Déploiement d'une Application Flask avec PostgreSQL sur une Instance Amazon EC2

## Objectif : 
- Configurer et déployer votre application Flask avec PostgreSQL sur une instance Amazon EC2.
- Ce guide inclut chaque étape, depuis la création de l'instance EC2 jusqu'à la configuration des points de terminaison et le lancement de l'application.

### 🚀 Étapes à suivre :

#### 1️⃣ Créer et Configurer une Instance Amazon EC2

1. **Se connecter à la console AWS**
   - Rendez-vous sur [AWS Management Console](https://aws.amazon.com/console/).
   - Connectez-vous à votre compte.

2. **Lancer une instance EC2**
   - Accédez au service **EC2**.
   - Cliquez sur **Launch Instance**.
   - **Nom de l'instance :** `FlaskAppInstance`
   - **AMI (Amazon Machine Image) :** Choisissez **Ubuntu Server 22.04 LTS** (gratuitement éligible).
   - **Type d'instance :** Choisissez `t2.micro` (gratuitement éligible).
   - **Configuration du stockage :** Par défaut, 8 Go sont suffisants.
   - **Groupe de sécurité :** Créez un groupe de sécurité avec les règles suivantes :
     - **SSH :** Port 22, IP Source `0.0.0.0/0` (pour un accès depuis n'importe où, mais vous pouvez restreindre l'accès à votre IP).
     - **HTTP :** Port 80, IP Source `0.0.0.0/0`.
     - **HTTPS :** Port 443, IP Source `0.0.0.0/0`.

3. **Télécharger la clé PEM**
   - Lors de la création de l'instance, créez une nouvelle paire de clés, téléchargez le fichier `.pem`, et gardez-le en sécurité.

4. **Se connecter à l'instance EC2**
   - Donnez les permissions au fichier `.pem` :
     ```bash
     chmod 400 votre_clé.pem
     ```
   - Connectez-vous à votre instance :
     ```bash
     ssh -i "votre_clé.pem" ubuntu@<Public_IP_de_votre_instance>
     ```

#### 2️⃣ Installer les Dépendances sur l'Instance EC2

1. **Mettre à jour les packages**
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

2. **Installer Python 3 et pip**
   ```bash
   sudo apt install python3-pip python3-dev python3-venv -y
   ```

3. **Installer PostgreSQL**
   ```bash
   sudo apt install postgresql postgresql-contrib libpq-dev -y
   ```

4. **Installer Nginx (pour servir l'application)**
   ```bash
   sudo apt install nginx -y
   ```

5. **Configurer PostgreSQL**
   - Accéder à PostgreSQL :
     ```bash
     sudo -u postgres psql
     ```
   - Créer un utilisateur et une base de données :
     ```sql
     CREATE USER flaskuser WITH PASSWORD 'flaskpassword';
     CREATE DATABASE flaskdb;
     GRANT ALL PRIVILEGES ON DATABASE flaskdb TO flaskuser;
     \q
     ```

#### 3️⃣ Configurer le Projet Flask

1. **Créer la structure du projet sur l'instance**
   ```bash
   mkdir flask_accounts
   cd flask_accounts
   ```

2. **Créer un environnement virtuel et l'activer**
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **Installer Flask et les autres dépendances**
   ```bash
   pip install Flask SQLAlchemy psycopg2-binary Flask-Migrate gunicorn
   ```

4. **Créer la structure du projet Flask**
   ```bash
   mkdir app migrations
   cd app
   touch __init__.py models.py routes.py services.py config.py
   cd ..
   touch requirements.txt run.py
   ```

5. **Ajouter la configuration de la base de données dans `config.py`**
   ```python
   import os

   class Config:
       SQLALCHEMY_DATABASE_URI = 'postgresql://flaskuser:flaskpassword@localhost:5432/flaskdb'
       SQLALCHEMY_TRACK_MODIFICATIONS = False
   ```

6. **Définir les modèles dans `models.py`**
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

   class Account(db.Model):
       __tablename__ = 'accounts'
       account_number = db.Column(db.Integer, primary_key=True)
       customer_id = db.Column(db.Integer, db.ForeignKey('customer.customer_id'))
       account_type = db.Column(db.String(20))
       branch_address = db.Column(db.String(100))
       create_dt = db.Column(db.DateTime)
   ```

7. **Initialiser l'application dans `__init__.py`**
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

8. **Définir les routes dans `routes.py`**
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

9. **Créer un fichier Gunicorn pour exécuter l'application**
   Créez un fichier `wsgi.py` dans le répertoire principal (flask_accounts) avec le contenu suivant :

   ```python
   from app import create_app

   app = create_app()

   if __name__ == "__main__":
       app.run()
   ```

10. **Testez votre application en local**
    Avant de configurer Nginx, assurez-vous que l'application fonctionne :
    ```bash
    gunicorn --bind 0.0.0.0:5000 wsgi:app
    ```

#### 4️⃣ Configurer Nginx pour Servir l'Application Flask

1. **Configurer Nginx**
   - Supprimez la configuration par défaut :
     ```bash
     sudo rm /etc/nginx/sites-enabled/default
     ```
   - Créez une nouvelle configuration pour votre application :
     ```bash
     sudo nano /etc/nginx/sites-available/flask_accounts
     ```

   Ajoutez le contenu suivant :
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

2. **Activer la configuration**
   ```bash
   sudo ln -s /etc/nginx/sites-available/flask_accounts /etc/nginx/sites-enabled
   ```

3. **Redémarrer Nginx**
   ```bash
   sudo systemctl restart nginx
   ```

4. **Configurer Gunicorn en tant que Service**
   - Créez un fichier de service pour Gunicorn :
     ```bash
     sudo nano /etc/systemd/system/flask_accounts.service
     ```

   Ajoutez le contenu suivant :
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

   - **User** : L'utilisateur qui exécute le service (généralement `ubuntu` sur une instance EC2 Ubuntu).
   - **Group** : Le groupe avec lequel Nginx interagit (`www-data` est recommandé pour Nginx).
   - **WorkingDirectory** : Le répertoire racine de votre projet Flask.
   - **ExecStart** : Le chemin pour démarrer Gunicorn avec les options nécessaires.



#### 5️⃣ Configurer Gunicorn en tant que Service (suite)

   
1. **Démarrer et activer le service Gunicorn**
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

2. **Vérifier le statut du service**
   - Pour vérifier que Gunicorn fonctionne correctement, exécutez :
     ```bash
     sudo systemctl status flask_accounts
     ```

   Vous devriez voir un message indiquant que le service est actif (running).

#### 6️⃣ Configuration des Points de Terminaison (Endpoints)

1. **Accéder à l'application depuis le navigateur**
   - Une fois que le service Gunicorn est en cours d'exécution et que Nginx est configuré, vous pouvez accéder à votre application Flask en visitant l'adresse IP publique de votre instance EC2 dans un navigateur :
     ```
     http://<votre_IP_publique>
     ```

2. **Tester les endpoints définis dans `routes.py`**
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

3. **Sécuriser les communications avec HTTPS (optionnel)**
   - Pour sécuriser votre application avec HTTPS, vous pouvez utiliser **Certbot** pour obtenir un certificat SSL gratuit de Let's Encrypt.
   - Installez Certbot et Nginx plugin :
     ```bash
     sudo apt install certbot python3-certbot-nginx -y
     ```
   - Obtenez un certificat SSL :
     ```bash
     sudo certbot --nginx -d votre_nom_de_domaine
     ```
   - Certbot configurera automatiquement Nginx pour utiliser le certificat SSL.

4. **Configurer le pare-feu**
   - Si vous avez activé un pare-feu (par exemple, **UFW**), assurez-vous d'autoriser les connexions sur le port 80 (HTTP) et le port 443 (HTTPS) :
     ```bash
     sudo ufw allow 'Nginx Full'
     sudo ufw enable
     ```

---

### 🚨 Résolution des Problèmes Courants

1. **Gunicorn ne démarre pas correctement :**
   - Vérifiez les logs du service pour des erreurs spécifiques :
     ```bash
     sudo journalctl -u flask_accounts.service
     ```

2. **Nginx affiche une erreur 502 Bad Gateway :**
   - Assurez-vous que le service Gunicorn est en cours d'exécution et que le socket Unix est correctement configuré.

3. **Erreur de connexion à PostgreSQL :**
   - Vérifiez que les informations d'identification dans `config.py` correspondent bien à celles de votre configuration PostgreSQL.

---

### 🌐 Points de Terminaison (Endpoints) Résumés

- **GET /customers** : Récupère la liste de tous les clients.
- **GET /customer/<int:id>** : Récupère un client spécifique par ID.
- **POST /newCustomer** : Crée un nouveau client.
- **POST /newAccount** : Crée un nouveau compte bancaire pour un client existant.

---

### 🎯 Prochaines Étapes

- **Améliorer la gestion des erreurs** : Implémentez une gestion des erreurs plus robuste pour les opérations CRUD.
- **Optimisation** : Envisagez de configurer la mise en cache avec Redis pour améliorer les performances.
- **Déploiement CI/CD** : Automatisez le déploiement de votre application avec des outils comme Jenkins ou GitHub Actions.

---
