Ejecicio A (GIT)
Intensificiación colaborativa
1.	Realice un fork de este repositorio con el nombre EGC2324-turno31-"uvus".

2.	Clone el repositorio del cual ha hecho el fork. 
/ Git clone url

3.	Cree una nueva rama llamada egc_test en el repositorio.
/ cd REPO
git branch egc_test

4.	"Salte" a la rama recien creada. 
/ Git chekcout egc_test
(git chekcout -b egc_test      crea y salta)

5.	En el código de DECIDE del repositorio existe un error. Identifique el error ejecutando en su máquina el código.

6.	Cree una "issue" en el fork del repositorio para reportar el error según lo visto en clase.
   Settings - Feautures - issues enabled

7.	Realice las modificaciones necesarias para corregir el error y haga commit de los cambios en la rama egc_test.
/ Git add .
Git commit -m “mensaje”

8.	Mediante una pull request, fusione en la rama master/main del repositorio los cambios de la rama de egc_test y asocielo a la issue anterior.
    / git push -u origin nombre_de_tu_rama
   Closes #1 (issue)	

9.	Refleje los cambios del repositorio local en el repositorio remoto que creó en el primer paso.
/
git checkout main
git pull origin main
git merge egc_test
Git push origin main
---
Balance técnico-organizativo

10.	Cree una rama rv1 y haga tres cambios en el fichero decide/visualizer/templates/visualizer/visualizer.html, de manera que cada cambio sea un commit diferente. 
/ Git checkout -b rv1

Git add .
Git commit -m “mensaje”

11.	Deshaga los dos últimos cambios de manera soft. 
/ git reset --soft HEAD~2

(Lo puedo comprobar con git log --oneline)
---
Balance técnico-organizativo (Turno mañana) https://github.com/OrlandoLAB/EGC2324-turno11-orllabled/blob/main/Examen11.md

10.	Cree dos ramas rq1 y rq2, haga modificaciones distintas en el fichero requirements.txt en las que se de un conflicto en alguna linea. 
/ git checkout -b rq1
(modificamos el archivo)
git add requirements.txt
git commit -m "Modificación en rq1"

git checkout -b rq2
(Modificamos)
git add requirements.txt
git commit -m "Modificación en rq2" 

11.	Fusione, resuelva el conflicto e integre los cambios en egc_test. 
/ git checkout egc_test
git merge rq1
	git merge rq2
	
	(Resolver el conflicto que salta)
	git add requirements.txt
	git commit -m "Resolución de conflictos entre rq1 y rq2"
	git status
git push origin egc_test

---

Balance técnico-organizativo (Turno 16:30)
https://github.com/laurolmer/EGC-2324-1630/blob/main/Examen32.md

10.	Cree una rama rv1 y haga tres cambios en el fichero decide/visualizer/templates/visualizer/visualizer.html, de manera que cada cambio sea un commit diferente. 

/ git checkout -b rv1
[Modificar +
git add decide/visualizer/templates/visualizer/visualizer.html
git commit -m "Agregar un nuevo título al visualizador"] x3


11.	Deshaga los dos últimos cambios de manera soft. 
/ git reset --soft HEAD~2

---

Balance técnico-organizativo (Turno 18:30)
https://github.com/alvarobernal2412/EGC2324-turno42-alvbercau/blob/main/Examen42.md

10.	Cree una rama ch1 y haga en ella 3 commits con cambios en el/los fichero/s de su preferencia. 

/ git checkout -b ch1
[Modificar +
git add decide/visualizer/templates/visualizer/visualizer.html
git commit -m "Agregar un nuevo título al visualizador"] x3

11.	Muévase a egc_test e integre únicamente los cambios relativos al segundo commit de la rama ch1, mediante cherry-pick. 

/ git checkout egc_test

Ahora, necesitas obtener el hash del segundo commit de la rama ch1:
git log ch1

Busca el hash del segundo commit. Usa el comando cherry-pick para aplicar ese commit a egc_test:
git cherry-pick hash1234

---

Intensificación técnica
12.	Realice un cambio en una línea del README.md. Genere un parche con este cambio. 
/ Git add README.md
Git diff HEAD > cambio_readme.patch

13.	Cambie a una rama diferente y aplique el parche en esa rama. 
/ Git chekout -b rama
Git apply cambio_readme.patch

14.	Haga commit de los cambios realizados. 
/ git add README.md
git commit -m "mensaje"

---

Intensificación técnica (Turno mañana)
12.	Traslade un cambio específico de la rama egc_test a la rama master/main utilizando cherry-pick.

