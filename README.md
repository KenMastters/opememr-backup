
# 🩺 OpenEMR - Backup de Instalación Personalizada

Este repositorio contiene una copia completamente funcional de OpenEMR 7.0.2, lista para restaurar desde cero.

- Usuarios, permisos y configuraciones ya aplicados.
- Sin datos reales (solo ejemplos).
- Backup de archivos y base de datos incluidos.
- Usuario administrador por defecto: `david_admin1234`
- Contraseña: `123456789123`

---

## 📥 Descarga de archivos y preparación

### Si estás trabajando en **localhost** (misma máquina)

No es necesario usar `scp`, simplemente copia los archivos usando `cp`:

```bash
sudo cp ~/openemr_db_backup.sql /home/david/
sudo cp ~/openemr_files_backup.tar.gz /home/david/
```

Luego sigue los pasos de restauración normales.

### Si estás en un **servidor real (externo)**

Supón que ya tienes estos archivos en tu PC local:

- `openemr_db_backup.sql`
- `openemr_files_backup.tar.gz` (descargado desde [este enlace de Google Drive](https://drive.google.com/file/d/12q3hdjar5PducnPK1I3j8Bo1SkwUpRAB/view?usp=sharing))

Usa `scp` para subirlos:

```bash
scp openemr_db_backup.sql tu_usuario@ip_del_servidor:/home/tu_usuario/
scp openemr_files_backup.tar.gz tu_usuario@ip_del_servidor:/home/tu_usuario/
```

📌 Cambia `tu_usuario` por tu nombre de usuario en el servidor (ej: `david`) y `ip_del_servidor` por la IP real.

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

✅ Esta guía completa te permitirá restaurar OpenEMR correctamente en localhost o en servidor real.
