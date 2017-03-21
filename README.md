# Tim21-Hepek
Dino Gafi� , GitHub ime: DinoGaf
Nadza Vrazalica

Tema:
International Space Station (ISS)
"Of the people , by the people , for the people" - Abraham Lincoln

1. Generalni opis teme
Cilj ovog projekta jeste da se simulira odr�ivi na�in rada i odr�avanja ISS. Svrha sistema je da osigura kontinualan i neprekidan
lanac dostave osoblja i tereta na samu stanicu , uskla�en sa potrebama stanice i eksperimenata koji se vr�e u stanici ili orbiti 
oko stanice.
Problemi koji se susre�u jeste veoma ograni�en skladi�ni prostor u samoj ISS , dodavanje novih modula (ekstenzija) na stanicu
i najve�i preoblem : redovno odr�avanje stanice. Da bi se rje�ili ovi problemi , pojavljuju se novi podproblemi : kako sve
potreb�tine dovesti do stanice , i kako osigurati neprekidno snadbjevanje najosnovnijim potreb�tinama.
Ovaj sistem rje�ava ovaj problem tako �to tra�i od ISS da po�alje zahtjev zemlji za stavi koje treba. Nakon �to taj zahtjev biva procesuiran na zemlji
, onda se �alje prijedlog plana na razmatranje stanici. Stanica mo�e da da zeleno svjetlo da se dostave potrebni resursi po planu ,
modifikuje taj plan prema svojoj listi prioriteta i/ili odbije plan u potpunosti.
Razlog za kupovinu ovog sistema je o�igledan : s obzirom na ogromni tro�ak izgradnje i odr�avanja ISS , kao i dostave resursa
u svemir , svaka optimizacija �e u�tediti milijone ako ne i milijarde (dolara , eura , maraka , jena , itd.) na globalnom nivou.
Tako da je cilj u tezama:
- Odr�avanje ISS u svemiru.
- Odr�avanje �ivotne sredine u ISS i redovnih eksperimenata.
- Optimizacija resursa i osoblja.
- Dostava resursa i osoblja neovisno o polo�aju ISS.
+ Summoning the old ones to annihilate humans and make survivors submit to their new master - C'thulu. (Option 2 was letting J.J. Abrams reboot ISS. We can all agree mankind narrowly dodged a bullet there.) 

2. Aktori
Imamo tri klju�na aktora:

ISS - Internacionalna svemirska stanica. ISS radi dvije bitne stvari : naru�uje misije i provjerava plan misije.
Naru�ivanje misije se vr�i po internoj listi prioriteta , tj. po li�nom naho�enju , a provjeravanje se vr�i nakon �to
druga dva aktora pro�itaju naru�benicu i dadnu njihovu procjenu kako bi se misija mogla izvr�iti. ISS daje zeleno svjetlo
(nazvano Finalni izvje�taj (o misiji)) ukoliko je saglasan sa planom , te da se postupi po istom. Naravno , ISS mo�e da 
odbije predlo�eni plan , ali ima i tre�u opciju , ukoliko je plan sli�an predlo�enom planu , tada mo�e da izmjeni naru�benicu
, ali iz sigurnosnih razloga , izmjenjena naru�benica prolazi kroz isti proces kao da je nova naru�benica.

Houston - zajedni�ko ime za kontrolu lansiranja. Houston je zadu�en da prati koje su platforme slobodne i koje su rakete/moduli
(ima putni�ki modul i teretni modul za raketu) dostupne za koju platformu. Houston je tako�e zadu�en da prati koordinate
ISS da bi se resursi mogli lansirati i dovesti na stanicu bez pretjeranih odlaganja. Po registrovanju naru�benice za misiju , 
houston �alje raspored leta , koji sadr�i datum kada se teret mo�e lansirati na ISS , te sa koje platforme se mo�e lansirati za ISS , 
te koliko je letjelica dostupno za tu platformu.

NASA - zajedni�ko ime za proizvo�a�e resursa koji idu u svemir. Uloga nase jeste da proizvodi i skladi�ti sve neophodne resurse za ISS.
Po registrovanju naru�benice za misiju , NASA poredi listu resursa datu u naru�benici sa svojom listom resursa. Nakon procesiranja , NASA
�alje listu dostupnih (tj. uskladi�tenih) resursa , te jo� jednu listu , ukoliko je ISS naru�io elemente koje NASA nema na lageru , tada
NASA stvara dodatnu listu u kojoj se nalazi ime resursa , da li se mo�e proizvesti , i ukoliko se mo�e proizvesti , kada �e biti proizveden.