/ git checkout egc_test
git log (visualizamos el historial de commits para identificar el hash que queramos trasladar) (Anota el hash (los primeros 7 caracteres son suficientes) del commit que deseas trasladar.)
git checkout master
git cherry-pick <commit-hash>
[Si hay conflictos: 
(Resolvemos)
git add <archivo-con-conflicto>
git cherry-pick  --continue]

---

Intensificación técnica (Turno 18:30)
12.	Cree una nueva rama rbs y haga en ella 5 commits (a,b,c,d,e). 

/ git checkout -b rbs

git add archivo.txt
git commit -m "a: Primer commit"
…

13.	Utilice rebase interactivo para combinar los commits b, c y d en uno solo, de manera que el historial final contenga 3 commits: a, bcd, e.  (Incluya las capturas que sean necesarias para demostrar el proceso).

/ git rebase -i HEAD~5

Se abrirá un editor de texto: 

pick 1234567 a: Primer commit
pick 2345678 b: Segundo commit
pick 3456789 c: Tercer commit
pick 4567890 d: Cuarto commit
pick 5678901 e: Quinto commit

Combinamos b c d:

pick 1234567 a: Primer commit
squash 2345678 b: Segundo commit
squash 3456789 c: Tercer commit
squash 4567890 d: Cuarto commit
pick 5678901 e: Quinto commit

Guardamos y cerramos

Verificamos: git log --oneline

**[Número de commits: Si usas HEAD~5, incluirás todos los commits:
HEAD (e): Quinto commit
HEAD~1 (d): Cuarto commit
HEAD~2 (c): Tercer commit
HEAD~3 (b): Segundo commit
HEAD~4 (a): Primer commit

Uso de HEAD~4: Si utilizaras HEAD~4, accederías solo a los commits:
HEAD (e)
HEAD~1 (d)
HEAD~2 (c)
HEAD~3 (b)
Esto omitiría el commit a]

---

Ejercicio B (GITHUB ACTIONS)
Intensificiación colaborativa

1.	Modifique el workflow django.yml para pasar las pruebas exclusivamente del módulo voting. (Turno mañana)

Localizo: 
- name: Run tests
  run: |
    cd decide
    ./manage.py test –keepdb

Modifico:
- name: Run tests for voting module
  run: |
    cd decide
    ./manage.py test voting --keepdb

2.	Modifique el workflow django.yml para que utilice la versión de postgres 15. 

services:
  postgres:
    image: postgres:14 //// cambiamos 14 por 15
    ports:
      - 5432:5432
    env:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: test_db
    options: >-
      --health-cmd pg_isready
      --health-interval 10s
      --health-timeout 5s
      --health-retries 5

3.	Prepare el workflow para que en lugar de ejecutarse sobre la última versión de ubuntu, lo haga explícitamente sobre la versión 22.04. 

Cambiamos runs-on: ubuntu-latest por runs-on: ubuntu-22.04

4.	Haga commit y push de los cambios realizados. 
/ git add .github/workflows/django.yml
git commit -m "mensaje"
git push

5.	Verifique el correcto funcionamiento del workflow.
Verificar en Github en la pestaña actions

Balance técnico-organizativo (Turno 18:30)

1.	Modifique el workflow django.yml para que utilice la versión de python 3.11. 

- name: Set up Python 3.11
  uses: actions/setup-python@v4
  with:
    python-version: '3.11'  

2.	Prepare el workflow para que la integración con codacy constituya un nuevo job llamado cobertura.

jobs:
  cobertura:

    runs-on: ubuntu-latest


Balance técnico-organizativo
5.	Configure el workflow django.yml para lanzar las pruebas con dos versiones de python diferentes (3.10.12 y 3.11). 

jobs:
  test:
    strategy:
      matrix:
        python-version: [3.10] / Cambio por [3.10.12, 3.11]

6.	Haga commit y push de los cambios realizados. 
/ git add .github/workflows/django.yml
git commit -m "mensaje"
git push

7.	Verifique el correcto funcionamiento del workflow. 

Balance técnico-organizativo (Turno 198:30)
5.	Configure el workflow django.yml para lanzar las pruebas con dos versiones de postgres diferentes (14.9 y 15). 

strategy: 
matrix: 
postgres-version: [14.9, 15] # Añadido para definir versiones de Postgres 
services: 
postgres: 
image: postgres:${{ matrix.postgres-version }}

Intensificación técnica
8.	Configure DECIDE para generar releases automáticas mediante el uso de workflows. 
Hay que poner todo esto (MACARRA):

name: Release

on:
  push:
    tags:
      - 'v*'

