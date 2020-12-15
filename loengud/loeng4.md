# 4. loeng. Regulaaravaldised

## Regulaaravaldised

> "Some people, when confronted with a problem, think 'I know I'll use regular expressions.' Now they have two problems."
> 
> — Jamie Zawinski/Fredrik Lundh?

Regulaaravaldis (ingl *regular expression*) on erilises keeles üleskirjutatud valem, mis kirjeldab teatavat sõnede klassi. Regulaaravaldisest võib mõelda kui kontrolleeskirjast, mida rakendatakse (mingile) sõnele. Sõne kas vastab regulaaravaldisele või mitte. Regulaararvaldisest võib mõelda ka kui teatud tüüpi keelest, millel on oma reeglid. Selles keeles kirjutamiseks ja sellest arusaamiseks tuleb need reeglid ära õppida. Mõnikord võib avaldise tähendus märkide järjekorra muutmisel täielikult muutuda. Mõnikord on aga võimalik sama asja väljendada väga erineval viisil. Mõnikord sõltub tähendus kontekstist.

Regulaaravaldiste otsing töötab reeglina ühe rea piires, st et ei ole võimalik otsida sõnet, mis algab ühel real ja lõpeb teisel real. Regulaaravaldistega on võimalik otsida kindla pikkusega sõnu, korraga kõiki kirjavahemärke, ainult vokaale, konsonante jne, need on ainult mõned näited.

## MÕISTEID

- **Literaalne sümbol** (*literal*). Esinevad vaatlusaluses tekstis esitatud kujul, st esindavad regulaaravaldises iseennast.  
- **Metasümbolid** (*metacharacter*). Esindavad regulaaravaldises midagi muud (mitte iseennast).  
- **Otsitav sõne** (*target string*, *search string*). Sümbolite järjend, millele regulaaravaldis peaks vastama, teatud mõttes otsingu märksõna.  
- **Otsing, regulaaravaldis** (*search expression*). Regulaaravaldis või sümbolite järjend, mida kasutame otsitava sõne leidmiseks.  
- **Varjestamine** (*escaping*). Metasümboli muutmine literaalseks. Metasümboli saab muuta literaalseks, \\-märgiga, st erisümbolilt võetakse ära tema eritähendus ning peale varjestamist esindab see sümbol iseennast, on literaalne.  
- Suuri ja väikseid tähti loetakse erinevateks sümboliteks, st et *a* ja *A* ei ole sama asi.


## LIHTSAID OTSINGUID

*Ja dekanaat töötab Akadeemia tee 3 ruumis 339 (uue raamatukogu poolses küljes).*

