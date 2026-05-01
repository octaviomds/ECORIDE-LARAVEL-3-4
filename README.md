# Documentation Projet Ecoride

## Getting Started

Follow these steps to set up and run the Laravel Docker Examples Project:

### Prerequisites

Ensure you have Docker and Docker Compose installed. You can verify by running:

```bash
docker --version
docker compose version
```

If these commands do not return the versions, install Docker and Docker Compose using the official documentation: [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/).

### Clone the Repository

```bash
git clone https://github.com/rw4lll/laravel-docker-examples.git
cd laravel-docker-examples
```

### Setting Up the Development Environment

1. Copy the `.env.example` file to `.env` and adjust any necessary environment variables:

```bash
cp .env.example .env
```

> Hint: adjust the `UID` and `GID` variables in the `.env` file to match your user ID and group ID. You can find these by running `id -u` and `id -g` in the terminal.

2. Start the Docker Compose services:

```bash
docker compose -f compose.dev.yaml up -d
```

3. Install Laravel dependencies:

```bash
docker compose -f compose.dev.yaml exec workspace bash
composer install
npm install
npm run dev
```

4. Run migrations:

```bash
docker compose -f compose.dev.yaml exec workspace php artisan migrate
```

5. Access the application:

Open your browser and navigate to [http://localhost](http://localhost).

---

## Usage

Here are some common commands and tips for using the development environment:

### Accessing the Workspace Container

The workspace sidecar container includes Composer, Node.js, NPM, and other tools necessary for Laravel development (e.g. assets building).

```bash
docker compose -f compose.dev.yaml exec workspace bash
```

### Run Artisan Commands

```bash
docker compose -f compose.dev.yaml exec workspace php artisan migrate
```

### Rebuild Containers

```bash
docker compose -f compose.dev.yaml up -d --build
```

### Stop Containers

```bash
docker compose -f compose.dev.yaml down
```

### View Logs

```bash
docker compose -f compose.dev.yaml logs -f
```

For specific services:

```bash
docker compose -f compose.dev.yaml logs -f web
```

### Creation d'un administrateur

```bash
docker compose -f compose.dev.yaml exec workspace php artisan make:admin
```

Ou via tinker :

```bash
docker compose -f compose.dev.yaml exec workspace php artisan tinker
```

```php
\App\Models\User::create([
    'name'     => 'Admin',
    'email'    => 'admin@example.com',
    'password' => bcrypt('password'),
    'role'     => 'admin',
]);
```

---

## Installation de l'environnement

### Verification des versions

```bash
herd --version
php --version
laravel --version
composer --version
node --version
```

### Demarrage du projet

```bash
docker compose -f compose.dev.yaml exec workspace bash
```

### Clonage et configuration initiale

```bash
git clone path-to-your-repository
cd repository-name
cp .env.example .env
composer install
herd php artisan key:generate
herd php artisan migrate
```

### Lier l'application a Herd

```bash
herd open
cd ~/Sites/your-project
herd link
herd link custom-domain
```

---

## Configuration des mails

Dans le fichier `.env` :

```env
MAIL_MAILER=smtp
MAIL_HOST=127.0.0.1
MAIL_PORT=2525
MAIL_USERNAME=${APP_NAME}
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"
```

---

## Installation de PostgreSQL

Dans le fichier `.env` :

```env
DB_CONNECTION=pgsql
DB_HOST=127.0.0.1
DB_PORT=5432
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=
```

---

## Installation de MongoDB

### Dependances

```bash
composer require mongodb/laravel-mongodb
```

### Configuration dans `.env`

```env
DB_CONNECTION=mongodb
DB_PORT=27020
DB_URI="mongodb://127.0.0.1:27020/laravel"
```

---

## Installation de Expose Laravel

```bash
docker build -t expose .
expose token 00a81d35-71e6-4c66-a397-4ccfdecebce5
expose default-server eu-2
expose share http://localhost
expose --basicAuth="admin:secret"
```

---

## Installation de Laravel Forge

### CLI Forge

```bash
composer global require laravel/forge-cli
forge
```

### SDK Forge

```bash
composer require laravel/forge-sdk
```

```php
$forge = new Laravel\Forge\Forge(TOKEN_HERE);
$servers = $forge->servers();
```

### Authentification

```bash
forge login
forge login --token=your-api-token
```

### Cles SSH

```bash
forge ssh:test
forge ssh:configure
forge ssh:configure --key=/path/to/public/key.pub --name=sallys-macbook
forge ssh
forge ssh server-name
```

### Deploiement

```bash
forge deploy
forge deploy example.com
```

### Logs de l'application

```bash
forge site:logs
forge site:logs --follow
forge site:logs example.com
forge site:logs example.com --follow
```

---

## Commandes Docker

### Commandes courantes

| Commande  | Description                                      |
|-----------|--------------------------------------------------|
| run       | Creer et demarrer un conteneur depuis une image  |
| exec      | Executer une commande dans un conteneur actif    |
| ps        | Lister les conteneurs                            |
| build     | Construire une image depuis un Dockerfile        |
| pull      | Telecharger une image depuis un registre         |
| push      | Publier une image vers un registre               |
| images    | Lister les images                                |
| login     | S'authentifier sur un registre                   |
| logout    | Se deconnecter d'un registre                     |
| search    | Rechercher des images sur Docker Hub             |
| version   | Afficher la version de Docker                    |
| info      | Afficher les informations systeme                |

### Commandes de gestion

| Commande   | Description                                           |
|------------|-------------------------------------------------------|
| builder    | Gerer les builds                                      |
| compose    | Docker Compose                                        |
| container  | Gerer les conteneurs                                  |
| image      | Gerer les images                                      |
| network    | Gerer les reseaux                                     |
| volume     | Gerer les volumes                                     |
| system     | Gerer Docker                                          |
| plugin     | Gerer les plugins                                     |
| manifest   | Gerer les manifests d'image                           |
| trust      | Gerer la confiance sur les images Docker              |

### Commandes supplementaires

| Commande  | Description                                                          |
|-----------|----------------------------------------------------------------------|
| attach    | Attacher les flux stdin/stdout/stderr a un conteneur actif           |
| commit    | Creer une image depuis les changements d'un conteneur                |
| cp        | Copier des fichiers entre un conteneur et le systeme local           |
| diff      | Inspecter les changements sur le systeme de fichiers d'un conteneur  |
| events    | Obtenir des evenements en temps reel depuis le serveur               |
| export    | Exporter le systeme de fichiers d'un conteneur en tar                |
| inspect   | Retourner des informations bas niveau sur des objets Docker          |
| kill      | Arreter un ou plusieurs conteneurs                                   |
| logs      | Afficher les logs d'un conteneur                                     |
| pause     | Mettre en pause les processus d'un conteneur                         |
| port      | Lister les mappings de ports d'un conteneur                          |
| rename    | Renommer un conteneur                                                |
| restart   | Redemarrer un ou plusieurs conteneurs                                |
| rm        | Supprimer un ou plusieurs conteneurs                                 |
| rmi       | Supprimer une ou plusieurs images                                    |
| save      | Sauvegarder une image en archive tar                                 |
| start     | Demarrer un ou plusieurs conteneurs arretes                          |
| stats     | Afficher les statistiques de ressources en temps reel                |
| stop      | Arreter un ou plusieurs conteneurs actifs                            |
| tag       | Creer un tag pour une image                                          |
| top       | Afficher les processus en cours dans un conteneur                    |
| unpause   | Reprendre les processus d'un conteneur mis en pause                  |
| update    | Mettre a jour la configuration d'un conteneur                        |
| wait      | Attendre l'arret d'un conteneur et afficher son code de sortie       |
