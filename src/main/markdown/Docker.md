# Docker
## Wichtige Befehle
Here are some basic Docker commands and their meanings:

- `docker run --name some-mongo -p 37017:27017 -d mongo:latest`: Runs a container named "some-mongo" based on the "mongo:latest" image in the background mode and maps container port 27017 to host port 37017.

- `docker ps`: Shows a list of running containers.

- `docker ps --all`: Shows a list of all containers, including stopped ones.

- `docker start <container_id>`: Starts a stopped container.

- `docker stop <container_id>`: Stops a running container.

- `docker rm <container_id>`: Deletes a stopped container.

- `docker image rm <image_name>`: Deletes a Docker image.

- `docker images`: Shows a list of available images.

- `docker inspect <object_id>`: Displays detailed information about a Docker object (container or image).

- `docker image inspect <image_name>`: Displays detailed information about a specific image.

## Getting started
### 0. Frontend JAR
Das Frontend muss zuerst gebaut werden, bevor das Backend gebaut wird.

* Dazu in der `package.json` auf "build" und nicht "dev" klicken.
* Das Ergebnis landet dann im dist-Ordner im Frontend.
* Diesen kann man dann in den resources Ordner im backend kopieren und noch in "static" umbenennen.
* Das Frontend wird dann in der `index.html` Datei im resources Ordner geladen.

### 1. Name der JAR-Datei

In der `pom.xml` können wir den Namen des JAR-Files ändern:
```xml
<build>
    <finalName>Currywurst</finalName>
    ...
</build>
```

### 2. Dockerfile
* Der Dockerfile gibt an wie das Image gebaut wird. 
* Er muss sich im Hauptverzeichnis des Projekts befinden.
* Der Name des Dockerfiles ist "Dockerfile" ohne Dateiendung.

#### Dockerfile Beispiel:
```
FROM --platform=linux/amd64 openjdk:21
EXPOSE 8080
ADD backend/target/app.jar app.jar
ENTRYPOINT ["java", "-jar", "app.jar"]
```

FROM --platform=linux/amd64 openjdk:21
* Das Image wird für Linux erstellt.

EXPOSE 8080
* Bevorzugter Port des Images.

ADD backend/target/app.jar app.jar
* Relativer Pfad und Name für unsere Image-Datei.
* Das zweite "app.jar" sorgt dafür, dass irgendwas im Hauptverzeichnis landet.

Bevor mit Docker ein Image gebaut werden kann, mit "docker build", muss das Projekt unter maven -> package gebaut werden.

### 3. Backend-JAR
Vor dem Build muss über Maven eine JAR-Datei erstellt werden. 
* Dazu auf Maven und dann in Lifecycle auf "package".

### 4. Image bauen
Mit dem Befehl `docker build -t username/app:latest .` wird ein Image mit dem Namen "currywurst" gebaut.

* Der Befehl funktioniert nur, wenn er in dem gleichen Ordner wie das Dockerfile ausgeführt wird.
* `username` ist der Name des Docker-Accounts.
* Um das Image auf Docker Hub zu pushen, muss man angemeldet sein: `docker login`.

### 5. Image pushen
Um ein Image auf Docker Hub zu pushen, muss `docker push username/app:latest` ausgeführt werden.

* `username` ist der Name des Docker-Accounts.
* Das Image muss vorher gebaut worden sein.
* `username/app:latest` ist der Name des Images.

### 6. Image pullen
Um ein Image von Docker Hub zu pullen, muss `docker pull username/app:latest` ausgeführt werden.

* `username` ist der Name des Docker-Accounts.
* `username/app:latest` ist der Name des Images.

### 7. Container starten
Um einen Container zu starten, muss `docker run --name app -p 8080:8080 username/app:latest` ausgeführt werden.

* `--name app` gibt dem Container den Namen "app".
* `-p 8080:8080` mappt den Container-Port 8080 auf den Host-Port 8080.
* Hier kann man den Port auf dem der Container läuft ändern. Wird 0 angegeben wird ein zufälliger freier Port benutzt.
* `username/app:latest` ist der Name des Images.

## CD
### deploy.yml
Die `deploy.yml` Datei ist eine GitHub Actions Datei, die das Deployment auf einem Server automatisiert.

