# Microsoft SQL Server 2017 with Docker

## Install

### 1. Pull the SQL Server 2017 Linux container image from Microsoft Container Registry.

```bash
docker pull mcr.microsoft.com/mssql/server:2017-latest
```

### 2. To run the container image with Docker

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong@Passw0rd>" \
   -p 1433:1433 \
   --name sql-server \
   -h sql-server \
   --restart=always \
   -d mcr.microsoft.com/mssql/server:2017-latest
```

### 3. To view your Docker containers

```bash
docker ps -a
```

### 4. If the STATUS column shows a status of Up

```bash
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

## Change the SA password

```bash
docker exec -it sql-server /opt/mssql-tools/bin/sqlcmd \
   -S localhost -U SA -P "<YourStrong@Passw0rd>" \
   -Q 'ALTER LOGIN SA WITH PASSWORD="<YourNewStrong@Passw0rd>"'
```

## Connect to SQL Server

### 1. Docker command

```bash
docker exec -it sql-server "bash"
```

### 2. SQL command

```bash
/opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P "<YourNewStrong@Passw0rd>"
```
