# django-web-app — Merchex

Application d'initiation à Django réalisée en suivant le cours OpenClassrooms « Découvrez le framework Django ». C'est ma première étape avec ce framework, avant les projets Django du parcours (LITReview, SoftDesk, OC-Lettings).

Auteur : Freddy KHUTI — [GitHub](https://github.com/Freddy0ne1) · [Portfolio](https://freddykhuti.fr)

## Objectif

Poser les bases d'une application Django de bout en bout : créer un projet (`merchex`) et une application (`listings`), définir des modèles et les migrer, écrire des vues, les relier à des URL, puis afficher des données dans des templates. Le fil conducteur du cours est Merchex, un site fictif de vente de produits dérivés de groupes de musique.

## Fonctionnalités

Le projet expose quatre pages, servies par des vues fonctionnelles :

- `/hello/` : page d'accueil qui liste les groupes (`Band`) enregistrés en base, en exerçant les boucles, conditions et filtres du langage de template.
- `/listings/` : liste des annonces (`Listing`) et compteur d'articles en vente.
- `/about-us/` : page « À propos ».
- `/contact-us/` : page de contact (statique, sans formulaire à ce stade).

Deux modèles, chacun avec un seul champ, sont définis et migrés :

- `Band` : un nom (`name`).
- `Listing` : un titre (`title`).

L'interface d'administration Django est activée sur `/admin/`, mais les modèles n'y sont pas encore enregistrés. Les données de test se créent depuis le shell Django, comme le propose le cours.

## Stack

- Python 3
- Django 5.2.7 (avec `asgiref` 3.10.0, `sqlparse` 0.5.3, `tzdata` 2025.2)
- SQLite (base de données par défaut, non versionnée)

## Installation et lancement

```bash
git clone https://github.com/Freddy0ne1/django-web-app.git
cd django-web-app

python -m venv env
source env/bin/activate        # Windows : env\Scripts\activate

pip install -r requirements.txt

cd src
python manage.py migrate
python manage.py runserver
```

Pour alimenter les pages, créer quelques objets depuis le shell :

```bash
python manage.py shell
```

```python
from listings.models import Band, Listing
Band.objects.create(name="De La Soul")
Listing.objects.create(title="T-shirt De La Soul")
```

Le site est ensuite accessible sur `http://127.0.0.1:8000/hello/`. La commande `python manage.py createsuperuser` permet d'ouvrir `/admin/` si besoin.

## Structure du projet

```
src/
├── manage.py
├── merchex/                # projet : settings, urls, wsgi, asgi
│   ├── settings.py
│   └── urls.py
└── listings/               # application
    ├── models.py           # Band, Listing
    ├── views.py            # hello, about, listings, contact
    ├── migrations/
    └── templates/listings/ # hello, about, listings, contact
```

## Ce que ce projet m'a appris

- Le découpage projet / application et le rôle de `settings.py` (`INSTALLED_APPS`, base de données, templates).
- L'architecture MTV : un modèle, une vue qui interroge la base et un template qui affiche le résultat.
- L'ORM Django : déclarer un modèle, générer une migration avec `makemigrations`, l'appliquer avec `migrate`, puis manipuler les objets avec `objects.all()` et `objects.create()`.
- La configuration des URL avec `path()` et le lien entre une route et une vue.
- Le langage de template : passage d'un contexte, boucles `for`, conditions `if` / `elif` / `else`, filtres `upper` et `length`.
- Le fonctionnement de l'administration Django, prête à l'emploi dès la création du projet.
