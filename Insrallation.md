
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

```
http://localhost/pgadmin4
```

<hr>


