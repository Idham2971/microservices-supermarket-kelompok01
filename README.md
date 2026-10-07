## Database Configuration

Project ini menggunakan database yang terisolasi berdasarkan domain microservices. Setiap database dijalankan menggunakan Docker Compose.

### Database Catalog

Catalog Service menggunakan MongoDB 8.0.4 sebagai DBMS.

| Domain  | DBMS    | Version | Database           | Host Port | Container Port | Username      | Password            |
| ------- | ------- | ------- | ------------------ | --------: | -------------: | ------------- | ------------------- |
| Catalog | MongoDB | 8.0.4   | catalog_service_db |     27017 |          27017 | catalog_admin | catalog_secret_pass |

### Clone Repository

Clone repository menggunakan Git:

```bash
git clone https://github.com/Idham2971/microservices-supermarket-kelompok01.git
cd microservices-supermarket-kelompok01
```

### Menjalankan Environment Container

Untuk menjalankan database Catalog:

```bash
cd deployments/docker
docker compose up -d catalog-db
```

Periksa status container:

```bash
docker compose ps
```

Container yang diharapkan:

```text
supermart-catalog-db
```

Status database harus menunjukkan:

```text
Up (healthy)
```

### Mengecek Versi MongoDB

Untuk memastikan MongoDB berhasil berjalan:

```bash
docker exec -it supermart-catalog-db mongosh --eval "db.version()"
```

Versi yang digunakan:

```text
8.0.4
```

### Mengakses MongoDB

Untuk masuk ke MongoDB menggunakan akun Catalog:

```bash
docker exec -it supermart-catalog-db mongosh -u catalog_admin -p catalog_secret_pass --authenticationDatabase admin
```

Database Catalog:

```text
catalog_service_db
```

### Menghentikan Environment Container

Untuk menghentikan database Catalog:

```bash
cd deployments/docker
docker compose stop catalog-db
```

Jika ingin menghapus container tetapi tetap mempertahankan volume database:

```bash
docker compose down
```

> Jangan menggunakan `docker compose down -v` jika data database masih diperlukan karena perintah tersebut dapat menghapus volume database.

### Informasi Koneksi

```text
DBMS          : MongoDB
Version       : 8.0.4
Host          : localhost
Port          : 27017
Database      : catalog_service_db
Username      : catalog_admin
Password      : catalog_secret_pass
Container     : supermart-catalog-db
Network       : supermart-isolated-net
```
