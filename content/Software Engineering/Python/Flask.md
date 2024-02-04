---
created: 2024-02-04T10:45
updated: 2024-02-04T12:50
---
Flask is a lightweight and robust [[python]] web framework with a minimal approach (as opposed to the batteries-included approach taken by [[django]]).

## Template

I have a template flask app with barebones db and config stuff set up here: https://git.jamesravey.me/ravenscroftj/flask-template

The template includes:
 - [Flask-SQLAlchemy](https://flask-sqlalchemy.palletsprojects.com/en/3.1.x/quickstart/)
 - [Flask-Alembic](https://flask-alembic.readthedocs.io/en/stable/)

### Contribution Grid
There is an example of doing this with HTML and CSS [here](https://codepen.io/ire/pen/Legmwo/)

## OAuth

I started by looking at Flask-OIDC but then worked out that I actually I probably just want to use flask_oauthlib to directly auth against todoist.

Turns out that `flask_oauthlib` is deprecated so I should use `authlib` instead. They give examples of using this with Flask [here](https://docs.authlib.org/en/latest/client/flask.html)

When using [[Todoist]] OAuth you have to send the `client_id` and `client_secret` again to the token endpoint which is not standard as far as I can tell.