# Borrado de Datos  
**Autor:** Evan Silva González  

> Un manual práctico, claro y con una dosis mínima de humor para sobrevivir al mundo del análisis forense (sin romper ningún disco... al menos sin querer).

---

## Índice
- [Los peritos y su trabajo](#los-peritos-y-su-trabajo)  
- [Gestión de un caso forense](#gestión-de-un-caso-forense)  
- [Puntos clave](#puntos-clave)  
- [Un equipo de forenses](#un-equipo-de-forenses)  
- [Tipos de peritos](#tipos-de-peritos)  
- [Habilidades de los peritos](#habilidades-de-los-peritos)  
- [Eliminación y recuperación de información](#eliminación-y-recuperación-de-información)  
- [Discos SSD](#discos-ssd)  
- [Métodos de uso](#métodos-de-uso)  
- [Recuva (Windows)](#recuva-windows)  
- [PhotoRec (Linux--windows--macos)](#photorec-linux--windows--macos)  
- [Foremost (Linux)](#foremost-linux)  
- [Scalpel (Linux)](#scalpel-linux)  
- [Advertencia importante (Borrado SSD)](#advertencia-importante-borrado-ssd)  
- [Ver los discos del sistema](#ver-los-discos-del-sistema-linux)  
- [Montar un disco en Linux](#montar-un-disco-en-linux)

---

# Resumen del ejercicio: Borrado permanente de datos

## Los peritos y su trabajo
Los peritos son fundamentales en los procesos de recogida y análisis de información. Existen dos tipos principales:

### Peritaje corporativo
- El entorno corporativo suele ser más relajado (pero sin pasarse).  
- Normalmente no se espera que la evidencia tenga la misma fortaleza legal que en un juicio.  
- Ejemplos: revisar correos, logs internos, páginas visitadas, etc.

### Peritaje judicial
- Aquí empieza la seriedad nivel “jefe final”.  
- Toda evidencia debe ser tratada con procedimientos estrictos.  
- Nunca se trabaja directamente sobre los datos originales: solo sobre copias forenses en modo solo lectura.  
- Si alteras la evidencia… el juez puede alterarse también.

Además, la documentación es clave. Un perito debe:
- Registrar cada paso.  
- Asegurar que todo es reproducible.  
- Mantener una cadena de custodia impecable.

Porque si no está documentado… no existe.

- Los peritajes corpotativos pueden volverse judiciales. Un perito DEBE denunciar infracciones contra la ley. Hay normas en la empresa que al romperse, no rompen la ley, un ejemplo seria que la empresa no permitiese acceder a páginas como Facebook o sucedáneos, que se te llame para ver si John Doe ha visitado páginas como Facebook. Al revisar, descubres que el empleado ha visitado páginas conocidas por albergar pornografia infantil, fraude fiscal, etc. Es tu deber denunciarlo a la ley.

---

## Gestión de un caso forense

## Puntos clave
- La bitácora y una línea temporal son imprescindibles, especialmente en la fase de análisis.  
- Registrar todo lo realizado en el análisis y en la recuperación.  
- Usar una estructura de carpetas cronológica y ordenada.  
- Demostrar cada paso con fotos o capturas.  
- Herramientas de referencia: Oxygen Forensics, Belkasoft, XRY.

---

## Un equipo de forenses
- Evita compartir datos sensibles en nubes públicas.  
- Alternativas recomendadas: File Browser o Nextcloud para nubes privadas.  
- Recuerda: la nube pública es cómoda… hasta que deja de serlo.

---

## Tipos de peritos
- Perito judicial: designado por el propio tribunal.  
- Perito de parte: contratado por alguna de las partes del conflicto; puede estar sesgado.  
- Perito tercero o dirimente: interviene cuando hay conflicto entre peritos; lo nombra el juez.

---

## Habilidades de los peritos
- Aseguramiento de la escena.  
- Recolección y preservación de pruebas.  
- Manejo de la cadena de custodia.  
- Análisis técnico y elaboración de dictámenes.  
- Conocimientos legislativos.  

---

# Eliminación y recuperación de información

## Discos HDD
El borrado de datos puede hacerse de varias formas:

### Eliminación normal
- “Eliminar” un archivo no lo elimina realmente.  
- Se elimina el enlace en la tabla del sistema de archivos; los datos siguen ahí.  
- Son recuperables fácilmente.

### Borrado seguro o saneado
- Sobrescribe los bits con datos aleatorios.  
- Herramientas: `wipe`, `shred`, `scrub`.  
- Puede realizar varias pasadas, lo que hace la recuperación prácticamente imposible.

### Destrucción física
- Aplicable cuando necesitas que el disco deje de existir de verdad.  
- Técnicas: romper, perforar, rayar (con cariño no, con ganas).  
- Los HDD están sellados herméticamente, pero eso no evita que un martillo haga su magia.

### Recuperación de datos
- Depende del sistema de archivos (FAT/NTFS/ext).  
- Cuanto mayor sea el disco, más lenta la recuperación.  
- Herramientas distintas recuperan resultados distintos.

Siempre que hagas un proceso de borrado, realiza un informe. Sin informe, solo has borrado “porque sí”.

---

## Discos SSD
Los SSD funcionan de forma diferente:

- Tienen TRIM, que mueve los datos internamente.  
- No se puede sobrescribir un sector concreto como en un HDD.  
- Para un borrado seguro suele ser necesario borrar todo el disco completo.  
- Existen herramientas y comandos específicos para ello.

---

# Métodos de uso

## Recuva (Windows)
Aplicación GUI (interfaz gráfica).

Uso básico:  
1. Instalar y abrir Recuva.  
2. Elegir el tipo de archivo a recuperar.  
3. Seleccionar ubicación.  
4. Activar “Deep Scan” si es necesario.  
5. Recuperar los resultados.

---

## PhotoRec (Linux / Windows / macOS)
Funciona en terminal con menú interactivo.

Comando básico:
```bash
sudo photorec
```

Pasos:
1. Elegir disco.  
2. Elegir partición.  
3. Elegir sistema de archivos (normalmente “Other”).  
4. Escoger Free o Whole.  
5. Seleccionar carpeta donde guardar los archivos.

---

## Foremost (Linux)

Comando básico:
```bash
sudo foremost -i /dev/sdX -o /ruta/salida
```

Ejemplos  
Recuperar desde imagen:
```bash
sudo foremost -i disco.img -o output/
```

Recuperar solo JPG y PDF:
```bash
sudo foremost -i /dev/sdX -o output/ -t jpg,pdf
```

---

## Scalpel (Linux)

Habilitar tipos de archivo:
```bash
sudo nano /etc/scalpel/scalpel.conf
```
Quitar el `#` de los tipos que quieras recuperar.

Comando básico:
```bash
sudo scalpel /dev/sdX -o output/
```

Desde imagen:
```bash
sudo scalpel disco.img -o output
```

---

# Advertencia importante (Borrado SSD)
Los comandos de `hdparm` pueden borrar todo el contenido del disco de forma irreversible.

En serio: revisa el disco dos veces. O tres. Tu futuro yo te lo agradecerá.

### 1. Comprobar soporte de Secure Erase
```bash
sudo hdparm -I /dev/sdX
```

### 2. Ver estado de seguridad
```bash
sudo hdparm -I /dev/sdX | grep -i security
```

Si aparece “frozen”, no podrás borrarlo.

### 3. Establecer contraseña temporal
```bash
sudo hdparm --user-master u --security-set-pass pwd /dev/sdX
```

### 4. Ejecutar Secure Erase
```bash
sudo hdparm --user-master u --security-erase pwd /dev/sdX
```

### 5. Secure Erase Enhanced
```bash
sudo hdparm --user-master u --security-erase-enhanced pwd /dev/sdX
```

### 6. Verificar desbloqueo
```bash
sudo hdparm -I /dev/sdX | grep -i security
```

---

# Resumen rápido

| Acción | Comando |
|-------|---------|
| Ver soporte de borrado | `hdparm -I /dev/sdX` |
| Poner contraseña | `hdparm --security-set-pass pwd /dev/sdX` |
| Secure Erase | `hdparm --security-erase pwd /dev/sdX` |
| Secure Erase Enhanced | `hdparm --security-erase-enhanced pwd /dev/sdX` |

---

# Ver los discos del sistema (Linux)

### 1. Listar discos y particiones
```bash
lsblk
```

### 2. Ver detalles completos
```bash
sudo fdisk -l
```

---

# Montar un disco en Linux

### Crear el punto de montaje
```bash
sudo mkdir /mnt/mi_disco
```

### Montar la partición
```bash
sudo mount /dev/sdb1 /mnt/mi_disco
```

### Desmontar
```bash
sudo umount /mnt/mi_disco
```

### Montaje especificando sistema de archivos
```bash
sudo mount -t ext4 /dev/sdb1 /mnt/mi_disco
```
