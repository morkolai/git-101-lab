README.md

# git 101 - lab

_This repo is as set of tasks related to a lecture on basic git._

_Clone this repo to proceed with the tasks._

## Oppgaver

### 0 Disclaimer

Noen av oppgavene bryter med det som er beste praksis og det som er realistisk i et indistruellt prosjekt. Dette er fordi oppgavenes poeng er å vise hvordan funksjonaliteten i git fungerer og at det er foskjellig hva folk mener er beste praksis.

### 1 - Staging Area

#### a\) Existing file

1. Kjør `git status` og se at du er på master/main branch, at working tree er clean og at det ikke er noe å comitt'e.
2. Åpne `EN.txt` og skriv noe i filen og lagre den.
3. Kjør `git status` og se at filen ligger under "not staged for commit", dette betyr at filen er registrert i git, men at endringene i den ikke er en del av neste commit.
4. Kjør `git add EN.txt`.
5. Kjør `git status` og se at filen nå ligger under "staged for commit", dette betyr at den blir en del av neste commit.
6. Kjør `git restore --staged EN.txt` for fjerne filen fra staging area.
7. Kjør `git status` for å verifisere handlingen.
8. Kjør `git restore EN.txt` for å sette filen tilbake til den tilstanden den var før du gjorde endringene.
9. Kjør `git status` og se at det er likt som i punkt 1.

##### b\) New file

1. Opprett en ny fil (med feks. `touch <filnavn>`).
2. Kjør `git status` - filen vil nå ligge under "untracked files", dette betyr at den ikke er registrert i git.
3. Kjør `git add <filnavn>`.
4. Kjør `git status` og se at filen er staget.
5. Kjør `git restore --staged <filnavn>` for å fjerne filen igjen fra staging.
6. Kjør `git status` for å se at filen er tilbake til "untracked files"
7. Kjør `git clean -f .` for å fjerne filen fra git og filsystemet.

### 2 - Commit and push

1. Kjør `git log` for å se historien til repositoriet.
2. Åpne `EN.txt`, skriv "oppgave 2" i filen og lagre den.
3. Kjør `git add *` for å stage endringen.
4. Kjør `git commit -m "oppgave 2"` for å commmit'e endringene lokalt.
5. Kjør `git log`. Du vil nå se at (HEAD -> main) ligger en commit foran (origin/main). Dette betyr at hodepekeren (der du ser på repositoriet) ikke er den samme tilstanden som repositoriet er i på GitHub.
6. Kjør `git push` før å sende dine endringer til remote repository.
7. Kjør `git log` for å set at origin/main og HEAD er på samme commit.

### 3 - Branching

1. Kjør `git status` og `git log` for å få oversikt over repositoriet.
2. Kjør `git checkout -b branch-1` for å opprette og bytte til grenen `branch-1`.
3. Lag en ny fil som heter "BRANCH-1.txt og commit den.
4. Kjør `git checkout -b branch-2` for å opprette og bytte til grenen `branch-2`. Denne grenen tar utgangspunkt i `branch-1`. 
5. Lag en ny fil som heter "BRANCH-2.txt og commit den.
6. Kjør `git log`, `git status` og `ls` for å se at alle endringene er i denne. branchen.
7. Kjør `git checkout -` for å skifte tilbake til forrige branch (branch-1).
8. Kjør `git log`, `git status` og `ls` for å se at endringene fra `branch-2` ikke er til stede.
9. Kjør `git checkout main` for å skifte tilbake til main-branch.
10. Kjør `git log`, `git status` og `ls` for å se at ingen av endringene i "branch-1" eller "branch-2" er til stede.

### 4 - Merging

#### a) Merging

1. Kjør `git pull` for å sørge for at du har de siste endringene lokalt.
2. Orienter deg på `main` branch. (`git log`, evt. `git status` og `ls`)
3. Bytt til branchen `merge-branch`.
4. Orienter deg på denne branchen og se at den har to commits som ikke er på `main`.
4. Kjør `git merge main` for å flette inn evt. endringer som har skjedd på `main` som ikke er på din branch. Dette er vanlig praksis fordi man vil skåne `main` for potensielle konflikter.
5. Orienter deg på branchen og se om det er noen endringer.
6. Bytt til `main` branch.
7. Kjør `git log`.
8. Kjør `git merge merge-branch` for å flette `merge-branch` inn i `main`.
9. Kjør `git log` og sammenlign loggen før og etter merge.

#### b) Conflicts

// NOT IMPLEMENTED

### 5 - Stashing

// NOT IMPELEMENTED

### 6 - Rebase

1. Kjør `git pull` for å sørge for at du har de siste endringene lokalt.
2. Orienter deg på `main` branch. (`git log`, evt. `git status` og `ls`)
3. Bytt til branchen `rebase-branch`.
4. Orienter deg på denne branchen og se at den har to commits som ikke er på `main`.
4. Kjør `git rebase main` for å putte inn evt. endringer som har skjedd på `main` som ikke er på din branch på toppen av din branch. Dette er vanlig praksis fordi man vil skåne `main` for potensielle konflikter.
5. Orienter deg på branchen og se om det er noen endringer.
6. Bytt til `main` branch.
7. Kjør `git log`.
8. Kjør `git rebase rebase-branch` for å sette `rebase-branch` på toppen av `main`.
9. Kjør `git log` og sammenlign loggen før og etter rebase.

### 7 - Reset and rollback and amend

#### a) Rollback

#### b) Reset

#### c) Amend

### 8 - Squash

1. Kjør `git pull` for å sørge for at du har de siste endringene lokalt.
2. Orienter deg på `main` branch. (`git log`, evt. `git status` og `ls`)
3. Bytt til branchen `squash-branch`.
4. Orienter deg på denne branchen og se at den har to commits som ikke er på `main`.
4. Kjør `git rebase -i <commit-hash>` der "commit-hash> er hash'en til commiten før "squash-1". (til men ikke med)
5. Endre "pick" til "squash" forran "squash-2" og endre "pick" til "reword". Klikk så "ctrl + x", etterfulgt av "y" på spørsmål om "Save modified buffer?", "eterfulgt av "enter".
5. Du vil nå få opp en skjerm hvor du kan endre commit-meldingen til "squash-1" commiten, og siden "squash-2" blir most inn i denne vil dette bli deres nye felles melding. 
6. Bytt til `main` branch.
7. Kjør `git log`.
8. Kjør `git rebase squash-branch` for å sette `squash-branch` på toppen av `main`.
9. Kjør `git log` og sammenlign loggen før og etter rebase.

### 9 - Rebase interactively

Lek deg med `git rebase -i <commit-hash>`. Les nøye gjennom alle mulighetene du har. Prøv f.eks. å endre en commit og/eller prøv å endre en commit-melding. Her er det tryggt å ødelegge ting. :)
