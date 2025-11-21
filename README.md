Perfecto.
Aquí tienes **el Markdown RAW**, sin bloques adicionales, **listo para copiar y pegar directamente en un archivo `.md`**.

---

````markdown
# Borrado de datos  
Evan Silva Gonzalez

## Índice
- [Los peritos y su trabajo](#los-peritos-y-su-trabajo)  
- [Gestión de un caso forense](#gestión-de-un-caso-forense)  
- [Puntos clave](#puntos-clave)  
- [Un equipo de forenses](#un-equipo-de-forenses)  
- [Tipos de peritos](#tipos-de-peritos)  
- [Habilidades de los peritos](#habilidades-de-los-peritos)  
- [Eliminación y recuperación de información](#eliminación-y-recuperación-de-información)  
- [Discos SSD](#discos-ssd)  
- [Metodos de uso](#metodos-de-uso)  
- [Recuva (Windows)](#recuva-windows)  
- [PhotoRec (Linux / Windows / macOS)](#photorec-linux--windows--macos)  
- [Foremost (Linux)](#foremost-linux)  
- [Scalpel (Linux)](#scalpel-linux)  
- [ADVERTENCIA IMPORTANTE (Borrado SSD)](#advertencia-importante-borrado-ssd)  
- [Ver los discos del sistema](#ver-los-discos-del-sistema-linux)  
- [Montar un disco en Linux](#montar-un-disco-en-linux)

# Resumen del ejercicio actividad de borrado permanente.

## Los peritos y su trabajo
Los peritos son una parte importante de procesos de recogida de información, existiendo dos tipos, corporativos y judiciales o legislativos.  
Es importante comprender que los procesos por los que se evalua la información para cada tipo de proceso es diferente.

- En los corporativos, todo es mas “Laxo”, los limites y la información que quiere recogerse suele no necesitar una solidez judicial, es decir, temas como revisar correos o ver algún log que indique que un empleado ha visitado alguna página web que no debia según los estatutos de la empresa.  
- En los judiciales todo requiere mas rigurosidad. NO se puede acceder a la información directamente, solo a través de clonados en solo lectura, las pruebas originales deben estar sin adulterar o es probable que pierdan validez en el juicio.

Mucho mas importante es la documentación, un perito debe siempre anotar sus pasos y dejar un rastro de sus acciones, toda prueba que recabe ha de ser reproducible y debe estar regisrada. Las pruebas de un perito.

## Gestión de un caso forense

## Puntos clave
- La vitácora y una linea temporal son imprescindibles, se toman en la fase de analisis.
- Notas de lo que se ha hecho, tanto en la fase de analsisis como en la fase de recuperación de datos.
- Sistema de directorio/carpetas cronologicamente.
- Ser ordenado.
- Demostrar la investigación con fotos.
- Oxygen Forensics, Belkasoft, XRY son referentes en forma de herramientas forenses.

## Un equipo de forenses
- Cuidado con utilizar herramientas de la nube para compartir información, File Browser sirve para compartir datos en nubes propias. Nextcloud tambien puede crear una nube propia. Ser precabido de la nube publica porque pueden haber ataques.

## Tipos de peritos
- Perito judicial: contratado por parte del organismo en si. El juéz.
- Perito de parte: contratado por una parte, son menos imparciales. Y pueden no indagar dónde no se interese.
- Perito tercero o dirimente: en caso de discrepancia grave entre varios peritos, desempatan. Lo nombra el juez en caso de ser judicial, en arbitrajes entre empresas, lo seleccionan entre ambas partes.

## Habilidades de los peritos
- Aseguramiento de la escena  
- Recolección de pruebas  
- Preservación de pruebas  
- Manejo de la cadena de custodia  
- Análisis de evidencias  
- Generación de dictámenes  
- Conocimiento legislativo  

# Eliminación y recuperación de información

## Discos SSD
El borrado de datos tiene varios tipos, la eliminación y el borrado seguro sanetizado y la destrucción física.

- La eliminación es simplemente clickar y darle a eliminar, los sistemas suelen NO borrar los archivos, si no que desenlazan las celdad de inicio/fin de archivo de la tabla de memoria, lo que hace que el sistema crea que no hay nada, y a futuro escriba por encima, son RECUPERABLES.  
- La eliminación seguro o sanetizado lo que hace es, en primer lugar, sobreescribir sobre los bits de memoria información aleatoria, comandos como wipe o shred hacen que la información quede totalmente inutilizada en los bits literales del disco y luego poder eliminarlos. El comando scrub hace lo mismo, pero se puede hacer que haga varias pasadas, haciéndo que sea imposible.  
- La eliminación en físico es literalmente romper, rallar, destrozar el disco físico. Los discos HDD están sellados de manera hermética.  
- La recuperación en estos casos es dependiente del tipo de sistema de guardado de archivos (FAT/NTFS – sdb1/sdb2). En los discos grandes, las herramientas de recuperado serán lentas y habrá muchos datos intrinsecos temporales. En discos pequeños, la recuperación es mas guiada y eficiente, asi como exitosa.  
- Dependiendo de la herramienta, se recuperarán diferentes archivos en menor o mejor medida.  

Es importante a la hora de hacér un borrado, realizar un informe, siempre.

## Discos SSD
El borrado de datos en los discos SSD son ligeramente diferentes.

- Los discos SSD tienen triming, por lo que mueven la memoria a traves de todo el disco ssd, y no funcionan como las celdas de un HDD. Hay que tilizar herramientas diferentes para ELIMINAR totalmente el disco, hay herramientas que sobre-escriben y eliminan todo el disco SSD. No es eficiente ni util borrar ciertas partes, asi que por defecto se borra todo el disco de alante a atrás.

# Metodos de uso

## Recuva (Windows)
Recuva es principalmente gráfico (GUI), así que su “comando básico” es simplemente ejecutarlo.

**Uso básico**  
1. Instalar y abrir Recuva.  
2. El asistente pregunta qué quieres recuperar → elige All Files o el tipo deseado.  
3. Seleccionar ubicación a analizar.  
4. Activar Deep Scan si quieres un análisis más profundo.  
5. Recuperar los archivos encontrados.

Recuva no se usa normalmente por comandos en consola.

## PhotoRec (Linux / Windows / macOS)
PhotoRec funciona por menú interactivo en terminal.

**Comando básico**
```
sudo photorec
```

**Pasos dentro del programa**
1. Selecciona el disco a analizar.  
2. Selecciona la partición (o “Whole disk”).  
3. Elige el tipo de sistema de archivos (normalmente "Other").  
4. Selecciona Free o Whole.  
5. Elige carpeta donde guardar los archivos recuperados.  

## Foremost (Linux)

**Comando básico**
```
sudo foremost -i /dev/sdX -o /ruta/salida
```

**Ejemplos**
Recuperar desde imagen:
```
sudo foremost -i disco.img -o output/
```

Recuperar solo JPG y PDF:
```
sudo foremost -i /dev/sdX -o output/ -t jpg,pdf
```

## Scalpel (Linux)

### Habilitar tipos de archivos
Editar:
```
sudo nano /etc/scalpel/scalpel.conf
```

→ Quitar el `#` de las extensiones que quieras recuperar (jpg, pdf, etc.)

### Comando básico
```
sudo scalpel /dev/sdX -o output/
```

Desde una imagen:
```
sudo scalpel disco.img -o output
```

# ADVERTENCIA IMPORTANTE (Borrado SSD)
Los comandos de hdparm pueden borrar todo el contenido de un disco de forma irreversible.  
Asegúrate al 100% de que el disco que vas a borrar es el correcto (NO la partición donde estás trabajando).

### 1. Ver si el disco soporta Secure Erase
```
sudo hdparm -I /dev/sdX
```

Buscar líneas como:
- supported: enhanced erase  
- supported: security erase  

### Ver el estado de seguridad del disco
```
sudo hdparm -I /dev/sdX | grep -i security
```

Si dice *frozen*, no podrás borrarlo.

### 3. Poner una clave temporal (requerido por el estándar ATA)
```
sudo hdparm --user-master u --security-set-pass pwd /dev/sdX
```

### 4. Ejecutar Secure Erase (borrado seguro estándar)
```
sudo hdparm --user-master u --security-erase pwd /dev/sdX
```

### 5. Secure Erase Enhanced
```
sudo hdparm --user-master u --security-erase-enhanced pwd /dev/sdX
```

### 6. Verificar desbloqueo
```
sudo hdparm -I /dev/sdX | grep -i security
```

# Resumen rápido

| Acción | Comando |
|-------|---------|
| Ver soporte de borrado | `hdparm -I /dev/sdX` |
| Poner contraseña | `hdparm --security-set-pass pwd /dev/sdX` |
| Secure Erase | `hdparm --security-erase pwd /dev/sdX` |
| Secure Erase Enhanced | `hdparm --security-erase-enhanced pwd /dev/sdX` |

# Ver los discos del sistema (Linux)

### 1. Listar discos y particiones
```
lsblk
```

### 2. Ver detalles completos
```
sudo fdisk -l
```

# Montar un disco en Linux

### Crear el punto de montaje
```
sudo mkdir /mnt/mi_disco
```

### Montar la partición
Ejemplo para `/dev/sdb1`:
```
sudo mount /dev/sdb1 /mnt/mi_disco
```

### Desmontar
```
sudo umount /mnt/mi_disco
```

### Montaje opcional con tipo de sistema de archivos
```
sudo mount -t ext4 /dev/sdb1 /mnt/mi_disco
```
````

---
