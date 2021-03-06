# Autocrackeo
Script en python que automatiza el uso del hashcat para crackear contraseñas


## Requisitos
Probado en windows/linux con python 3.6.3
* [python3.6](https://www.python.org/downloads/)
* [hashcat](https://github.com/hashcat/hashcat)

## Manual de usuario

### Por dónde empezar

1. Especifica el path al ejecutable de hashcat y las opciones de rendimiento en el archivo de configuración del equipo "host-config.json", por ejemplo:
```
{
	"executable": "hashcat64.exe",
	"resources": {
		"resource_level": "low",
		"resource_low": "--force",
		"resource_high": "-w 3"
	}
}
```

2. Prueba cualquiera de los comandos del apartado *Ejemplos* de más abajo, por ejemplo:
Ejecutar:
```
python3.6 autocrackeo.py -m 1000 hashes\test.hash --config config\quick_test.json --extra-params="--username"
```
Sólo ver los resultados:
```
python3.6 autocrackeo.py -m 1000 hashes\test.hash --config config\quick_test.json --extra-params="--username" --just-results
```

### Personalización

1. Introduce archivos con hashes en el directorio hashes.
2. Introduce archivos de diccionarios, reglas y máscaras en los directorios wordlists/, rules/ y masks/ respectivamente.
3. Modifica el archivo de configuración host-config.json para tu entorno y necesidades.
	* **Presta atención al valor del ejecutable y de la opción de recursos**.
4. Modifica los archivos de configuración de ataques a tu gusto.
	* Lista los archivos de diccionarios, reglas y máscaras que quieras utilizar en este caso.
	* Define los modos ataque que quieras lanzar con sus parámetros correspondientes.
		* La idea es tener varios archivos config.json (fast.json, basic.json, full.json...) que se ajusten a la velocidad/eficiencia que se requiera en cada momento.
		* En config\test.json hay múltiples ejemplos del formato requerido en cada tipo de ataque.
4. Ejecuta el programa: Durante la ejecución...
	* En plaintext_passwords.txt se irán almacenando las contraseñas en texto plano.
	* Se muestra por pantalla la ejecución del hashcat, por lo que se puede interactuar con él:
		* **s**: mostrar estado (status) / también sirve el "Enter"
		* **p**: pausar (pause)
		* **r**: reanudar (resume)
		* **b**: saltarse fases de un mismo ataque (bypass)
		* **q**: saltarse un ataque completo (quit)

Nota: El tiempo que tarde dependerá de muchos factores como el número de hashes, el tipo de hash, el tamaño de los diccionarios, la capacidad del equipo, etc.

### Ayuda
Para ver todas las opciones: `python3.6 autocrackeo.py -h`

### Ejemplos
```
python3.6 autocrackeo.py -m "NTLM" hashes\test.hash -c config\quick_test.json
python3.6 autocrackeo.py -m 1000 hashes\test.hash -c config\quick_test.json
python3.6 autocrackeo.py -m 1000 hashes\test.hash -c config\fast.json
python3.6 autocrackeo.py -m 1000 hashes\test.hash -c config\basic.json
python3.6 autocrackeo.py -m 1000 hashes\test.hash -c config\full.json
python3.6 autocrackeo.py -m 1000 hashes\test_user_hash_format.hash -c config\test.json -e=“--username”
python3.6 autocrackeo.py -m 1000 hashes\test_only_hash_format.hash -c config\one_word_per_hash.json

python3.6 autocrackeo.py -m 1000 hashes\test.hash -c config\quick_test.json -e=“--username” --just-results
```

## Organización
El proyecto está dividido por directorios de distintos recursos. Aunque en ningún momento se restringe completamente a seguir esta estructura. Los directorios de hashes, diccionarios, reglas, máscaras y resultados, se pueden especificar como parámetros de entrada o en la configuración json, por lo que se pueden modificar o unificar perfectamente.

* En el directorio **hashes/** se almacenaran los archivos de texto que contengan hases.
* En el directorio **wordlists/** se almacenaran los diccionarios que contengan palabras o frases susceptibles a aparecer en contraseñas.
* En el directorio **rules/** se almacenaran los archivos con reglas.
* En el directorio **masks/** se almacenaran los archivos con máscaras.
* En el directorio **results/** se almacenarán ciertos archivos utilizados por hashcat e irán apareciendo los hashes crackeados, entre otros.
* En el directorio **config/** se almacenarán los archivos en formato json que contienen la configuración de opciones de rendimiento, lista de archivos de diccionario/reglas/máscaras a utilizar, ataques a ejecutar...
* En el directorio **src/** está el código fuente del programa.
* En el directorio **docs/** se almacenarán archivos de interés relacionados con el proyecto:
	* changelog.md: aquí se irán indicando los cambios realizados y las nuevas ideas
	* Tutorial de crackeo (para hashcat).md: aquí he reunido los conceptos y ejemplos del hashcat que me han sido de utilidad para realizar este proyecto.

## Autora
* **Eneritz Azqueta** → proyecto realizado como Auditora en **S21sec**