**A**: Ja dekanaat töötab **A**kadeemia tee 3 ruumis 339 (uue raamatukogu poolses küljes).  
**aa**: Ja dekan**aa**t töötab Akadeemia tee 3 ruumis 339 (uue r**aa**matukogu poolses küljes).  
**3**: Ja dekanaat töötab Akadeemia tee **3** ruumis **33**9 (uue raamatukogu poolses küljes).  
**33**: Ja dekanaat töötab Akadeemia tee 3 ruumis **33**9 (uue raamatukogu poolses küljes).  
**u p**: Ja dekanaat töötab Akadeemia tee 3 ruumis 339 (uue raamatukog**u p**oolses küljes).  
**339 (uue**: Ja dekanaat töötab Akadeemia tee 3 ruumis **339 (uue** raamatukogu poolses küljes).  
**raamat**: Ja dekanaat töötab Akadeemia tee 3 ruumis 339 (uue **raamat**ukogu poolses küljes).
**m**: Ja dekanaat töötab Akadee**m**ia tee 3 ruu**m**is 339 (uue raa**m**atukogu poolses küljes).
**\\.**: Ja dekanaat töötab Akadeemia tee 3 ruumis 339 (uue raamatukogu poolses küljes)**.**  


## TRADITSIOONILISED METASÜMBOLID

**.**  - punkt: suvaline üks sümbol

**^** - (katus): rea algus, nurksulgude sees esimese märgina eitus. Katusemärgi saab klaviatuurilt kombinatsiooniga `Shift + AltGr + ä`.

**$** - (dollar): rea lõpp

**\\** - tagurpidi kaldkriips: teeb talle järgneva metasümboli literaalseks sümboliks


## KVANTORID

**\*** - tärn: suvaline arv, sh 0 temast vasakule jäävat sümbolit (null kuni lõpmatu arv kordusi)

**\+** - pluss: eelnev sümbol kordub üks või enam korda: *aa+* = *aa*, *aaa*, *aaaaa*, mitte *a*

**?** - küsimärk: eelnev sümbol kordub null või üks kord: *aa?* = *a*, *aa*, mitte *aaa*  

**{n,m}** - looksulud: mitu eelnevat sümbolit (nt *ai{2}* leiab *aii*; *ai{2,4}* leiab *aii*, *aiii* ja *aiiii*)  

**{n,}** - leiab vähemalt n eelnevat sümbolit

**{,n}** - leiab kuni n eelnevat sümbolit

**{n}** - leiab n eelnevat sümbolit


## KÜSIMUS. MIS ON ERINEVUS?

1. \+ ja {1,}
2. ? ja {0,1} ja {,1}


## HARJUTUS. KVANTORID JA LIHTSAD METASÜMBOLID OTSINGUS

*Ja dekanaat töötab Akadeemia tee 3 ruumis 339 (uue raamatukogu poolses küljes).*  
* Ära sellegipoolest lase end sellest heidutada, AB-veregrupiga inimesega koos ei hakka sul kunagi igav, nad on alati valmis lõbutsema.* 

Millised on allolevate otsingute tulemused neist kahest reast otsides?

.
^J
^ä
$
l+
a?
na?


## KLASSID

**\[...\]** - klass: üks \[\] vahel olevatest sümbolitest

Nurksulgude sees on erimärgid tavalises tähenduses. Nii leiab *\[akm\]* kas *a*, *k* või *m*. NB! Nurksulgudes saab niimoodi otsida ainult üksikuid sümboleid, *a* või *k* või *m*, aga mitte järjendit *akm*.  
Ka kompleksseid märke, nt *\w* ja *\S* (põhjalikumalt hiljem), võib kasutada nurksulgude vahel.  
Kui nurksulgude vahel on vaja kasutada sidekriipsu (literaalsena) või lõpetavat nurksulgu, siis tuleb see panna esimeseks märgiks sulgude sees, või peab talle eelnema tagurpidi kaldkriips. Nii leiab *\[\]abc\]* näiteks lõpetava nurksulu ja tähed *a*, *b* ja *c*.

Nurksulgudes on võimalik ka eitada, st mingid sümbolid otsingust välja arvata. Selleks tuleb ^ panna esimeseks märgiks sulgude sisse. Kui ^ ei ole esimene märk, siis kasutatakse teda (literaalsena) nagu iga teist märki. Nii näiteks leiab *A\[^5\]* järjendid *A4*, *A3*, *A2*, *A1*, *Aa*, kuid mitte *A5*. *\[^^\]* leiab kõik peale ^.


## VEEL METASÜMBOLITEST

\- tähistab vahemikku
| - toru: tähendus: või.
Järgnev regulaaravaldis: mina|meie leiab nii mina kui ka meie.
NB! Pane tähele erinevust [minameie] ja mina|meie vahel.


## KÜSIMUS. MIDA OTSITAKSE?

1. *\[ms\]ina*  
2. *mina|sina*


## LÜHENDATUD KLASSID

