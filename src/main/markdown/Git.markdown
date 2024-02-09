
ChatGPT
Hier ist ein Cheat-Sheet für Git, das die grundlegenden Befehle und deren Verwendung zusammenfasst:

1. Konfiguration
   git config --global user.name "Your Name": Setze deinen Benutzernamen für Git.
   git config --global user.email "youremail@example.com": Setze deine E-Mail-Adresse für Git.
   git config --list: Zeige die Konfigurationsoptionen für Git an.
2. Repository erstellen
   git init: Initialisiere ein neues Git-Repository im aktuellen Verzeichnis.
   git clone <repository-url>: Klone ein vorhandenes Repository von einer URL.
3. Änderungen verfolgen
   git status: Zeige den Status der Arbeitskopie und des Index an.
   git add <file>: Füge Änderungen einer Datei zum Index hinzu.
   git add .: Füge alle Änderungen im aktuellen Verzeichnis zum Index hinzu.
   git reset <file>: Entferne eine Datei aus dem Index (unstage).
   git commit -m "Commit message": Committe die Index-Änderungen mit einer Nachricht.
4. Branches
   git branch: Zeige die Liste der Branches im Repository an.
   git branch <branch-name>: Erstelle einen neuen Branch.
   git checkout <branch-name>: Wechsle zu einem vorhandenen Branch.
   git checkout -b <branch-name>: Erstelle und wechsle zu einem neuen Branch.
   git merge <branch-name>: Führe Änderungen aus einem anderen Branch in den aktuellen Branch ein.
   git branch -d <branch-name>: Lösche einen Branch.
5. Zusammenarbeit
   git remote add origin <repository-url>: Füge ein entferntes Repository als "origin" hinzu.
   git push -u origin <branch-name>: Lade lokale Commits in das entfernte Repository hoch.
   git pull origin <branch-name>: Aktualisiere die lokale Arbeitskopie mit Änderungen aus dem entferten Repository.
   git fetch origin: Lade Änderungen aus dem entfernten Repository herunter, ohne sie zusammenzuführen.
   git clone <repository-url>: Klone ein Repository von einer URL.
6. Rückgängig machen
   git reset --hard HEAD: Setze den Arbeitsbereich und den Index auf den letzten Commit zurück.
   git checkout -- <file>: Verwerfe lokale Änderungen in einer Datei und stelle den letzten Commit wieder her.
   git revert <commit-hash>: Erzeuge einen neuen Commit, der die Änderungen des angegebenen Commits rückgängig macht.
7. Historie
   git log: Zeige die Liste der Commits an.
   git log --oneline: Zeige die Commit-Historie in einer kompakten Form an.
   git diff: Zeige die Unterschiede zwischen dem Arbeitsbereich und dem Index an.
   git diff HEAD: Zeige die Unterschiede zwischen dem Arbeitsbereich und dem letzten Commit an.
8. Tags
   git tag: Zeige die Liste der Tags an.
   git tag <tag-name>: Erstelle einen neuen Tag für den aktuellen Commit.
   git tag -a <tag-name> -m "Tag message": Erstelle einen annotierten Tag mit einer Nachricht.
   git push origin <tag-name>: Lade einen Tag in das entfernte Repository hoch.
   git push --tags: Lade alle Tags in das entfernte Repository hoch.
   Das sind nur einige der häufigsten Git-Befehle und ihre Verwendung. Es gibt viele weitere Befehle und Optionen, die in verschiedenen Situationen nützlich sein können. Es ist wichtig, sich mit den Grundlagen von Git vertraut zu machen und bei Bedarf die Dokumentation oder Online-Ressourcen zu konsultieren.