* Sie muss im `.github/workflows` Ordner liegen.
* Kann hier auch ohne workflows von GitHub erstellt werden.
* Es müssen noch die entsprechenden Secrets in den Repository-Einstellungen hinterlegt werden.
    * 

Beispiel:
```yml
name: "Deploy App"

on:
  push:
    branches:
      - main

jobs:
  build-frontend:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Build Frontend
        working-directory: frontend
        run: |
          npm install
          npm run build

      - uses: actions/upload-artifact@v4
        with:
          name: frontend-build
          path: frontend/dist/

  build-backend:
    runs-on: ubuntu-latest
    needs: build-frontend
    steps:
      - uses: actions/checkout@v4

      - uses: actions/download-artifact@v4
        with:
          name: frontend-build
          path: backend/src/main/resources/static

      - name: Set up JDK
        uses: actions/setup-java@v4
        with:
          java-version: '21' # must match the version in the pom.xml
          distribution: 'temurin'
          cache: 'maven'

      - name: Build with maven
        run: mvn -B package --file backend/pom.xml

      - uses: actions/upload-artifact@v4
        with:
          name: app.jar
          path: backend/target/app.jar # must match the finalName in the pom.xml

  push-to-docker-hub:
    runs-on: ubuntu-latest
    needs: build-backend
    steps:
      - uses: actions/checkout@v4

      - uses: actions/download-artifact@v4
        with:
          name: app.jar
          path: backend/target

      - name: Login to DockerHub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }} # must match the name of the Dockerhub account
          password: ${{ secrets.DOCKERHUB_PASSWORD }} # must match the password of the Dockerhub account

      - name: Build and push
        uses: docker/build-push-action@v5
        with:
          push: true
          tags: ${{ secrets.DOCKERHUB_TAG }} # Example: username/project:latest
          context: .

  deploy:
    name: deploy-to-render
    runs-on: ubuntu-latest
    needs: push-to-docker-hub
    environment:
      name: Capstone Project # Capstone Project name
      url: https://neuefische.de/ # Link to deployment
    steps:
      - name: Trigger Render.com Deployment
        run: |
          curl -X POST ${{ secrets.RENDER_DEPLOY }} #muss mit der url des Render Deployments übereinstimmen
```

### Secrets
In den Repository-Einstellungen müssen die folgenden Secrets hinterlegt werden:

* `DOCKERHUB_USERNAME`: Der Name des Docker-Accounts.
* `DOCKERHUB_PASSWORD`: Das Passwort des Docker-Accounts.
* `DOCKERHUB_TAG`: Der Name des Images.
* `RENDER_DEPLOY`: Die URL des Render Deployments.

## Render
Render ist eine vereinheitlichte Cloud, um alle Ihre Apps und Websites mit kostenlosen TLS-Zertifikaten, einem globalen CDN, DDoS-Schutz, privaten Netzwerken und automatischen Bereitstellungen aus Git zu erstellen und auszuführen.

Render ermöglicht es uns, unsere Webanwendung kostenlos mit unserem Docker-Image bereitzustellen. Der Nachteil ist, dass der Server bei Inaktivität heruntergefahren wird, was zu längeren Ladezeiten führt, wenn er erneut aufgerufen wird.

Einrichtung:

1. Registrieren Sie sich bei Render.
2. Erstellen Sie einen Webservice. 
3. Wählen Sie die Option zum Bereitstellen eines Docker-Images.
4. Geben Sie den Namen oder die URL Ihres Docker-Images auf Dockerhub ein. 
5. Wählen Sie einen Namen für Ihren Webservice. 
6. Wählen Sie die Free Tier-Option!
7. Webservice erstellen. 
8. Geben Sie die erforderlichen Umgebungsvariablen im Umgebungstab ein.


## Sonstiges
Man kann das Frontend über Vite bauen: In `package.json` auf "build" und nicht "dev" klicken. Das Ergebnis landet 
dann im dist-Ordner im Frontend.

Diesen kann man dann in den resources Ordner im backend kopieren.

Um das Image mit auf GitHub zu schicken: `docker build -t "githubname"/"name des Image" .`

docker login

`deploy.yml` erstellen im `.github/workflows` Ordner.

## Links:
https://docs.github.com/en/actions/publishing-packages/publishing-docker-images