Lihtsad märgiklassid sisaldavad vaid üht või enamat literaalset märki, näiteks *\[abc\]* (sobivad tähed *a*, *b* või *c*) või *\[0123456789\]* (sobib iga number). Kuna tähtedel ja numbritel on loogiline järjekord, võib neid vahemikke määrates ka lühendada: *\[a-c\]* on sama, mis *\[abc\]* ja *\[0-9\]* on sama, mis *\[0123456789\]*. Selliseid konstruktsioone võib kombineerida näiteks *\[a-fynot1-38\]* (selle vastab *a*, *b*, *c*, *d*, *e*, *f*, *y*, *n*, *o*, *t*, *1*, *2*, *3* või *8*). Et suur- ja väiketähti käsitletakse erinevatena, siis tuleb tõstutundetu märgiklassi loomiseks, mis leiaks näiteks *a*, *b*, *A* ja *B*, kindlasti kirjutada *\[aAbB\]*.

Võimalik luua ka "negatiivseid" märgiklasse, kus sobib "kõik, välja arvatud". Selleks tuleb klassi alguses märkida katusega ^.
*\[^abc\]* tähendab, et sobib iga märk, välja arvatud *a*, *b* või *c*.  
*\[^ \]\** tähendab, et sobib kõik peale tühiku.
*\[^ \]\** tähendab, et otsitakse kõiki sümboleid ükskõik kui palju, kuid mitte tühikuid.
*\[0-9\]* – otsitakse numbreid.
Aga kõik tähed? Milline tähestik? *\[a-zA-Z\]* *\[a-üA-Ü\]*?
Kirjakeele korpuste [kasutajaliideses](http://www.cl.ut.ee/korpused/kasutajaliides/) *\[a-z\]*, aga täpitähti esitavad olemid jäävad neist klassidest ikkagi välja.


## EELDEFINEERITUD KLASSID

Ei kehti kirjakeele korpuste kasutajaliideses, aga nt enamasti programmeerimiskeeltes olemas.
**\[:alpha:\]** tähestiku tähed
**\[:upper:\]** suurtähed
**\[:lower:\]** väiketähed
**\[:digit:\]** numbrid
**\[:punct:\]** kirjavahemärgid


## HARJUTUSI

1. Milline regulaaravaldis vastab tervele reale, ükskõik mida ja ükskõik millisel hulgal ta sisaldab?  
2. Milline regulaaravaldis vastab reale,  
	- mis sisaldab ainult tühikuid?  
	- mis ei sisalda ühtegi tühikut (aga ükskõik mida muud ükskõik kui palju)?  
	- milles on mõni number?  
	- milles pole ühtegi numbrit?  
	
	
## KOMPLEKSSED MÄRGID

Koosnevad tagurpidi kaldkriipsust (\\) ja ühest alltoodud märkidest. Kui \\ järel ei ole üht allpooltoodud märkidest, siis otsitakse \\-le järgnevat märki ennast.  
Nii näiteks leitakse \\$ vasteks dollarimärk.

\\A - Leiab rea alguse (sama mis ^).
\\b - Leiab sõna alguse ja lõpu.

Sõna defineeritakse kui tähtede-numbrite ja allkriipsude jada, nii et sõna lõppu tähistab tühik või märk, mis ei kuulu tähtede, numbrite ega allkriipsu hulka. Kuna täpitähed ja "susisevad" tähed kirjakeele korpuste [kasutajaliideses](http://www.cl.ut.ee/korpused/kasutajaliides/) sisaldavad ampersandi (&) ja semikoolonit (;), siis ei kuulu nad selle definitsiooni kohaselt sõna hulka, nagu ka sidekriips.  

**\t** või **\011** - tabulaator  
**\n** või **\012** - nn *newline*, Unixi/Linuxi reavahetus ja sageli selline ka tavalistes tekstiredaktorites.  
**\r** või **\015** - nn Windowsi reavahetus. NB! Windowsi tekstifailides on rea lõpus **\r\n** Oluline teada, kui kasutad tulevikus tekstitöötlemiseks skripte: **\r\f** *form feed* (uus lehekülg; leheküljevahetus)  
**\v** - vertical tab, nn vertikaalne kriips
**\d** - kõik numbrid, samaväärne väljendiga **\[0-9\]**.
**\D** - kõik mittenumbrid, samaväärne väljendiga **\[^0-9\]**.
**\s** - kõik "valged vahed", samaväärne väljendiga **\[ \t\n\r\f\v\]**.  
**\S** - kõik mitte-"valged vahed", samaväärne väljendiga **\[^ \t\n\r\f\v\]**.
**\w** - leiab iga tähe, numbri või allkriipsu, samaväärne klassiga **\[a-zA-Z0-9_\]** kasutajaliideses, AGA ei otsi html-täpitähti.
**\W** - leiab iga mitte-tähe, mitte-numbri või mitte-allkriipsu, samaväärne väljendiga **\[^a-zA-Z0-9_\]** kasutajaliideses. NB! html-olemid.
**\Z** - rea lõpp, samaväärne $-ga.


## "AHNED" (*GREEDY*) JA "LAISAD" (*LAZY*) PÄRINGUD

Kvantorid on vaikimisi "ahned", st et regulaaravaldisele vastab maksimaalne sobiv üksus. Sageli pole see aga soovitud tulemus. Ahne päringu saab laisaks muuta ?-ga.

Näide:

*Kuna rahast meeldib kõigile rääkida , siis püüangi järgnevalt seletada veebilansi müüdi olemust tavalise pere rahakoti mudeliga .*

Kuidas otsiksid sellest lausest *r*-ga algavaid sõnu?

Mida otsib "**r.\***"?
Aga " **r.\*?** "?

**Kuidas otsida sellest tekstist ainult kõiki lauseid?**

*<p> <s> Võib-olla on aga praegusaja vanemaist teismelistest eakamad põlvkonnad juba lootusetult kadunud , et niisugusest " keelest ” aru saada ? </s> <s> Sallivust ja mõistmist , et kõik ei ole ega peagi olema ühesugused , pole siin maailmanurgas just kaua kuulutatud . </s> <s> Seda teemat käsitleti sovetlikus ühiskonnas peamiselt hea – halva skaalal : siledad , ühetaolised ja ohutud on " meiega ” . </s> <s> On head ja " normaalsed ” . </s> <s> Teistsuguseid meil peaaegu ei olegi , või kui , siis on nad vaenlased või muidu väärdunud . </s> </p>*


## RÜHMAD JA TAGASIVIITAMINE

Tavaliste sulgudega saab moodustada ka rühmi, millele on võimalik n-ö tagasi viidata või avaldist korrata. Sellisel juhul pole sulud osa otsitavast avaldisest, vaid tähistavad mingi vahemiku algus- ja lõpp-positsiooni näiteks (@[^ ]*). Tagasiviitamiseks on võimalik koostada ka rohkem gruppe ja tagasi viidatakse sel juhul esinemisjärjekorras: \1, \2.

Näide:
tere, tere, vana kere

Kuidas leida selle näite eeskujul juhtumid, kus sõna tere esineb kaks korda järjest?
Kuidas samast näitest teha otsing kahe grupiga, nii et leitaks nii tere kui ka talle järgnev koma ja tühik?
Kuidas tagasiviitamist ja rühmi kasutades vahetada sõnade vana ja kere järjekord?










https://xkcd.com/208/


LISAMATERJALE

Mõned selgitavad videod:
https://www.youtube.com/watch?v=hwDhO1GLb_4
https://www.youtube.com/watch?v=RGLldper5II
https://www.youtube.com/watch?v=DRR9fOXkfRE
Kirjakeele korpuste kontekstis
Väga hea sissejuhatav ülevaade
Näiteid, viiteid õpetusi: http://www.regular-expressions.info/
Regulaaravalidsi valmiskujul: http://regexlib.com/?AspxAutoDetectCookieSupport=1
Testi oma avaldist: http://www.regexpal.com/, http://regexr.com/
Sissejuhatav ülevaade: http://www.zytrax.com/tech/web/regex.htm
Regulaaravaldiste spikreid: [1], [2], [3]


Midagi eestikeelset


Markus Dickinsoni loenguslaidid
Mõnest edasijõudnumast teemast