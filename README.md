
# 🩺 OpenEMR - Backup de Instalación Personalizada

Este repositorio contiene una copia completamente funcional de OpenEMR 7.0.2, lista para restaurar desde cero.

- Usuarios, permisos y configuraciones ya aplicados.
- Sin datos reales (solo ejemplos).
- Backup de archivos y base de datos incluidos.
- Usuario administrador por defecto: `david_admin1234`
- Contraseña: `123456789123`

---

## 📥 Descarga de archivos

- `openemr_db_backup.sql`: incluido en este repositorio.
- `openemr_files_backup.tar.gz`: disponible en Google Drive.

🔗 [Descargar openemr_files_backup.tar.gz](https://drive.google.com/file/d/12q3hdjar5PducnPK1I3j8Bo1SkwUpRAB/view?usp=sharing)

Coloca el archivo `.tar.gz` descargado en la carpeta donde vayas a restaurar OpenEMR.

---

# 🔁 Guía Completa de Restauración y Puesta en Marcha

## 1. Instalar dependencias necesarias

```bash
sudo apt update
sudo apt install apache2 mysql-server php php-mysql libapache2-mod-php php-xml php-mbstring php-zip php-soap php-gd php-curl unzip -y
```

## 2. Habilitar y arrancar servicios

```bash
sudo systemctl enable apache2
sudo systemctl start apache2
sudo systemctl enable mysql
sudo systemctl start mysql
```

## 3. Restaurar archivos de OpenEMR

```bash
sudo tar -xzvf openemr_files_backup.tar.gz -C /var/www/html/
sudo chown -R www-data:www-data /var/www/html/openemr
sudo chmod -R 755 /var/www/html/openemr
```

## 4. Crear la base de datos

```bash
sudo mysql -u root -p
```

Dentro del prompt de MySQL:

```sql
CREATE DATABASE openemr CHARACTER SET utf8 COLLATE utf8_general_ci;
EXIT;
```

## 5. Importar la base de datos

```bash
mysql -u root -p openemr < openemr_db_backup.sql
```

## 6. Verificar configuración en `sqlconf.php`

```bash
sudo nano /var/www/html/openemr/sites/default/sqlconf.php
```

Asegúrate de que contiene lo siguiente:

```php
$login = 'root';
$pass = 'tu_contraseña_mysql';
$dbase = 'openemr';
```

## 7. Reiniciar Apache

```bash
sudo systemctl restart apache2
```

## 8. Acceder a OpenEMR

Abre tu navegador y ve a:

```
http://IP_DEL_SERVIDOR/openemr
```

Usa estas credenciales iniciales:

- **Usuario:** `david_admin1234`
- **Contraseña:** `123456789123`

---

✅ Esta guía completa te permitirá reinstalar OpenEMR tal como lo tenías configurado, en minutos y sin errores.
