# 6. loeng. Tere, terminaliaken!

## Töö terminaliga, käsurida ja Unixi käsud

Praktikumides kasutame [Bitvise](https://www.bitvise.com/download-area)'i, aga arvutiklassi arvutites on olemas ka näiteks [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/) ning kasutada võib mis tahes endale meelepärast rakendust.
Suvalisest arvutist saab sisse logida ssh-terminaliakna abil ülikooli Linuxi-serverisse **adalberg.ut.ee** (täpitähtede kuvamiseks vt [siia](http://anti.teamidiot.de/nei/2007/02/irssi_putty_screen_unicode_utf/) ja ülikooli serverisse logimise kohta [siia](https://wiki.ut.ee/pages/viewpage.action?pageId=17105728)).  

Linuxi graafilise keskkonna kasutamiseks (GNOME, KDE) installeerida arvutisse [NX Client](http://web10.nomachine.com/download).

Praktikumide materjalid on kaustas:
`/home/mustikas/k/kriztel5/korpustePraktikumid`


## KESKKONNA SEADISTAMINE

Kontrolli, millist shelli kasutad (oleneb ülikooli kasutajakonto seadistustest, mida sa ise püsivalt muuta ei saa).

```
which $shell  
which $SHELL  
echo $0  
```
Vaata olemasolevaid shelle.

```
cat /etc/shells  
```

Kui sinu masin kasutab midagi muud peale tcsh, siis saad seda ajutiselt muuta nii (iga kord peale sisse logimist):

```
exec /bin/tcsh  
```

Kõige lihtsam on aga kirjutada oma skriptid faili ja esimesel real defineerida, millist shelli peaks käivitatav skript kasutama.

```
#! /bin/bash  
#! /bin/tcsh  
#! /bin/sh  
jne
```

tcsh kasutamine ei ole kohustuslik, aga praktikumides esitatud näited on tcsh-põhised. Koduste tööde skripte võib esitada endale sobivas shelli versioonis.  

Linke, millest võib seadistamisel abi olla: [1](http://www.thegeekstuff.com/2009/10/change-login-shell-from-bash-to-sh-csh-ksh-tcsh/), [2](http://stackoverflow.com/questions/4132661/run-csh-scripts-from-bash-change-shell-temporary-via-command), [3](http://unix.stackexchange.com/questions/20629/how-to-change-from-csh-to-bash-as-default-shell).  

Mõnest bashi ja tcsh [erinevusest](http://www.thegeekstuff.com/2009/10/change-login-shell-from-bash-to-sh-csh-ksh-tcsh/).

Täpitähtede seadistamine käsurealt

```
setenv LANG et_EE.UTF-8  
export LANG=et_EE.UTF-8
```

Kui tekib probleeme, siis kasuta pigem

```
setenv LANG en_US.UTF-8  
export LANG=en_US.UTF-8
```

Kehtib ainult selles aknas kuni akna sulgemiseni. Parem on seadistada kodeering kohe sisselogimisel.

Käsud töötavad põhimõttel:

käsk  \[-lipuke/täpsustav kriteerium] \[argument]

Rohkem infot iga käsu kohta:

```
man käsuNimi  
käsuNimi --h  
```

## TÖÖ LIHTSUSTAMISEKS

**Nooleklahv üles**: näita eelmist käsku, mille sisestasid  

**Ctrl + u**: kustuta käsurida  

**Ctrl + a**: mine käsurea algusesse  

**Ctrl + c**: katkesta protsess  

**Ctrl + l** või ***clear***: puhasta aken  

**TAB**: lihtsustab trükkimist  

**q**: välju teksti lehitsemisest (*quit*)   

Välju masinast:  

```
exit  
```


## TÖÖ KATALOOGIDEGA/KAUSTADEGA

Töökataloogi vahetamine (cd \- *change directory*)

```
cd kataloog1/kataloog2/…/soovitudKataloog

# tagasi kodukataloogi
cd

# üks samm töökataloogist tagasi
cd ..
```

```
#Mis on töökataloogis (ls - list)?

ls
ls kataloogiNimi

#Detailsemalt kataloogis olevate failide ja alamkataloogide kohta

ls -l
ls -l kataloogiNimi

#Näita ka n-ö peidetud faile
ls -a

#Kataloogi sisu rekursiivselt
ls -R

#Kus ma olen?
pwd

#Kes ma olen?
who
whoami

#Millistesse gruppidesse kuulun?
groups kasutajaNimi

#Kataloogide ja failide sisu sirvimine kitsendatult
less
more
head
tail
head -25
tail -25

#Loo uus kataloog (mkdir - make directory)
mkdir KataloogiNimi

#Kustuta kataloog (rmdir - *remove directory*)
rmdir kustutatavaKataloogiNimi

#Kustuta fail (rm - remove)
rm kustutatavaFailiNimi
```

Kustuta kataloog ja kõik tema alamkataloogid koos oma sisuga, rekursiivselt (NB! Selle käsu kasutamisel ole ettevaatlik ja veendu, et soovid tõepoolest kõike kustutada.)

```
rm -r kustutatavaKataloogiNimi

#Küsi faili kustutamisel nõusolekut
rm -i
```


## TÖÖ FAILIDEGA

Mis on failis? Faili sisu vaatamine (cat \- *concatenate*, *catenate*)  

```
cat failiNimi
cat failiNimi | less
cat failiNimi | head
cat failiNimi | tail
cat failiNimi | less
cat failiNimi | head -10
cat failiNimi | tail -3
```

Faili sisu ülevaade. Kui palju on failis ridu, sõnu, sümboleid (wc - *word count*)  

```
cat failiNimi | wc
```

Kopeeri faile (cp - *copy*)  

```
cp kopeeritafaFailiNimiVõiTeekond kuhuKopeeridaTeekond
```

Liiguta/teisalda faile, nimeta fail ümber (mv - *move*)  

```
mv vanaFailiNimi uueFailiNimi
mv vanaFailiNimi uueFailiNimiKoosTeekonnaga
```

Vaata kõiki faile, mis lõpevad, sisaldavad, algavad etteantud ühisosaga failinimes.

```
ls ühisosa*
ls *ühisosa*
ls *ühisosa
```

Faili õiguste muutmine: chmod - *change mode*  
u = **u**ser, g = **g**roup, o = **o**thers, a = **a**ll  

\+    anna õigused  

\-    võta õigused ära  

**r**  lugemisõigused (*read*)   

**w** kirjutamisõigused (*write*)  

**x** käivitamisõigused (*execute*)  

```
# Näiteks

chmod o+x failiNimi
chmod u-w failiNimi
chmod ugo-rw failiNimi
```

Väljundi suunamine uude faili (või n-ö salvestamine): > ja >>

```
# uus fail kirjutatakse ümber/üle
cat failiNimi > uueFailiNimi


# faili sisu lisatakse olemasoleva faili lõppu
cat failiNimi >> väljundFailiNimi
```

## FAILIST OTSIMINE, ASENDAMINE, KUSTUTAMINE. GREP, TR

grep otsib ridu etteantud mustri järgi:  

```
grep ’maja’
grep ’#’
```

Otsingule on võimalik lisada eritingimusi.  
**-i** ei tee vahet suurtel ja väikestel tähtedel  
**-v** otsib ridu, mis ei sisalda mingit mustrit / viskab välja read, mis sisaldavad etteantud mustrit  
**-n** näitab väljundis lisaks rea numbrit, kus otsitav märk või märgijada leiti  
**-c** väljastab otsingule vastavate ridade arvu  
**-2** lisab konteksti otsingule vastava rea ümber kaks rida ette ja taha  

Võib kasutada mitut lipukeste korraga, näiteks  

```
grep –vc ’maja’
```

Vaata ka **egrep** ja **fgrep**.  

Sümbolite teisendamine ja kustutamine: **tr** (*translate*)  

```
# Muuda kõik suured tähed väikesteks

tr '[:upper:]' '[:lower:]'
tr '[A-Z]' [a-z]'

# Asenda numbrid suure A-tähega

tr '[0-9]' 'A'

# Asenda trellid @-märgiga

tr '#' '@'

# Asenda reavahetused tühikuga.

tr '\012' ' '
```

Sümbolite kustutamine **-d** (*delete*). Mõned näited:  

```
tr -d '\012'
tr -d '@'
tr -d '[0-9]'
```

Korduvate sümbolite kustutamine **-s**. Näiteks kustuta kõik korduvad *a*-tähed (*aa*, *aaa*, *aaaa* … > *a*)

```
tr -s 'a'
```

NB! tr "tõlgib" ühe baidi teiseks baidiks, aga utf8-s on mõned sümbolid esitatud mitme baidi abil, seega tr ja utf-8 kodeering ei ole päris hästi kooskõlas. Võib kasutada nt tühiku, reavahetuse asendamiseks, aga muul puhul olla ettevaatlik.

## SED. PIKEMATE MÄRGIJADADE ASENDAMINE JA KUSTUTAMINE, GRUPEERIMINE

Pikemate märgijadade asendamiseks ja kustutamiseks (asendus mitte millegagi).

```
sed 's/asendatav/asendus/'
sed 's/asendatav/asendus/g'
```

Esimene variant asendab ainult iga rea esimese tabamuse. Teine variant (**g** = *global*) asendab kõik real leitud tabamused.  

**sed**-ga on võimalik kasutada ka grupeerimist. Selleks kasutatakse sulge, mille ette on lisatud tagurpidi kaldkriipsud. Gruppidele on võimalik tagasi viidata (töötab samamoodi nagu kasutajaliidestes).  

```
# lisa kahe järjestikuse a-tähe ette ja taha alakriipsud
cat fail | sed 's/\(aa\)/_\1_/g'

# ühe grupi puhul on samas funktsioonis võimalik aksutada ka &-märki
# sisuliselt sama, mis eelmine
cat fail | sed 's/aa/_&_/g'
```


## CUT

Töötleb teksti kui tabelit, selleks peab olema tekstifailis veergudel üks kindel eraldaja.  

**-d** selle käsu puhul märgib *d* (*delimiter*) välja eraldajat  
**-f** (*field*) anna ette, mitmes väli "ära lõigata"  

```
# lõika failist välja kõik, mis algab kolmandast väljast (jäta alles ainult kaks esimest välja), välju eraldab %-märk
cat test.txt | cut -d % -f 1-2

# lõika failist välja kõik, mis algab kolmandast väljast (jäta alles ainult kaks esimest välja), välju eraldab tühik
cat test.txt | cut -d " " -f 1-2

# lõika failist välja osa, mis algab teisest väljast (eemalda esimene väli), välju eraldab tühik
cut -d " " -f 2-
```


## SORTEERIMINE. SORT

**sort** järjestab read, vaikimisi tähestikulises järjekorras

**sort –n** sorteerib ridu kui arve (*numeric*)  
**sort –r** sorteerib vastupidises järjekorras (*reverse*)  

**uniq** jätab identsetest ridadest alles vaid ühe, fail peab olema eelnevalt sorteeritud  

**uniq –c** loeb identsed read ka kokku (*count*)  


## ERISÜMBOLEID

**\t**: tabulaator  

**\011**: tabulaator  

**\n**: Linuxi reavahetus  

**\012**: Linuxi reavahetus  

**\015**: Windowsi reavahetus  


## NÄITEID

Käske võib omavahel kombineerida, eraldades need |-ga.

```
# Võta failist välja read, kus esineb sõna maja, ja suuna tulemus uude faili.

cat algfail | grep 'maja' > väljundfail

# Võta failist välja read, kus esineb sõna maja.
# Asenda seejärel maja sõnaga hoone.
# Muuda tekst suurtäheliseks.
# Lisa tulemus juba olemasolevasse faili.

cat sisendfail | grep 'maja' | sed 's/maja/hoone/' | tr '[:lower:]' '[:upper:]' >> väljund
```


## LISAMATERJALE

[Tere, terminaliaken!](https://drive.google.com/file/d/0BzzoDgAQIa9nY0JINXhlM0xuV0U/view)  

[Unix for corpus users: a beginner's guide](http://www.port.ac.uk/media/Media,168754,en.pdf)  

[Unix for Poets](http://web.stanford.edu/class/cs124/kwc-unix-for-poets.pdf)  

[Unix Tutorial for Beginners](http://www.ee.surrey.ac.uk/Teaching/Unix/index.html)  

[Bash Quick Reference](../failid/Bash-Quick-Reference-pdf)  


## HARJUTUSI

1. Tekita oma kodukataloogi uus kataloog, näiteks *kirjakeel*.  
2. Kopeeri minu kodukataloogi alamkataloogist `/home/mustikas/k/kriztel5/korpustePraktikumid` fail `1900_aja`.  
3. Liigu oma kodukataloogi, kuhu selle faili kopeerisid (kui sa juba pole seal).  
4. Nimeta kopeeritud fail ümber failiks `aja_1900.txt`.  
5. Vaata ümbernimetatud faili \25 esimest rida.  
6. Vaata ümbernimetatud faili \10 viimast rida.  
7. Mitu rida, sõna ja sümbolit selles failis on?  
8. Kopeeri endale SLOhtulehe failidega kaust (terve kausta kopeerimiseks **cp -r**)  