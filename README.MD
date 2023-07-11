# This is my own git commands overview

Je možné, že bez všech techto prikazu se obejdeme použitím Git Hub Desktop, ale co když nebude nainstalován?

Při tvorbě tohoto přehledu jsem čerpal z tutoriálů [Miso Hucko ZDE](https://www.youtube.com/watch?v=wbbWlbRBfmY&list=PLNAMH_0HgWT-ey31hQqrmi_Rgr4OVWgH3&index=19&ab_channel=InformatikasMi%C5%A1om), a z knihy [https://git-scm.com/book/en/v2] za což děkuji.
____________________
## Začínáme:
____________________
nastavení po instalaci apod.
```
git config --list //prehled nastavenych pravidel
git config --global user.name "Petr Novák" //nastaveni jmena uzivatele gitu
git config --global user.email "petr@novek.com" 
git config --global core.editor "'C:/Program Files (x86)/Notepad++/notepad++.exe' -multiInst -nosession" (prikaz nastavujici pojmenovani commitů pres aplikaci notepad)
``
_______________________________________
# .gitignore - VYTVOŘIT vždy na začátku
____________________
Pro správné nastavení .gitignore - lze najít připravené šablony daného jazyka
.gitignore používá [Regex prikazy](https://regex101.com/library).Soubor se vloží do adresáře s projektem. Git pak, vyradi soubory, dle nazvů. Pokud opomeneme a přidáme soubor do gitignore, který je jiz sledovany, tak samotny gitignore to nevyresi. Je třeba explicitně zadat gitu, aby tento soubor nesledoval příkazem 
```
git rm --cached utils/draw.py 
```
(soubor zustane v pc, ale jiz se nebude odesilat v commitech)
____________________
## Vytvoreni repository
____________________
```
git status
git init //spusteno v dannem prostoru kde je ulozen projekt (pokud jiz existuje tak je prepsan)
```
### Zakladni deleni prostoru gitu:
* 1)working area(mistni slozka - zalozi se prikazem git init[v projektu vznikne slozka .git]), 
* 2)stage area (sledovane ale zatím ne commit. Vznikne po příkazu git add. Jedná se o změny určené pro uložení do commitu), 
* 3)local repository(zmeny propsane do gitu) prikazem git commit -m "Nějaký popis změn"
* 4)remote repository - vzdálený adresář např. Github [zde](https://github.com/josse7cz/GitTutorial/edit/master/README.MD)
```
git init
git add <název souboru nebo tečka(všechny)>
git commit -m "e.g. Initial commit" (-m = message "text our message")
git status (seznam změn)
git log --oneline(vypíše podrobnosti a všechny commity-možnost ulozit do souboru [>someName.txt]. Ukončit výpis klavese q)
```

## Vymazani posledního záznamu git pomocí HEAD (pri obnove smazaneho a sledovaneho souboru (vratime se k predchozimu commitu))
```
git reset HEAD slouzi pro navrat po příkazu add
git checkout . se vrátí k řredchozimu commitu a zahodí veškere zmeny
git push (nahrava se na remote, ale musi již být nakonfigurovaný s uctem na GitHubu a musí být vygenerovaný SSh key - viz. níže)
```
___________________
 ## REMOTE repository (GitHub etc.), Připojení nového pc k remote repository
 ____________________
 zkontrolujeme, zda je nastaven uzivatel, remote apod.
 ```
 git config --list
 git remote
 ```
Nutne mit vygenerovany SSH klic (pouzivat sifrovane spojeni SSH!)
spustit git bash nebo cmd 
ssh-keygen -o 
odentrovat
vygeneruje se v Users/<aktualni user>/.ssh 
(vykopirovat vygenerovaný klíč příkazem) cat <nazev.pub> (type <nazev souboru>) OR Windows type <název souboru s koncovkou .pub> a toto zkopirovat do nastavení SSH na Githubu.
Pro stažení použít např:
git clone https://github.com/libgit2/libgit2 mylibgit (klonovani existujiciho adresare do adresare mylibgit[vytvoří tam kde se cmd nacházíme])

klonování repozitáře:
 git clone <adresa z github zálozka SSH> (nastaveni vzdaleneho repozitare)
dojde ke stazeni repozitare do pc

dále je vhodné pokud pracujeme ve více lidech novou větev prikazem
git branch <název>
 a prepneme se do teto větve
git checkout <název větve>
Pro git push zmeny na remote je pak nutne zalozit novou branch v remote, to provedeme buď ručně, ale raději:
```
git remote
git push origin (selze pokud jsme vytvorili novou vetev, která není na remote a pouzijeme prikaz)
  git push --set-upstream origin <nazev branche> (vytvoříme vetev na remote a prepneme se do ni.)
   POZOR pri uprave v jinych nez mnou vytvorenych souborech, vznikaji konflikty!!!
```

```
git diff (co je zmeneno, ale zatím neni připraveno k zapsání)
git diff --cached ukáže změny, které už jsou připraveny k zapsání

git commit (urcen pro zapsani zmen nachystanych po prikazu git add do git image (repository))
git commit -a -m 'nejaky popis zmeny' (parametr -a vylucuje nutnost pouziti add a zapise veskere zmeny do commitu rovnou-nutna opatrnost)
```
## Přejmenování
```
git mv stare_jmeno_souboru nove_jmeno_souboru (prejmenovani souboru)
příklad(nutno včetně cesty) git mv src/utils/TextFile.txt src/utils/Notepad.txt
```
## Odstranění
```
git rm --cached README (odstraneni souboru z prostoru sledovani zmen (napr opomenut do .gitignore))
git rm (odstraneni souboru z adresare) - pokud je jiz pripraven k zapsani, je treba pouzit parametr -f
git reset --hard (smaze veskere zmeny ve stage area tzn. vrátí odstraněné soubory apod.)
```
____________________
## Práce s větvemi
____________________
```
git branch <název>
    git branch pythonic_files
Dále možné přepínat se mezi větvemi příkazem:
git checkout <nazev branch> (mozne vypsat větve příkazem git branch)
```
pokud nemame nainstalovany git graph mozno zobrazit stromovou strukturu prikazem:
```
git log --online --all --graph

git merge <název větve>-spojovaní větví (zalezi co vse bylo zmeneno) pokud jsme zmenili master i dalsi je treba vice commitů
```
prepneme se do master verze prikazem:
```
git checkout master
```
tedy ulozime zmeny v master a pouzijeme prikaz:
```
git merge <nazev spojovane větve>
git merge pythonic_files (hotovo :)
```
nepotrebnou větev je dále možné odstranit příkazem:
```
git branche -d <nazev branche>
```
------------------
## Prace s nove pridanou vetvi na githubu z jineho pc
--------------------
Pokud na jinem pc připojeném k projektu ve kterém vznikly nov0 větve chceme pracovat s novou větví
 je třeba nekoli kroku:
```
 git fetch (nacteni změn na remote)
 git branch (vypíše lokalni větve)
 git branch -r(vypíše větve na remotu)
 git checkout origin/<název branche> (stav kdy se větev zobrazi ale muzeme prohlížet ale ne zapisovat větev není 
  propojena mezi lokálem a remotem)
 (pro práci ve vetvi je třeba prolinkovani tedy vytvoreni místní větve se stejnm názvem 
  a nastaveni propojeni na remote větev)
 (bud git branch <název větve> a pak git merge <název větve>)
 git checkout -b <název branch> origin/<nazev branch>(prepni se do branche a vytvoř ji pokud 
  zde není a propoj ji s remote branch)
 git branch (zkontrolujeme větve)
 origin/branch - jsou jen pro čteni
 git merge <název větve>-pripojeni větve do stávající. Muže být nutné vyřešit konflikty
``
 ____________________
 ## Konflikty mezi branchemi (jsou změněny soubory, které jsou součástí master anebo více větví mezi programátory)
____________________
Někdy je třeba provést ruční dekonflikci - tedy zjistit jaké změny mají být uloženy.
pro odmazani pripojene větve pomocí:
```
git branch -d <nazev větve>
Větev je mozne vymazat i na remote prikazem 
git push origin -d <branch-name>

Při vymazání větve na githubu je třeba propsat změny příkazem:
git fetch --prune origin (tím dojde k odmazání branche i na lokále)
```
### Zkratka
```
git fetch (nacteni zmen oproti remote) lepsi je prikaz 
git pull, ktery slučuje dva prikazy (git fetch a git merge), ktery nacte zmeny remote a slouci je do working space
```
____________________
## Vracení se v čase po příkazech git commit a git add(lokálně)
  dvě kategorie po prikaze add a po prikaze commit
___________________

pro zapomenutí uložených změn slouží příkazy
```
git reset main.py (vrátí zmeny provedene a addnuté v tomto souboru)
   git reset --hard(Nejpřísnější příkaz. smaze zmeny, ktere byly pridane od posledního commitu 
    a zaroven je odebere i fyzicky z working direktory)
git reset odeberou vse co bylo addnuté

git reset --soft <cislo commitu> (vrati vsechny zmeny do stagging area ale zachovavá veškeré změny ve working area)
git reset --hard <cislo commitu> (Nejpřísnější příkaz. smaze zmeny, ktere byly pridane od posledního commitu 
      a zaroven je odebere i fyzicky z working direktory)
git reset --mixed <cislo commitu>

git checkout <cislo commitu>(presunuti HEAD na jiný commit-slouzi pouze pro prohlizeni pro zmeny je 
    mozne zalozit branch z tohoto mista[git switch -c <nazev branch>])
    git switch - (vraci na puvodni polohu po checkoutu)


git tag (slouzi pro oznaceni např. funkcnich verzí)
git tag -a v0.9.9 -m "Some message" <tag id kam chceme pridat>
git push nepridava na remote tagy na to je treba prikaz git push --tagsq

git push -u origin master (odeslání na remote-doporucuji mit vse commited)
```
## Ostatní

* clear (prikaz pro vycisteni okna)
* q (klavesa se pouziva pro ukonceni vypisu nebo CTRL+C)
