# OpenEMR Backup

Este repositorio contiene:
- Backup de archivos de OpenEMR (`openemr_files_backup.tar.gz`)
- Backup de base de datos de OpenEMR (`openemr_db_backup.sql`)

## Restauración rápida

1. Descomprimir archivos en `/var/www/html/`
2. Restaurar base de datos en MySQL.
3. Configurar `sqlconf.php` si es necesario.
4. Ajustar permisos y reiniciar Apache.