jobs:
  release:
    runs-on: ubuntu-22.04

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Create GitHub Release
        uses: actions/create-release@v1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          tag_name: ${{ github.ref }}
          release_name: Release ${{ github.ref }}
          body: |
            Automatic release based on the tag ${{ github.ref }}.
          draft: false
          prerelease: false

9.	Haga commit y push de los cambios realizados.
/ git add .github/workflows/release.yml
git commit -m "mensaje"
git push

10.	Verifique que se ha creado una release. 
/ git tag v1.0.0
git push origin v1.0.0
Comprobamos en la pestaña Releases de Github si funciona el paso 8 y se ha generado la reléase automática.

---

EJERCICIO C (DOCKER)
Intensificiación colaborativa
1.	Realice los cambios necesarios en los archivos de docker para que despliegue este repositorio. 
Para desplegar el proyecto usando Docker, debes asegurarte de que el Dockerfile y el archivo docker-compose.yml estén correctamente configurados.
•	Dockerfile: Asegúrate de que el Dockerfile esté correctamente configurado para el entorno de tu aplicación (por ejemplo, Django, Flask, etc.). Aquí hay un ejemplo básico para una aplicación Django:
dockerfile
Copiar código
Usa una imagen base oficial de Python
FROM python:3.11

Establece el directorio de trabajo en el contenedor
WORKDIR /app

Copia los archivos del proyecto al contenedor
COPY . /app

Instala las dependencias necesarias
RUN pip install -r requirements.txt

Expone el puerto que usará el servidor web
EXPOSE 8000

Comando para iniciar la aplicación
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "myproject.wsgi:application"]
•	docker-compose.yml: Aquí asegúrate de tener los servicios correctos, como la base de datos y la aplicación web. Por ejemplo:
yaml
Copiar código
version: '3.9'

services:
  web:
    build: .
    command: gunicorn --bind 0.0.0.0:8000 myproject.wsgi:application
    volumes:
      - .:/app
    ports:
      - "8000:8000"
    depends_on:
      - db
  
  db:
    image: postgres:15
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydatabase
    ports:
      - "5432:5432"

2.	Haga commit de los cambios realizados. 
/ git add Dockerfile docker-compose.yml
git commit -m "mensaje"
git push

Balance técnico-organizativo
3.	Realice los cambios necesarios en la configuración de docker para que el servicio web lanzado mediante docker compose utilice 4 workers de gunicorn. 

•  En el Dockerfile, cambia el comando final:
CMD ["gunicorn", "--workers", "4", "--bind", "0.0.0.0:8000", "myproject.wsgi:application"]
•  En el docker-compose.yml, si prefieres modificarlo ahí, el comando debe verse como:
command: gunicorn --workers 4 --bind 0.0.0.0:8000 myproject.wsgi:application


4.	Haga commit y push de los cambios realizados. 

5.	Realice los cambios necesarios para que DECIDE sea accesible desde el puerto 8003 en docker. (Turno mañana)

Localizo:
ports:
  - "8000:80"

Cambio:
ports:
  - "8003:80"

Reinicio docker
docker-compose up --build

---

EJERCICIO D (VAGRANT)
Intensificiación colaborativa
1.	Realice los cambios necesarios en los archivos de Vagrant para que despliegue este repositorio. 

Abre el archivo Vagrantfile. Configura la máquina virtual para el entorno de desarrollo del proyecto. Aquí hay un ejemplo para un proyecto Django:
ruby
Copiar código
Vagrant.configure("2") do |config|
  Utilizar una box de Ubuntu 22.04
  config.vm.box = "ubuntu/bionic64"

  Configuración de red (red privada)
  config.vm.network "private_network", type: "dhcp"

  Definir la configuración de la máquina
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = 2
  end

  Provisión de la máquina
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y python3-pip python3-dev libpq-dev postgresql postgresql-contrib nginx
    pip3 install -r /vagrant/requirements.txt
  SHELL
end


Asegúrate de que los scripts de provisión instalen las dependencias necesarias para tu aplicación

2.	Haga commit de los cambios realizados. 
Balance técnico-organizativo

3.	Realice los cambios necesarios para que DECIDE se despliegue con Vagrant y sea accesible desde el sistema host en el puerto 8081. 
Modificar Vagrantfile:
config.vm.network "forwarded_port", guest: 80, host: 8081
vagrant up

4.	Haga commit y push de los cambios realizados. 

5.	Realice los cambios necesarios para que DECIDE se despliegue con Vagrant en el sistema host utilizando 4 núcleos de CPU y 4 GB de memoria RAM. (Turno mañana)

v.memory = 4096  # Asignar 4 GB de RAM
v.cpus = 4      # Asignar 4 núcleos de CPU

vagrant up
vagrant ssh (verifico recursos)


