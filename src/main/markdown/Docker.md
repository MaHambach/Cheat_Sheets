Dockerfile Example:
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

In der "pom.xml" kann mann in <build> das Tag <finalName> setzen.Bsp.:
```
<finalname>Currywurst</finalname>
```

Bevor mit Docker ein Image gebaut werden kann, mit "docker build", muss das Projekt unter maven -> package gebaut werden.


Man kann das Frontend über Vite bauen: In ???.json auf "build" und nicht "dev". Das ergebnis landet dann im dist-Ordner im Frontend.

Diesen kann man dann in den resources Ordner im backend kopieren.

Um das Image mit auf GitHub zu schicken: docker build -t "githubname"/"name des Image".

docker login