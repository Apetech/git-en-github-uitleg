<!-- vscode-markdown-toc -->
* 1. [Introductie](#Introductie)
* 2. [Git](#Git)
	* 2.1. [Initiële setup van Git](#InitilesetupvanGit)
	* 2.2. [Repository](#Repository)
	* 2.3. [Optie 1: lokaal een repository aanmaken](#Optie1:lokaaleenrepositoryaanmaken)
	* 2.4. [Optie 2: een repository uit GitHub ophalen](#Optie2:eenrepositoryuitGitHubophalen)
	* 2.5. [Herhaling van stappen](#Herhalingvanstappen)
	* 2.6. [Stap 1: Staging](#Stap1:Staging)
	* 2.7. [Stap 2: Commit](#Stap2:Commit)
	* 2.8. [Atomic commits](#Atomiccommits)
	* 2.9. [Combinatie van Add en Commit](#CombinatievanAddenCommit)
	* 2.10. [De juiste message](#Dejuistemessage)
	* 2.11. [Logfile bekijken](#Logfilebekijken)
	* 2.12. [Negeren van files en/of mappen](#Negerenvanfilesenofmappen)
	* 2.13. [Branches](#Branches)
	* 2.14. [Branch commando's](#Branchcommandos)
	* 2.15. [Checkout](#Checkout)
	* 2.16. [Merging](#Merging)
	* 2.17. [Verschillen zien met diff](#Verschillenzienmetdiff)
	* 2.18. [Tijdelijk opslaan met stash](#Tijdelijkopslaanmetstash)
* 3. [GitHub](#GitHub)
	* 3.1. [Cloning](#Cloning)
	* 3.2. [Push](#Push)
	* 3.3. [Push code naar GitHub](#PushcodenaarGitHub)
	* 3.4. [Git push: uitgebreid](#Gitpush:uitgebreid)
	* 3.5. [Remote](#Remote)
	* 3.6. [Fetching](#Fetching)
	* 3.7. [Pull](#Pull)
* 4. [Overig](#Overig)
	* 4.1. [Help](#Help)
	* 4.2. [Vim tips](#Vimtips)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->


# Het gebruik van Git en GitHub

##  1. <a name='Introductie'></a>Introductie

**Git** is een VCS (Version Control System) oftewel een versiebeheersysteem. Het houdt bij welke veranderingen je aan bestanden maakt, zodat je:

- Terug kunt naar een eerdere versie als iets misgaat.
- Verschillende versies kunt beheren (bijv. features of bugfixes).
- Makkelijk kunt samenwerken met anderen, zonder elkaars werk te overschrijven.

Je gebruikt Git meestal lokaal op je computer, via de command line of tools zoals VS Code.

**GitHub** is een online platform waar je Git-projecten kunt opslaan, delen en samenwerken met anderen.
- Je kunt je Git-repository er naartoe uploaden.
- Anderen kunnen jouw code bekijken, downloaden of eraan meewerken (via pull requests).
- Het biedt extra’s zoals issue tracking, wiki’s en CI/CD-integraties.

----
##  2. <a name='Git'></a>Git

###  2.1. <a name='InitilesetupvanGit'></a>Initiële setup van Git

Zorg dat je de laatse versie van git hebt geinstalleerd. Om de huidige versie van Git te zien:
```
$ git —version
```
Geef vervolgens eenmalig je naam en e-mailadres in:
```
$ git config —global user.name “Robert”
$ git config user.name

$ git config —global user.email robert@gmail.com
$ git config user.email
```

💡Je kunt je favoriete editor opgeven, zodat deze wordt geopend bij een mogelijk conflict.

Nano:	
```
$ git config --global core.editor "nano -w"
```
Vim:
```
$ git config --global core.editor "vim --nofork"
```
VS Code:
```
$ git config --global core.editor "code --wait"
```
###  2.2. <a name='Repository'></a>Repository
Een repository is een (project/app) workspace in Git die files volgt, beheert en bijhoudt in een folder. Voor het gemak spreek je van een *repo*. Je kunt op twee manieren een repo maken.

###  2.3. <a name='Optie1:lokaaleenrepositoryaanmaken'></a>Optie 1: lokaal een repository aanmaken

Je maakt **eenmalig** een repo aan in een nieuwe folder:
```
$ git init
```
De repo geldt dan voor deze folder en subfolders.
In deze folder vind je een hidden .git folder. Je kunt deze zien door het volgende op de command line te typen:
```
$ ls -la
```
Als je de .git folder ziet, weet je dat een repo is aangemaakt.

    ⚠️ Maak in een subfolder geen nieuwe repo aan!

Het meest gebruikte git-commando is:
```
$ git status
```
Gebruik dit commando regelmatig om de status van de repo te bekijken.

###  2.4. <a name='Optie2:eenrepositoryuitGitHubophalen'></a>Optie 2: een repository uit GitHub ophalen

Een tweede mogelijk om een repo aan te maken is om deze remote van GitHub op te halen:
```
$ git clone https://github.com/apetech/git123.git test123
```
Dit kopieert de repository *git123* naar de folder *test123*. En maakt hierbij lokaal een repo aan.


###  2.5. <a name='Herhalingvanstappen'></a>Herhaling van stappen
De volgende stappen herhaal je vaak in je workflow. Het maken van (1) een *add* en vervolgens (2) een *commit*. Een commit is een soort snapshot (of checkpoint). Doe een add en commit na elke groepering van aanpassingen.

Je hebt bijvoorbeeld een aanpassing aan een file gedaan of een file verwijdert. Sla vervolgens je aanpassingen op en doe een commit.

###  2.6. <a name='Stap1:Staging'></a>Stap 1: Staging
```
$ git add
```
Hiermee plaats je je aanpassingen vanuit de *working directory* in de *staging area*. Deze stap wordt ook wel *staging* genoemd.

Maak bijvoorbeeld twee files aan en stage deze:
```
$ git add file1.txt file2.txt
```
Je kunt alle files in 1x stagen (let op de punt):
```
$ git add .
```
Ongedaan maken (unstagen) doe je als volgt:
```
$git rm --cached <file>
```
###  2.7. <a name='Stap2:Commit'></a>Stap 2: Commit
```
$ git commit -m "add initial file"
```
Hiermee plaats je je aanpassingen vanuit de staging area in de lokale repo. De *-m* staat voor *message* en kun je terugzien in de log.

    💡 Je kunt je aanleren om elk uur een commit te doen.

###  2.8. <a name='Atomiccommits'></a>Atomic commits
Beter is het om na elke kleine verandering (een enkele feature, change, fix) een add/commit te doen.

###  2.9. <a name='CombinatievanAddenCommit'></a>Combinatie van Add en Commit
Je kunt een add en commit in één keer uitvoeren:
```
$ git commit -am “voeg tekst in file1 toe”
```

###  2.10. <a name='Dejuistemessage'></a>De juiste message
Gebruik tegenwoordige tijd in de gebiedende wijs in de commit message:
```
"Maak initiele file aan"
of
"Add X and Y"
```
###  2.11. <a name='Logfilebekijken'></a>Logfile bekijken
Het volgende commando laat een volledig overzicht van al je logs plus bijbehorende info zien:
```
$ git log
```
Dit kan overweldigend overkomen; gebruik --oneline om alleen de messages te zien:
```
$ git log —oneline
```

###  2.12. <a name='Negerenvanfilesenofmappen'></a>Negeren van files en/of mappen

Je kunt bestanden (met bijvoorbeeld **paswoorden** erin) of Mac OS gerelateerd zaken (deze staan in .DS_store) uitsluiten door deze in de file *.gitignore* in de root te plaatsen. Hieronder enkele bestanden en folders in de file. Plaats ze afzonderlijk op een regel:
```
.DS_store
.settings
.project
.NPproject
.idea
library/
node_modules/
tensorflow/
```
💡 De site [gitignore.io](https://www.toptal.com/developers/gitignore/) bevat overzichten met wat in de .gitignore file kan worden geplaatst.


###  2.13. <a name='Branches'></a>Branches

Zie een banch als een alternatieve tijdlijn waarin je kunt werken. De default branch heet “master”, of sinds 2020 “main”.

HEAD is een pointer die refereert naar de “huidige locatie” (lees branch) in de repo. 
```
$ cat .git/HEAD
```
Wijst vaak naar de laatste branch, niet naar de laatste commit.
Stel HEAD wijst naar een bepaalde branch, dan wordt de commit van die branch uitgevoerd.

    💡 de term HEAD komt van een analoge taperecorder.

###  2.14. <a name='Branchcommandos'></a>Branch commando's
```
$ git branch			
// laat alle branches zien; met * ervoor is de huidige branch

$ git branch -v		
// geeft iets meer info

$ git branch name1	
// maak branch name1 aan

$ git switch name1	
// HEAD wijst nu naar name1 i.p.v. master

$ git switch -c name2		
// maakt branch name2 aan èn laat HEAD ernaar wijzen
```
De “-c” staat voor create.Hiermee kun je een branch aanmaken en er gelijk naar toegaan.

Het verwijderen van een branch:
```
$ git branch -d name3
```
⚠️ ga naar een andere branch, anders doet dit commando het niet.

Het hernoemen van een branch:
```
$ git branch -m name4 name5
```
De “-m” staat voor move/rename.

⚠️ blijf in deze branch, anders doet dit commando het niet.

Laat een remote branche zien:
```
$ git branch -r
```
De "-r" staat voor remote.

###  2.15. <a name='Checkout'></a>Checkout
Checkout doet hetzelfde als “git switch”:
``` 
$ git checkout name1
```
Alleen kan “checkout” veel meer! Zie online docs voor meer informatie. Met het volgende commando ga je bijvoorbeeld terug in de tijd:
```
$ git checkout <commit nr>
```
Hiermee ga je naar deze commit (type het commit nummer volledig of alleen de eerste 7 karakters).

💡Soms zie je de term “detached HEAD state”; hierin kun je experimenteren met changes en commits doen. Vervolgens kun je teruggaan naar een branch zonder impact te hebben.

###  2.16. <a name='Merging'></a>Merging

Merging voegt branches samen. De master branch heet ook wel de *source of truth* en daar experimenteer je niet op. Experimenteren doe je op een *trunk*; een andere branch.
Samenvoegen van features op de trunk op de master heet merging.

    ⚠️ Je merged branches, niet commits! En altijd naar waar de HEAD is.
Ga eerst naar master om daarna de branch met master te mergen: 
```
$ git switch master

$ git merge name5	
// merged branch name5 naar master
```

###  2.17. <a name='Verschillenzienmetdiff'></a>Verschillen zien met diff

Diff laat verschillen tussen commits, branches, files en working directory zien.
```
$ git diff			
// laat unstaged verschillen zien (wat is weg en wat is erbij gekomen)
```
Laat verschillen zien tussen staging area en de working directory.
```
$ git diff HEAD	
// laat verschillen tussen HEAD en de working directory
```
Laat verschillen zien in de working directory en de laatste commits (staged èn unstaged)
```
$ git diff —staged		
// laat staged verschillen zien

$ git diff —cached		
// doet hetzelfde
```

###  2.18. <a name='Tijdelijkopslaanmetstash'></a>Tijdelijk opslaan met stash

Je kunt je uncommited changes tijdelijk opslaan voordat je naar een andere branch gaat.
```
$ git stash			
// plaatst dingen in stash

$ git stash save		
// doet hetzelfde als "git stash"
```
Om de stashed changes te verwijderen en deze in je huidige of een andere branch toe te voegen:
```
$ git stash pop		// haalt dingen uit stash
```
----
##  3. <a name='GitHub'></a>GitHub

De voordelen van het gebruik van GitHub:
* Backup: slaat public en private repo’s op in de cloud.
* Projecten delen: handig voor samenwerking.
* Open: dè thuishaven voor open source projecten.
* Exposure: showcase van je projecten.

De term *remote* wordt gebruikt om de bestemming (lees GitHub url) aan te geven waar de repo zich bevindt. *Origin* is een veel gebruikte naam/label van de GitHub url.

###  3.1. <a name='Cloning'></a>Cloning

Haal code op uit een repo in GitHub voor lokaal gebruik. Dit heet *cloning*:
```
$ git clone <url>
```
    ⚠️ let er op dat je niet in een bestaande repo bent. Na de clone bevat de folder waarin je stond een volledige repo die geïnitialiseerd is. Nu kun je met ‘git log’ de historie zien.


###  3.2. <a name='Push'></a>Push
De syntax is:
```
$ git push <remote> <branch>

$ git push -u origin main
// origin is de remote repository 
// en main is de lokale repository
```
    ⚠️ Bovenstaande kan een foutmelding op SSH key geven.


###  3.3. <a name='PushcodenaarGitHub'></a>Push code naar GitHub
Je kunt op twee manieren een repo pushen naar GitHub.

**Optie 1** (een bestaande repo)
- Maak een nieuwe repo aan op GitHub
- Verbind je lokale repo hiermee (add a remote):
    ```
	$ git remote add <remote> <url>
	// bijvoorbeeld:
	$ git remote add origin https://github.com/Apetech/book123.git
    ```
- Push je aanpassingen naar GitHub:
    ```
	$ git push <remote> <local branch>
	// bijvoorbeeld:
	$ git push origin master
    ```


**Optie 2** (begin van scratch)
- Maak in GitHub een nieuwe repo aan.
- Kopieer deze (clone) naar je lokale omgeving.
- Maak een nieuwe folder aan en ga erin staan.
    ```
	$ git clone <url>		
    // de repo is nu lokaal aktief
    ```
- Maak lokaal enkele aanpassingen.
- Push deze aanpassingen naar GitHub:
    ```
	$ git push origin master
    ```


Alle commando's van optie 1 achter elkaar:
```
git remote add origin https://github.com/Apetech/
book123.git

git branch -M main
// "-M" staat voor "--move --force"
// en hernoemt "master" in "main".

git push -u origin main
```
    💡 De "-u" voegt een (tracking-)referentie toe aan de GitHub server waarnaar je aan het pushen bent. Wat hieraan belangrijk is, is dat je later een "git pull" kunt doen zonder nogmaals de argumenten mee te geven. 


Alle commando's van optie 2 achter elkaar:
```
git init

git add README.md

git commit -m "first commit"

git branch -M main		
// "-M" staat voor "--move --force"
// en hernoemt "master" in "main".

git remote add origin https://github.com/Apetech/book123.git

git push -u origin main
```


###  3.4. <a name='Gitpush:uitgebreid'></a>Git push: uitgebreid

De syntax is:
```
$ git push <remote> <local branch>:<remote branch>

// Bijvoorbeeld:
$ git push origin pancake:waffle
```
Hier wordt de lokale branch *pancake* naar de remote branch *waffle* gepusht.
Een andere gebruiker kan nu deze files ophalen:
```
$ git pull
```

Vervolgens bewerken en toevoegen:
```
$ git add -A
```
De "-A" staat voor alle files

Herhaal vervolgens commit en push.


###  3.5. <a name='Remote'></a>Remote

Een bestaande remote van je repo bekijken:
```
$ git remote

$ git remote -v	
// laat meer informatie zien
```
Dit laat de push/pull url’s zien

Toevoegen van een nieuwe remote:
```
$ git remote add <name> <URL>

// Bijvoorbeeld:
$ git remote add origin https://github.com/robertn/git123.git
```
Origin is de (vaak gebruikte) naam (lees: label) van de GitHub url.

Overige remote commando's:
```
$ git remote rename <old> <new>
// naam van de remote branch veranderen.

$ git remote remove <name>
// remote branch verwijderen
```

###  3.6. <a name='Fetching'></a>Fetching

Download wijzigingen van een remote repository naar je lokale repository (**niet je working directory**). De wijzigingen worden **niet** geïntegreerd in je werkbestanden. Het laat je zien waar anderen aan gewerkt hebben, zonder dat je deze hoeft samen te voegen in je lokale repo.
```
$ git fetch <remote>
$ git fetch origin
```

###  3.7. <a name='Pull'></a>Pull

Pull werkt de HEAD branch bij met alle wijzigingen die zijn opgehaald van de remote en **het werkt je working directory bij**. Het download data van GitHub en werkt de lokale repo bij met de wijzigingen.  
```
$ git pull <remote> <evt. branch>
```
----
##  4. <a name='Overig'></a>Overig

###  4.1. <a name='Help'></a>Help
```
$ git
```
Laat een lijst van meest gebruikte commando’s zien.
```
$ git <command> --help
```
Laat de man-pages van het commando zien.


###  4.2. <a name='Vimtips'></a>Vim tips
Om uit een *full blown* commit te komen: type “i” van *insert* en breng een eventuele aanpassing aan. Type vervolgens:
```
<ESC>
:wq
```
