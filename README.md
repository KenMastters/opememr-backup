# OpenEMR Backup

Este repositorio contiene:
- Backup de archivos de OpenEMR (`openemr_files_backup.tar.gz`)
- Backup de base de datos de OpenEMR (`openemr_db_backup.sql`)

## Restauración rápida

1. Descomprimir archivos en `/var/www/html/`
2. Restaurar base de datos en MySQL.
3. Configurar `sqlconf.php` si es necesario.
4. Ajustar permisos y reiniciar Apache.
=======

# 🩺 OpenEMR - Backup de Instalación Personalizada

Este repositorio contiene una copia completamente funcional de OpenEMR 7.0.2, lista para restaurar.

- Usuarios, permisos y configuraciones ya aplicados.
- Sin datos reales (solo ejemplos).
- Backup de archivos y base de datos incluidos.

---

## 📥 Descarga de archivos

- `openemr_db_backup.sql`: incluido en este repositorio.
- `openemr_files_backup.tar.gz`: disponible en Google Drive.

🔗 [Descargar openemr_files_backup.tar.gz](https://drive.google.com/file/d/12q3hdjar5PducnPK1I3j8Bo1SkwUpRAB/view?usp=sharing)

Coloca el archivo `.tar.gz` descargado en la carpeta donde vayas a restaurar OpenEMR.

---

# 🔁 Guía de Restauración Completa

## 1. Restaurar archivos de OpenEMR

```bash
sudo tar -xzvf openemr_files_backup.tar.gz -C /var/www/html/
sudo chown -R www-data:www-data /var/www/html/openemr
sudo chmod -R 755 /var/www/html/openemr
```

## 2. Restaurar la base de datos MySQL

1. Crear base de datos vacía:

```bash
sudo mysql -u root -p
```

Dentro del prompt de MySQL:

```sql
CREATE DATABASE openemr CHARACTER SET utf8 COLLATE utf8_general_ci;
EXIT;
```

2. Importar el backup SQL:

```bash
mysql -u root -p openemr < openemr_db_backup.sql
```

## 3. Ajustar sqlconf.php (si hace falta)

```bash
sudo nano /var/www/html/openemr/sites/default/sqlconf.php
```

Verifica que estos valores estén correctos:

```php
$login = 'root';
$pass = 'tu_contraseña_mysql';
$dbase = 'openemr';
```

## 4. Reiniciar Apache

```bash
sudo systemctl restart apache2
```

## 5. Acceder desde el navegador

```
http://IP_DEL_SERVIDOR/openemr
```

---

✅ Esta guía te permite restaurar en minutos una instalación operativa sin necesidad de instalar desde cero.

