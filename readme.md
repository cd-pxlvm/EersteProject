
# Werken in Git via Git Shell

Wij gaan eerst lokaal leren werken met Git, om dan ons project in GitHub te plaatsen. Voorlopig gaan we ook enkel met de masterbranche werken. Als je later GitHub gaat gebruiken om je code project in onder te brengen is het beter dat je met meerdere branches gaat werken.  Een goede afspraak is dat de masterbranche je ‘clean’ code is: hier staat geteste code, die zo in productie gebruikt kan worden. (Weet wel dat Git je daarin vrij laat, je kan hier ook andere afspraken maken) Elke andere branche geef je een naam, zodat je altijd weet in welke branche je aan het werken bent. In Git is het begin van een branche altijd een verwijzing (pointer = HEAD)  naar de versie van dat moment in de branche van waaruit je vertrekt. Je kan een branche zien als een kopie van de masterbranche op dat moment. Hier kan je dan in gaan werken en dit kan je dan op een gegeven moment weer gaan samenvoegen (= merge). Later gaan we hier iets dieper op in, maar wil je dit al eens bekijken, vind je dit visueel voorgesteld op: [GitHub flow](https://guides.github.com/introduction/flow/).  

Commandline: heel simpel: alle commando’s die te maken hebben met Git beginnen ook met git en dan een spatie. Als je niet meer weet wat een commando juist doet, kan je altijd volgende commando typen:
 ```>git help [commandonaam]``` 

##Een lokale repository (repo) aanmaken

### Te gebruiken commando's:

```
cd [pad]
git init
git config --global user.name “naam”
git config --global user.email jouwEmailadres
```

### Gebruik:

Om te beginnen heb je een map nodig waarin je je project gaat maken. Je navigeert naar de plaats waar je die map wil plaatsen:  ‘cd [pad]’. Want standaard kom je immers in de automatisch gegenereerde map GitHub terecht.  
Wij noemen deze map: ‘EersteProject’ en zetten die in de documenten map op onze computer.  
```
C:\Users\UsersName\Documents\Github> cd ..
C:\Users\UsersName\Documents> mkdir .\EersteProject\
```
Nu gaan we in die map staan:  
```
C:\Users\UsersName\Documents> cd .\EersteProject\
```
En je krijgt dan:  
```
C:\Users\UsersName\Documents\EersteProject>
```

Eenmaal in de map doe je ‘git init’, nu heb je van de map een repositorie gemaakt, waarbinnen versiebeheer nu mogelijk is. In de Windows verkenner in de map EersteProject is er nu een verborgen map ‘.git’. Zet verborgen items zichtbaar in het lint en je zal deze map zien. Zoals eerder al aangegeven, gaat hier de metadata van de commits in opgeslagen worden.  

```
C:\Users\UsersName\Documents\EersteProject> git init
Initialized empty Git repository in C:/Users/UsersName/Documents/EersteProject/.git/
C:\Users\UsersName\Documents\EersteProject [master]>
```
Je ziet nu aan de prompt dat je niet gewoon meer in de map staat, maar dat je in de masterbranche van je Git project staat.  
Als je GitHub for Windows hebt geïnstalleerd zoals aangegeven (dus ook gebruikersnaam en e-mailadres ingevuld), dan kan je deze stap overslaan. Maar als je dat niet gedaan hebt, moet je iemand eigenaar maken hiervan: dit doe je dan als volgt:  

```
C:\Users\UsersName\Documents\EersteProject [master]> git config --global user.name 'gebruikersnaam'
C:\Users\UsersName\Documents\EersteProject [master]> git config --global user.email gebruikersemail
C:\Users\UsersName\Documents\EersteProject [master]> git commmit --amend --reset-author
```
Die laatste regel zorgt ervoor, dat indien er al iemand anders als user ingesteld staat, deze vervangen wordt door deze.  
Indien je iemand enkel van dit project gebruiker wil maken, laat je die global in bovenstaande commando's weg.  

Zo, je lokaal project om met versiebeheer in te werken staat klaar. Maar dit is nog een leeg project.  

## Git add, commit lokaal

### Te gebruiken commando's:
```
git add bestandsnaam 
git add
git commit
git commit -m “Boodschap”
git cat-file commit commit_id 
git diff
```
### Gebruik:

Als je al een project hebt, dat je wil gebruiken, kan je dat nu in de map zetten. Maar in deze cursus maak je een heel nieuw project, zodat je alle stappen kan doorlopen.
Nu: een bestand in de map zetten: ‘readme.md’. Dit kan je in kladblok maken en bij opslaan als kiezen voor ‘alle bestanden’ en dan als extensie .md meegeven. Of je kan aan de prompt notepad readme.md typen  

```
C:\Users\UsersName\Documents\EersteProject [master]>notepad readme.md
```
Nu opent kladblok en krijg je een pop-up: dit bestand bestaat niet, moet ik dit aanmaken? Je klikt ja.  
![schermafbeelding](/images/screen1.png)
Je zet  *Hier komt het doel van ons project* in het bestand (met de asterisken ervoor en erachter) en slaat dit op en sluit het bestand.  Opmerking: als je die pop-up niet gekregen hebt: doe dan alsnog ‘opslaan als’ en sla het op als readme.md , alle bestanden(geen tekstbestand!!!)  
Je typt nu ‘git status’: Je krijgt nu de melding dat er nog ‘Untracked files’ zijn en dat je die best toevoegt aan datgene je wil committen.  
```
C:\Users\UsersName\Documents\EersteProject [master]> git status
```
Je ziet nu aan de prompt [master ] met rode cijfers erachter. Dit wil zeggen dat je werk area niet gelijk is aan je repo.   
Het is niet omdat het in de map zit, dat het ook in Git zit. (Work area vs Staging area vs repository)  
Als je maar 1 bestand wil toevoegen aan Git:  
git add bestandsnaam 
```
C:\Users\UsersName\Documents\EersteProject [master]> git add readme.md
```
Als je meerdere bestanden hebt, ga je ze niet op die manier toevoegen aan de staging area, maar doe je alles in 1 keer:  
```
C:\Users\UsersName\Documents\EersteProject [master]> git add . 
```
Je ziet nu aan de prompt [master] dat je groene cijfers krijgt: dit is hoe nu je staging area eruit ziet.  
Maar nu ben je er nog niet. Als je nu wil dat de huidige toestand van alle bestanden in je staging area gezien worden als een nieuwe versie van je project, dan moet je dat met een commit in de repo zetten.  
git commit : op deze manier opent zich kladblok, opdat je een commitboodschap kan meegeven. Geef altijd een duidelijke boodschap mee, met wat veranderd is ten opzichte van de vorige versie. Dit is handig als je ooit een vorige versie van je project nodig hebt.  
Je kan ook ‘git commit -m “boodschap” ‘ ingeven. Nu krijg je geen pop-up meer, want je hebt al de reden van commit meegegeven.  
Nu zie je aan de prompt terug gewoon [master] omdat alles uit je werk area ook in je repo zit.  
Omdat alles lokaal staat, zie je misschien niet of er veranderingen zijn. Hiervoor kan je altijd git status gebruiken. Die geeft aan wat waar zit.  
![voorbeeld Git Shell met bovenstaande acties](images/screen2.png)   

### *Oefeningen*
Voeg nog 2 bestanden toe, breng 3 wijzigingen aan in die bestanden en doe na iedere verandering een add en een commit.  
Doe nu een ''' git status ''' en bekijk aandachtig de boodschap die je nu krijgt.  
Kies 2 verschillende commits en ga na wat de verschillen zijn tussen de 2. Doe ```git diff commit_id1 commit_id2```  
Alle mogelijkheden met betrekking tot gebruik van [git diff](https://git-scm.com/docs/git-diff) opgelijst.  

## Lokale repo pushen naar remote.
### Te gebruiken commando's:
```
git remote add origin https://github.com/gebruikersnaam/projectnaam.git
git push -u origin master
ls
git status
```
### Gebruik:
Het project bestaat nog steeds enkel lokaal. Als je met meerdere aan het project wil werken, zien de anderen nog niet dat er iets gewijzigd is. Hiervoor moet je nu je code pushen naar GitHub.    
Maar op dit moment bestaat ons project nog maar enkel lokaal. We maken nu op GitHub ook een repo aan met dezelfde naam. Hiervoor moet je je inloggen op GitHub.com en je kiest dat je een nieuwe repository wil aanmaken. Dit kan met ![het plusje naast je account afbeelding](images/newRepo1.png) Of met de knop ‘”New repository” in ![het kader met het overzicht van jouw projecten](images/newRepo2.png).   
Je krijgt nu een ![invulveld](images/newRepo3.png). We geven het dezelfde naam als ons lokaal project ‘EersteProject’. Je geeft een korte uitleg over jouw project bij de beschrijving. Vermits wij in ons project een Readme.md hebben gemaakt, gaan we dit hier niet meer aanvinken.   
In je eerste project, gaan we ook geen .gitignore laten genereren. Weet dat je in een project met code altijd opneemt. In punt 4 gaan we dieper in op dit soort bestand en waarom het goed is om altijd een .gitignore bestand in je project te zetten. Je kan dit dan later nog toevoegen.  
Nu klik je op de knop ‘Create repository’ en je remote repo is aangemaakt.  
Nu moet je nog een verbinding maken met je lokaal project. In GitHub opent zich nu een [venster](images/newRepo4.png) dat je helpt met hoe je dat nu best doet. Vermits je lokaal je project al volledig klaar hebt staan, ga je dit nu nog moeten pushen naar GitHub. We kiezen hiervoor de optie om dit vanaf de prompt te doen.  
```
C:\Users\UsersName\Documents\EersteProject [master]>git remote add origin https://github.com/gebruikersnaam/projectnaam.git 
C:\Users\UsersName\Documents\EersteProject [master]>git push -u origin master
```
Nu heb je een link gelegd met GitHub en heb je je project geüploaded naar GitHub. En dan krijg je een ![boodschap](images/pushMaster.png) wat hij doet en als laatste moet dan staan: ‘Branch master set up to track remote branch master from origin'.  

Maak nu in de ![verkenner](images/testbestand.png) in de projectmap een tekstbestand testBestand.txt .  
Aan de prompt typ je ls. Je ziet dat in het project nu 2 bestanden zitten, maar dit zegt niet veel. Als je nu naar de prompt gaat kijken, zie je dat er weer rode cijfers achter master staan. Typ nu git status en je krijgt de boodschap dat je branche up-to-date is met ‘origin/master’, maar dat er wel nog een bestand in zit, dat niet tot het Git project behoort. En je krijgt dan de boodschap hoe je dat bestand kan opnemen in de staging area, zodat bij een volgende commit het automatisch in je masterbranche zit.
![ls git status voorbeeld](images/lsStatus.png)  
Je doet dus terug ```C:\Users\UsersName\Documents\EersteProject [master= rode cijfers]>git add testbestand.txt``` en de rode cijfers achter master, zijn groen.  
Nu doen we weer een commit en lokaal zit alles in de master branche. Maar nu zie je achter master een pijl staan, die aangeeft dat je verandering nog gepusht moet worden.  
Dus doe je nu weer: ```C:\Users\UsersName\Documents\EersteProject [master= groene cijfers]> git push -u origin master ```. En als aan de prompt nu weer [master =] verschijnt, dan heb je lokaal en remote dezelfde versie van je project staan.  

## Remote pullen naar lokaal.
### Te gebruiken commando's:
```
git pull origin master
```
### Gebruik:
Vooraleer je verder werkt aan je project, ga je altijd na of je lokaal dezelfde versie hebt als remote. Het kan immers zijn dat een collega nog verder aan het project heeft gewerkt en dat jij niet meer de laatste versie lokaal hebt staan.  Om problemen te vermijden ga je dus altijd eerst de versie van GitHub afhalen.  
Dit doe je met git pull origin master. Als er niets gewijzigd is, krijg je : Already up-to-date.
```
C:\Users\UsersName\Documents\EersteProject [master=]>git pull origin master
```
Maar nu ga je een ![verandering](images/verandering1.png) aanbrengen remote: Zet in het bestand ‘testBestand.txt’ wat tekst.  
Een bestand editen doe je door op de naam van het bestand te klikken en dan op het potlood in het lint.  
In dit ![venster](images/verandering2.png) zet je tekst in het bestand. Je vult een commit boodschap in en klikt op de knop 'Commit changes'.  
Maar nu staat die aanpassing wel online, maar die zit niet in onze lokale repo.  
Laat je echter niet vangen: als je nu lokaal git status doet, ga je nog krijgen dat alles ok is. Want dit git status gaat kijken of jij lokaal nog iets hebt toegevoegd, dat nog niet gecommit is. Nu gebruik je  
 ```C:\Users\UsersName\Documents\EersteProject [master=]>git pull origin master```  
en nu krijg je weer een hele lijst van acties. Als je gaat ![kijken](images/afterPull.png) dan zegt de tekst dat 1 bestand gewijzigd is.  
>**Dus**: voordat je lokaal begint te werken altijd een pull doen ook al staat [master =].  
Zo vermijd je al een eerste reeks problemen, wanneer je jouw aanpassingen wil pushen naar remote.  

## Merge conflict oplossen.
### Te gebruiken commando's:
alle reeds gebruikte commando's
### Gebruik:
Zoals hierboven aangegeven, kunnen er ook problemen opduiken als je jouw aanpassingen wil pushen.   
Hiervoor ga je nu zelf een probleem uitlokken.  
In GitHub voeg je in het ![tekstdocument](images/merge1.png) testbestand.txt een tweede regel tekst toe en commit dit.  
Lokaal ga je in ![testbestand.txt](images/merge2.png) ook een tweede regel tekst toevoegen.  
Nu open je de Git Shell. In je project doe je git status. Nu zie je dat je lokaal iets hebt veranderd en dat je dat nog moet toevoegen aan je project. ![Doe nu weer git add testBestand.txt en een commit. Nu ga je dit naar je remote repo pushen.](images/merge3.png).  
Oei, dit lukt precies niet: remote staat er een andere versie van je project dan die, die je lokaal gewijzigd hebt. Voorstel is om eerst een git pull uit te voeren, zodat je lokaal project up-to-date is. ![Dit](images/merge4.png) ga je nu proberen.  
Maar ook dit gaat niet zomaar: je ziet dat er nu 2 reeksen getallen verschijnen en dat er een tweerichtingspijl na master staat. Dit wil zeggen dat je dit eerst moet oplossen, voordat je verder kunt. Je opent nu het bestand waar zich een ‘Merge conflict’ voordoet.  
Dit doe je via de prompt: notepad .\testbestand.txt. Nu opent zich het ![bestand](images/merge5.png) en je ziet dat beide aanpassingen in je document zijn opgenomen, maar dat er nog dingen zijn bijgekomen.  
Als eerste staan er kleiner dan tekens gevolgd door HEAD. HEAD is een pointer met metadata van de laatste commit. Die geeft aan wat in de versie die je wil mergen staat. Daaronder zie je gelijkheidstekens en daaronder dan de regel die anders is in de versie die jij wil mergen, met daaronder groter dan tekens en dan de id van de commit die het probleem geeft. Die vind je ook op GitHub terug.  
Jij moet nu bepalen wat juist is. Met andere woorden, je gaat het ![bestand](images/merge6.png) manueel aanpassen en opslaan.  
Ga dit terug toevoegen en committen. Nu push dit terug naar remote. Je ![ziet](images/merge7.png): nu lukt het wel.  
En in je browser refresh je GitHub, je gaat kijken naar de commits en zie je ![de verschillende commits](images/merge8.png)  
Dus beide commits zijn opgenomen in de geschiedenis van je versiebeheer, evenals de commit die nodig was om het probleem op te lossen.  
Je ziet: het was nu maar 1 regel en toch vroeg het al je aandacht om dit juist op te lossen. Stel je eens voor dat je een groot aantal code geschreven hebt en dit probleem doet zich dan voor!
>**Dus**: Altijd zo snel mogelijk commits (van logische blokken) doen en pushen naar GitHub, evenals voor start nieuwe code steeds een pull, zelfs als je zelf net gepusht hebt. Alleen zo blijf je sommige problemen steeds een stapje voor. 
Een andere manier om problemen voor te blijven is goede afspraken maken: Werkverdelingen en goede ontwerpen maken met losse koppelingen tussen de onderdelen.  

Maar vroeg of laat ga je toch een merge probleem tegen komen, weet dan dat je hier geleerd hebt hoe je die best oplost. Soms moet je op zo een moment met je collega(‘s) overleggen hoe het moet opgelost worden. Vergeet dan niet dat issues, in punt 6, hier een goed hulpmiddel kunnen zijn. (Pull requests kunnen hier ook voor gebruikt worden, maar dit wordt in deze cursus niet behandeld.)  


