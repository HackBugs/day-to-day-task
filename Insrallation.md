
## **Install pgAdmin** - [Insrallation link](https://www.pgadmin.org/download/pgadmin-4-apt/)

1. Create file - 1.sh
2. Paste this code

```
#
# Setup the repository
#

# Install the public key for the repository (if not done previously):
curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo gpg --dearmor -o /usr/share/keyrings/packages-pgadmin-org.gpg

# Create the repository configuration file:
sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'

#
# Install pgAdmin
#

# Install for both desktop and web modes:
sudo apt install pgadmin4

# Install for desktop mode only:
sudo apt install pgadmin4-desktop

# Install for web mode only: 
sudo apt install pgadmin4-web 

# Configure the webserver, if you installed pgadmin4-web:
sudo /usr/pgadmin4/bin/setup-web.sh
```

<hr>

```
sudo systemctl status pgadmin4
```

## 1. pgAdmin 4 ko open karne ke liye terminal mein simply type karen:

```
pgadmin4
```

## 2. Agar aapne web mode install kiya hai, toh aapko pehle web server ko configure karna hoga. Aapne jo command run ki thi:

```
sudo /usr/pgadmin4/bin/setup-web.sh
```

## 3. Setup ke baad, aap pgAdmin ko web browser ke through access kar sakte hain. Aapko browser mein yeh URL type karna hoga:

```
http://127.0.0.1/pgadmin4
```

- Example
```
http://192.168.1.72/pgadmin4/login?next=/pgadmin4/browser/
```

```
http://localhost/pgadmin4
```

<hr>

> ## Step-by-Step Process: PostgreSQL Database Install Karna

1. **System ko Update Karna:**
   Sabse pehle apne system ke package list ko update karein:
   ```bash
   sudo apt update
   ```

2. **PostgreSQL Install Karna:**
   Ab PostgreSQL aur uske required tools ko install karen:
   ```bash
   sudo apt install postgresql postgresql-contrib
   ```

   - **postgresql-contrib** package me kuch extra extensions aur tools hote hain jo PostgreSQL ke sath aate hain, jaise ki `pg_stat_statements` aur `pg_upgrade`.

3. **PostgreSQL Service ko Start Karna:**
   Installation ke baad, PostgreSQL service ko start karen:
   ```bash
   sudo systemctl start postgresql
   ```

4. **PostgreSQL Service ka Status Check Karna:**
   Ensure karen ki service successfully run ho rahi hai:
   ```bash
   sudo systemctl status postgresql
   ```

   Agar service running hai, toh output kuch is tarah dikhega:
   ```
   ● postgresql.service - PostgreSQL RDBMS
      Loaded: loaded (/lib/systemd/system/postgresql.service; enabled; vendor preset: enabled)
      Active: active (running) since Thu 2024-12-12 10:15:00 UTC; 1h 30min ago
   ```

5. **PostgreSQL Command Line Interface (CLI) ko Access Karna:**
   PostgreSQL installation ke baad, `postgres` user ko access karne ke liye aapko `psql` command line tool ka use karna hoga. `postgres` user ke under login karne ke liye:
   ```bash
   sudo -i -u postgres
   ```

   Ab aap PostgreSQL shell (`psql`) me login kar sakte hain:
   ```bash
   psql
   ```

   Ye aapko PostgreSQL shell me le jayega jahan aap SQL queries run kar sakte hain.

6. **PostgreSQL User aur Database Create Karna:**
   - **New User Banana:**
     ```bash
     createuser --interactive
     ```
     Is command ke through aap naya user create kar sakte hain.
   
   - **New Database Banana:**
     ```bash
     createdb mydatabase
     ```

   - **PostgreSQL Shell Se Exit Karna:**
     Agar aap PostgreSQL shell se bahar nikalna chahte hain, toh simply `exit` type karen.

7. **PostgreSQL ko Restart Karna (Agar zarurat ho):**
   Agar aapko configuration changes ke baad PostgreSQL ko restart karna ho:
   ```bash
   sudo systemctl restart postgresql
   ```

### PostgreSQL ko pgAdmin Se Access Karna:
Aapne jo **pgAdmin 4** install kiya hai, usse aap apne PostgreSQL server ko manage kar sakte hain:
1. **pgAdmin 4 ko open karein** (ya toh terminal se `pgadmin4` type karen, ya web mode ke liye `http://127.0.0.1/pgadmin4` browser me open karein).
2. **Server add karein**: Jab pgAdmin open ho, aapko apne PostgreSQL server ko add karna hoga (server ko connect karne ke liye `localhost` ko host ke roop mein set karein aur username `postgres` aur password set karein).
   
### Summary:
- Aapne **pgAdmin 4** install kiya hai jo ek GUI tool hai PostgreSQL ko manage karne ke liye.
- Aapko **PostgreSQL database server** alag se install karna padega (jo maine upar step-by-step bataya hai).
- Jab PostgreSQL server install ho jayega, tab aap usse pgAdmin ya `psql` command line tool se manage kar sakte hain.

Ab aap apne PostgreSQL server ko use karne ke liye ready hain!
