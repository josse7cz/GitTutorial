# This a my own commands tutorial with Git

Je dost možné, že bez vsech techto prikazu se obejdeme použití Git Hub Desktop, ale co když nebude nainstalován?

Při tvorbě tohoto přehledu jsem čerpal z tutoriálů [Miso Hucko ZDE](https://www.youtube.com/watch?v=wbbWlbRBfmY&list=PLNAMH_0HgWT-ey31hQqrmi_Rgr4OVWgH3&index=19&ab_channel=InformatikasMi%C5%A1om)
____________________
## Začínáme:
____________________
nastavení po instalaci apod.
```
git config --list //prehled nastavenych pravidel
git config --global user.name "Petr Novák" //nastaveni jmena uzivatele gitu
git config --global user.email "petr@novek.com" 
    
Pro správné nastavení gitignore - lze najít připravené šablony daného jazyka

```
__________________________________________
# .gitignore - VYTVOŘIT vždy na začátku
____________________
Regex prikazy v tomto souboru, zaradi nazvy souboru které bude git ignorovat
pokud nepridame soubor do gitignore a je jiz sledovany, tak samotny gitignore to nevyresi.
Je třeba zadat gitu, aby tento soubor nesledoval příkazem 
 (take pokud jsem uz pridal pomoci add ., ale zapomnel jsem udelat commit na jinem souboru) git rm --cached utils/draw.py (soubor zustane v pc ale jiz se nebude
  odesilat v commitech a vrati se jeho sledovaní, jeho zmena apod.)

____________________
## Vytvoreni repository
____________________
```
git status
git init //spusteno v dannem prostoru kde je ulozen projekt (pokud jiz existuje tak je prepsan)
```
Zakladni deleni prostoru gitu:
1)working area(mistni slozka - zalozi se prikazem git init[vznikne slozka .git]), 
2)stage area (sledovane ale necomittle vznikne po prikaze git add . jedná se o změny určené pro uložení do commitu), 
3)local repository(zmeny propsane do gitu-) prikazem
4)remote repository
 
```
git commit -m "e.g. Initial commit" (-m = message "text our message")
or
git config --global core.editor "'C:/Program Files (x86)/Notepad++/notepad++.exe' -multiInst -nosession" (prikaz nastavujici pojmenovani commitů pres aplikaci notepad-nastavuje ho defaultne)

git log --oneline(vypíše podrobnosti a všechny commity-možnost ulozit do souboru [>someName.txt]. Ukončit výpis klavese q)

vymazani zaznamu HEAD (pri obnove smazaneho a sledovaneho souboru (vratime se k predchozimu commitu))
git reset HEAD slouzi pro navrat prikazu add
git checkout . se vrati k predchozimu commitu a zahodi veskere zmeny
git push (nahrava se na remote, ale musi již být napárovaný s uctem a repository na Gitu)
```
____________________
## Stažení projektu do lokalního repository
____________________
```
git clone https://github.com/libgit2/libgit2 mylibgit (klonovani existujiciho adresare do adresare mylibgit)
git diff (co je zmeneno, ale zatím neni připraveno k zapsání)
git diff --cached ukáže změny, které už jsou připraveny k zapsání

git commit (urcen pro zapsani zmen nachystanych po prikazu git add do git image (repository))
git commit -a -m 'nejaky popis zmeny' (parametr -a vylucuje nutnost pouziti add a zapise veskere zmeny do commitu rovnou-nutna opatrnost)
git mv stare_jmeno_souboru nove_jmeno_souboru (prejmenovani souboru)
příklad(nutno včetně cesty) git mv src/utils/TextFile.txt src/utils/Notepad.txt

git rm --cached README (odstraneni souboru z prostoru sledovani zmen (napr opomenut do .gitignore))
git rm (odstraneni souboru z adresare) - pokud je jiz pripraven k zapsani, je treba pouzit parametr -f
git reset --hard (smaze veskere zmeny ve stage area tzn. vrátí odstraněné soubory apod.)
```
____________________
## Nová větev
____________________
```
git branch <název>
    git branch pythonic_files
Dále možné přepínat se mezi větvemi příkazem:
git checkout <nazev branch> (mozne vypsat větve příkazem git branch)
pokud nemame nainstalovany git graph mozno zobrazit stromovou strukturu prikazem:
git log --online --all --graph

git merge <název větve>-spojovaní větví (zalezi co vse bylo zmeneno) pokud 

 jsme zmenili master i dalsi je treba vice commitů
prepneme se do master verze prikazem git checkout master
tedy ulozime zmeny v master a pouzijeme prikaz:
 git merge <nazev spojovane větve>
 git merge pythonic_files (hotovo :)
 nepotrebnou větev je dále možné odstranit příkazem:
 git branche -d <nazev branche>
 ```
____________________
 ## REMOTE repository (GitHub etc.), Připojení nového pc k remote repository
 ____________________
 zkontrolujeme zda je nebo neni nastaven uzivatel, remote apod.
 ```
 git config --list
 git remote
 dalsi prikazy viz níže po prikazu git clone...

 nainstalovani gitu a nastaveni viz vyse (git config --list....)
 Nutne mit vygenerovany SSH klic (pouzivat sifrovane spojeni SSH!)
 spustit git bash 
 ssh-keygen -o 
 vygeneruje se v Users/<aktualni user>/.ssh 
 (vykopirovat vygenerovaný klíč příkazem) cat <nazev.pub> (type <nazev souboru>)a toto zkopirovat do github uctu
 klonování repozitáře:
 git clone <adresa z github zálozka SSH> (nastaveni vzdaleneho repozitare)
dojde ke stazeni repozitare do pc
dále muzeme vytvorit novou větev prikazem
git branch <název>
 a prepneme se do teto větve
git checkout <název větve>
nyni nejake zmeny a pak nutne zalozit novou branch v remote, to provedeme:
git remote
git push origin (selze pokud jsme vytvorili novou vetev, která není na remote a pouzijeme prikaz)
  git push --set-upstream origin <nazev branche> (vytvoříme vetev na remote a prepneme se do ni.)
   POZOR pri uprave v jinych nez mnou vytvorenych souborech, vznikaji konflikty!!!
```
------------------
## Prace s nove pridanou vetvi na githubu z jineho pc
--------------------
Pokud na jinem pc připojeném k projektu ve kterém vznikly nove větve chceme pracovat s novou větví
 je třeba nekoli kroku:
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
 ____________________
 ## Konflikty mezi branchemi (jsou změněny soubory, které jsou součástí master anebo více větví mezi programátory)
____________________
 je třeba provést ruční dekonflikci - tedy zjistit jaké změny mají být uloženy.
```
po odmazani pripojene větve pomocí:
git branch -d <nazev větve>je mozne ji vymazat i na remote prikazem 
  git push origin -d <branch-name>

Při vymazání branche na githubu je třeba zadat příkaz:
  git fetch --prune origin (tím dojde k odmazání branche i na lokále)
  ```

--------------------------------------------

git fetch (nacteni zmen oproti remote) lepsi je prikaz git pull, ktery se sklada ze dvou 
 prikazu (git fetch a git merge), ktery nacte zmeny na remote a slouci je do vetvi na working space
git pull (nacteni a slouceni zmen v pracovnim adresari-
 obsahuje dva prikazy git fetch a git merge)

____________________
Vracení se v čase po příkazech git commit a git add(lokálně)
  dvě kategorie po prikaze add a po prikaze commit
___________________
```
pro zapomenutí uložených změn slouží příkaz 
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