# Todo Minimal API

Une API REST simple construite avec .NET 8 Minimal API pour gérer une liste de tâches (todos).

## 🚀 Fonctionnalités

- Création de todos
- Lecture de todos (individuelle ou liste complète)
- Mise à jour de todos
- Suppression de todos
- Base de données en mémoire pour un développement rapide

## 📋 Prérequis

- [.NET SDK 8.0](https://dotnet.microsoft.com/download/dotnet/8.0)
- [Docker](https://www.docker.com/products/docker-desktop/) (optionnel)

## 🛠 Installation

1. Cloner le repository
```bash
git clone https://github.com/Leith-Gharbi/DotnetMinimalApi.git
cd TodoApi
```

2. Restaurer les packages
```bash
dotnet restore
```

3. Lancer l'application
```bash
dotnet run
```

## 🔄 Endpoints API

| Méthode | Endpoint | Description |
|---------|----------|-------------|
| GET | /todoitems | Récupère tous les todos |
| GET | /todoitems/{id} | Récupère un todo spécifique |
| POST | /todoitems | Crée un nouveau todo |
| PUT | /todoitems/{id} | Met à jour un todo existant |
| DELETE | /todoitems/{id} | Supprime un todo |

## 📝 Exemples de requêtes

### Créer un nouveau todo
```http
POST http://localhost:8080/todoitems
Content-Type: application/json

{
    "name": "Acheter du lait",
    "isComplete": false
}
```

### Mettre à jour un todo
```http
PUT http://localhost:8080/todoitems/1
Content-Type: application/json

{
    "name": "Acheter du lait bio",
    "isComplete": true
}
```

## 🏗 Structure du Projet

```
TodoApi/
├── Program.cs                 # Point d'entrée et configuration de l'API
├── TodoDb.cs                 # Contexte de base de données
├── TodoItem.cs              # Modèle de données
├── Dockerfile              # Configuration Docker
└── README.md             # Ce fichier
```

## 🐳 Docker

Build l'image :
```bash
docker build -t todoapi .
```

Lancer le conteneur :
```bash
docker run -p 8080:8080 todoapi
```

## 🔧 Configuration

L'application utilise une base de données en mémoire par défaut. Voici la configuration dans Program.cs :

```csharp
builder.Services.AddDbContext<TodoDb>(opt => opt.UseInMemoryDatabase("TodoList"));
```

Pour utiliser une base de données SQL Server, modifiez la configuration ainsi :

```csharp
builder.Services.AddDbContext<TodoDb>(opt => 
    opt.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));
```

## ⚡ Performance

Les Minimal APIs offrent plusieurs avantages en termes de performance :
- Démarrage plus rapide
- Empreinte mémoire réduite
- Moins de surcharge de code
- Idéal pour les microservices

## 👥 Contribution

Les contributions sont les bienvenues ! Pour contribuer :

1. Forkez le projet
2. Créez votre branche (`git checkout -b feature/AmazingFeature`)
3. Committez vos changements (`git commit -m 'Add some AmazingFeature'`)
4. Pushez sur la branche (`git push origin feature/AmazingFeature`)
5. Ouvrez une Pull Request