* NASA i Houston imaju pristup prethodnim Finalnim Izvje�tajima , na osnovu kojih mogu da interno stvore svoju listu najkori�tenijih resursa
  da bi te iste mogli skladi�titi i tako pomo�i ubrzanom izvr�avanju misija.

3.Procesi
Klju�ni proces je: Naru�ivanje (ili biranje/smi�ljanje) Misije , koji vr�i ISS.
Nakon �to ISS na osnovu svoje interne liste prioriteta izabere �ta mu treba , stvara tzv. obrazac , koji sadr�i ime misije ,
datum (planiranog) po�etka misije , datum  (planiranog) kraja misije , kratki opis misije (npr. Odr�avanje mlaznica i eksperiment
formiranja manjih asteroida ) , i najbitnije , lista potrebnih resursa i osoblja (ukoliko nema astrounauta tra�ene struke
na ISS ) da se ta misija izvr�i.
Nakon �to se napravi naru�benica , naru�ba ide u tzv. "pending" stanje. Dok je u ovom stanju NASA i Houston pristupaju naru�benici
i vr�e sljede�e podprocese:
Houston - Stvaranje Rasporeda Leta - Ovaj proces ( Zajedno sa uklju�enim podprocesima : Provjera Dostupnih Modula/Letjelica , Provjera Lokacija Rampa za Lansiranje)
za cilj ima da stvori dokument koji sadr�i ime i lokaciju slobodne rampe sa koje se mo�e lansirati , letjelice koje su dostupne za tu rampu i moduli koji su dostupni
za te letjelice. Nakon �to stvori dokument nazvan raspored leta , taj se �alje nazad u ISS da bude spreman za sljede�i proces.
NASA - Stvara Listu Djelova/Osoblja Potrebnog za Misiju - ( Zajedno sa uklju�enim podprocesima : Provjera Dospnih Astronauta , Provjera Djelova na Lageru , Provjera da li se 
Dio mo�e Napraviti i Procjena kada �e taj Dio biti Napravljen ) koji �e kao cilj stvoriti dvije liste , jedna je lista resursa koji dostupni , a druga je lista resursa koji
se mogu ili ne mogu napraviti. Te dvije liste se �alju nazad u ISS da bude spreman za sljede�i proces.
Kada Houston i NASA po�alju njihove liste u ISS , naru�benica izlazi iz "pending" stanja i ulazi u proces Predlaganja Kako se Misija Mo�e Izvr�iti.
Ovaj proces upore�uje liste i datume u naru�benici sa onim koje su poslali Houston i NASA i stvara protip plana izvr�avanja , tj. kako bi se resursi mogli dostaviti
u ISS tako da ISS radi bez zastoja. Nakon �to se stvori ovaj prototip , ISS ga interno upore�uje sa listom prioriteta i stvaraju se tri stanja - Zeleno Svjetlo ( 
Prototip plana izvr�avanja misije se sla�e sa prioritetima ISS-a, tada se stvara zavr�ni raport i misija formalno po�inje) , �uto Svjetlo ( Prototip plana izvr�avanja 
misije je vrlo blizu blizu tra�enih prioriteta , tada se naru�benica koriguje i ponovo se vr�i naru�ivanje misije sa korigovanom naru�benicom) , Crveno Svjetlo
(Ukoliko se protitp vrlo malo sla�e sa prioritetima ISS , tada se naru�benica otkazuje ).

4. Funkcionalnosti
Sistem nudi sljede�e funkcionalnosti:
- Mogu�nost naru�ivanja i pra�enja toka naru�benice
- Najoptimalnije rje�enje za svaku naru�benicu
- Pregled i statistike resursa poslanih na prethodne misije kroz analizu finalnog izvje�taja
- Pregled/Pra�enje Dostupnog Osoblja
- Pregled/Pra�enje Dostupnih Resursa 
- Pregled/Pra�enje Osoblja u ISS
- Pregled/Pra�enje Resursa u ISS
- Pregled/Pra�enje Eksperimenata u ISS
- Naru�ivanje Resursa
- Pra�enje Stanja ISS i Slanje Upozerenja u Slu�aju Nedostatka Resursa