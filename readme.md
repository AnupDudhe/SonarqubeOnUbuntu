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
Create SonarQube Database and User 
```
sudo -i -u postgres psql
```
Inside the PostgreSQL shell, run 
```
CREATE DATABASE sonarqube;
CREATE USER sonar WITH ENCRYPTED PASSWORD 'cbz123';
ALTER ROLE sonar SET client_encoding TO 'utf8';
ALTER ROLE sonar SET default_transaction_isolation TO 'read committed';
ALTER ROLE sonar SET timezone TO 'UTC';
GRANT ALL PRIVILEGES ON DATABASE sonarqube TO sonar;
\q 
```

Install SonarQube
```
cd /opt
sudo wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-25.3.0.104237.zip
sudo unzip sonarqube-25.3.0.104237.zip
sudo mv sonarqube-25.3.0.104237 sonarqube
```
Create a SonarQube User
```
sudo groupadd sonar
sudo useradd -d /opt/sonarqube -g sonar sonar
sudo chown -R sonar:sonar /opt/sonarqube
```

Configure SonarQube
```
sudo vim /opt/sonarqube/conf/sonar.properties

Modify these lines:
sonar.jdbc.username=sonar
sonar.jdbc.password=StrongPassword
sonar.jdbc.url=jdbc:postgresql://localhost:5432/sonarqube
```