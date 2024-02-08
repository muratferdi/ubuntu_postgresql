# ubuntu_postgresql
PostgreSQL 13 Setup in Ubuntu 20

sudo apt update
sudo apt install curl gpg gnupg2 software-properties-common apt-transport-https lsb-release ca-certificates

curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc|sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg

echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" |sudo tee  /etc/apt/sources.list.d/pgdg.list

sudo apt update

sudo apt install postgresql-13 postgresql-client-13

sudo su - postgres
psql -c "alter user postgres with password 'mypass'"


psql
postgres=# \conninfo
postgres=# CREATE DATABASE mytestdb;
postgres=# \l
postgres-# \c mytestdb
createuser myuser --password


sudo nano /etc/postgresql/13/main/postgresql.conf 
listen_addresses = '*'


sudo nano /etc/postgresql/13/main/pg_hba.conf
# Accept from anywhere
host all all 0.0.0.0/0 md5

# Accept from trusted subnet
host all all 10.10.10.0/24 md5

# Restart PostgreSQL Service
sudo systemctl restart postgresql

# Check
netstat  -tunelp | grep 5432
