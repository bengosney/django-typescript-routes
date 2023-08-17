# django-typescript-routes

Meant as a spiritual successor to [django-js-reverse](https://pypi.org/project/django-js-reverse/), `django-typescript-routes` is meant to answer to the following question:

> I've got a Typescript-based SPA that is powered by a Django-based API. How do I safely make requests to Django without messing up the routes or parameters?

`django-typescript-routes` is how! At a high level, it turns:

```
urls = [
    path(
        r"about",
        about,
        name="about",
    ),
    path(
        r"/<str:username>",
        subscribe,
        name="subscribe",
    ),
    path(
        r"/<str:username>/subscribers/<pk:uuid>/success",
        subscription_success,
        name="subscription-success",
    ),
]
```

into:

```
const URLS = {
    'about': () => `/`,
    'subscribe': (username: string) => `/${username}`,
    'subscription-success': (username: string, pk: string) => `/${username}/subscribers/${pk}/success`,
}
```

## Quick start

1. Add `django-typescript-routes` to your `INSTALLED_APPS` setting:

```
INSTALLED_APPS = [
    ...,
    "typescript_routes",
    ...
]
```

2. Run the management command to print out the typescript file:

```
python manage.py generate_typescript_routes --conf projectname.urls > assets/urls.ts
```