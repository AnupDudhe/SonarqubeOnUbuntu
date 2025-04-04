Step 1: Update System and Install Dependencies
```
sudo apt update && sudo apt upgrade -y
sudo apt install openjdk-17-jdk unzip curl wget -y
```

Install PostgreSQL
```
sudo apt install postgresql postgresql-contrib -y
```

Start and Enable PostgreSQL
```
sudo systemctl enable postgresql
sudo systemctl start postgresql
```


