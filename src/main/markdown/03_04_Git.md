# Git
## 1. Konfiguration
* __git config --global user.name "Your Name":__ Setze deinen Benutzernamen für Git.
* __git config --global user.email "youremail@example.com":__ Setze deine E-Mail-Adresse für Git.
* __git config --list:__ Zeige die Konfigurationsoptionen für Git an.
## 2. Repository erstellen
* __git init:__ Initialisiere ein neues Git-Repository im aktuellen Verzeichnis.
* __git clone <repository-url>:__ Klone ein vorhandenes Repository von einer URL.
## 3. Änderungen verfolgen
* __git status:__ Zeige den Status der Arbeitskopie und des Index an.
* __git add <file>:__ Füge Änderungen einer Datei zum Index hinzu.
* __git add . :__ Füge alle Änderungen im aktuellen Verzeichnis zum Index hinzu.
* __git reset <file>:__ Entferne eine Datei aus dem Index (unstage).
* __git commit -m "Commit message":__ Committe die Index-Änderungen mit einer Nachricht.
## 4. Branches
* __git branch:__ Zeige die Liste der Branches im Repository an.
* __git branch <branch-name>:__ Erstelle einen neuen Branch.
* __git checkout <branch-name>:__ Wechsle zu einem vorhandenen Branch.
* __git checkout -b <branch-name>:__ Erstelle und wechsle zu einem neuen Branch.
* __git merge <branch-name>:__ Führe Änderungen aus einem anderen Branch in den aktuellen Branch ein.
* __git branch -d <branch-name>:__ Lösche einen Branch.
## 5. Zusammenarbeit
* __git remote add origin <repository-url>:__ Füge ein entferntes Repository als "origin" hinzu.
* __git push -u origin <branch-name>:__ Lade lokale Commits in das entfernte Repository hoch.
* __git pull origin <branch-name>:__ Aktualisiere die lokale Arbeitskopie mit Änderungen aus dem entferten Repository.
* __git fetch origin:__ Lade Änderungen aus dem entfernten Repository herunter, ohne sie zusammenzuführen.
* __git clone <repository-url>:__ Klone ein Repository von einer URL.
## 6. Rückgängig machen
* __git reset --hard HEAD:__ Setze den Arbeitsbereich und den Index auf den letzten Commit zurück.
* __git checkout -- <file>:__ Verwerfe lokale Änderungen in einer Datei und stelle den letzten Commit wieder her.
* __git revert <commit-hash>:__ Erzeuge einen neuen Commit, der die Änderungen des angegebenen Commits rückgängig macht.
## 7. Historie
* __git log:__ Zeige die Liste der Commits an.
* __git log --oneline:__ Zeige die Commit-Historie in einer kompakten Form an.
* __git diff:__ Zeige die Unterschiede zwischen dem Arbeitsbereich und dem Index an.
* __git diff HEAD:__ Zeige die Unterschiede zwischen dem Arbeitsbereich und dem letzten Commit an.
## 8. Tags
* __git tag:__ Zeige die Liste der Tags an.
* __git tag <tag-name>:__ Erstelle einen neuen Tag für den aktuellen Commit.
* __git tag -a <tag-name> -m "Tag message":__ Erstelle einen annotierten Tag mit einer Nachricht.
* __git push origin <tag-name>:__ Lade einen Tag in das entfernte Repository hoch.
* __git push --tags:__ Lade alle Tags in das entfernte Repository hoch.
   
Das sind nur einige der häufigsten Git-Befehle und ihre Verwendung. Es gibt viele weitere Befehle und Optionen, die in verschiedenen Situationen nützlich sein können. Es ist wichtig, sich mit den Grundlagen von Git vertraut zu machen und bei Bedarf die Dokumentation oder Online-Ressourcen zu konsultieren.