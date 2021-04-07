# Procedure for setting up PostgreSQL database with Django

Must have postgresql installed before following steps.

### Connect to database with root username
```
psql -U <root_user>
```
Log in with root user credentials.  
You will be inside postgres shell.
<br>

### Create database
```
CREATE DATABASE mydatabase;
```
<br>

### Create database user
```
CREATE USER databaseuser WITH PASSWORD 'mypassword';
```
<br>

### Change attributes of the database user
```
ALTER ROLE databaseuser SET client_encoding TO 'utf8';
ALTER ROLE databaseuser SET default_transaction_isolation TO 'read committed';
ALTER ROLE databaseuser SET timezone TO 'America/Los_Angeles';
```
See [Optimizing PostgreSQL's configuration (Django Docs)](https://docs.djangoproject.com/en/3.0/ref/databases/#postgresql-notes)
<br>
<br>
### Give database user access rights to the database
```
GRANT ALL PRIVILEGES ON DATABASE <database_name> TO <user_name>;
```
<br>

### Exit from postgres shell
```
exit
```
<br>

### Install psycopg2
```
pip install psycopg2
```
<br>

### Update settings.py file
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'mydatabase',
        'USER': 'databaseuser', 
        'PASSWORD': 'mypassword',
        'HOST': '',
        'PORT': '',
    }
}
```
<br>

### References
[PostgreSQL Notes (Django Docs)](https://docs.djangoproject.com/en/3.1/ref/databases/#postgresql-notes)  
[psql](https://www.postgresql.org/docs/13/app-psql.html)  
[Manual (v13)](https://www.postgresql.org/docs/13/index.html)
[psycopg](https://www.psycopg.org/)