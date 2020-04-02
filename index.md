---
title: Witryna Komisji IT PZBS
---

## Obsługa rozgrywek

<div class="row">
<div class="col">
### Punkty klasyfikacyjne (PKL)
#### [Kalkulator](http://pzbs.pl/sedziowie/pkl/pkle2018.php)
Formularz obliczający PKL dla turniejów zgodnie z pkt. 9 [Regulaminu Klasyfikacyjnego PZBS](https://www.pzbs.pl/regulaminy-stale/2340-regulamin-klasyfikacyjny).
#### API dla programistów
Interfejs programistyczny udostępniający aktualne obliczenia PKL: [dokumentacja](doc/api-pkl/).
</div>
<div class="col">
### SquareDeal
Procedura zapobiegająca manipulacji rozkładami rozdań, poświadczająca ich losowość.
- [opis procedury](http://www.pzbs.pl/sedziowie/inne/procedura-generowania.pdf)
- [instrukcja](https://emkael.github.io/2019/01/03/generating-and-verifying-boards-with-squaredeal/)
- [wykaz rozgrywek PZBS z wdrożoną procedurą](https://pzbs.github.io/square-deal/)

### Tabele IMP -&gt; VP
[Generator tabel VP](https://www.pzbs.pl/sedziowie/vp/).
</div>
</div>

## Wykaz odnośników do oprogramowania

<div class="row">
<div class="col">
### [Tournament Calculator](https://www.pzbs.pl/nowosci/4665-program-tournament-calculator)

### [JFR Teamy / Pary](https://www.pzbs.pl/pary-teamy)

</div>
<div class="col">

### [Zegar sędziowski](http://jfr.pzbs.pl/zegar.html)

### [CongressScore](https://michzimny.pl/congressscore-info)
 - obliczenia punktacji długofalowych

</div>
</div>

<div class="row">
<div class="col">
### [Aktywator](https://michzimny.pl/aktywator)
 - obsługa zaawansowanych opcji systemu BridgeMate

### [FillBWS](https://michzimny.pl/fillbws)
 - narzędzie do szybkiego uzupełniania zapisów w pliku BWS
 - wbudowany wykrywacz "burtówek"

### [Proximity Printer](https://github.com/PZBS/proximity-printer)
 - wydruk historii z użyciem kart zbliżeniowych
</div>
<div class="col">
### [Bridge Calculator](http://bcalc.w8.pl/) (bcalc)
 - silnik obliczeń rozgrywki "w widne" oraz "w zakryte"

### [BCDD](https://github.com/emkael/bcdd)
 - zapis informacji o rozgrywce "w widne" w rozkładach w plików PBN
 - używa bcalc jako silnika obliczeń

### [Deal Converter](https://deal.emkael.info/)
 - konwerter formatów zapisu rozkładów rozdań
 - dostępna [wersja off-line](https://github.com/emkael/deal-convert)

</div>
</div>

## Programy pomocnicze

<div class="row">
<div class="col">
### JFR Teamy
 - [samouczek / instrukcja obsługi](http://www.warsbrydz.pl/druki/Admin.pdf)
 - [teamy-diff-deals](https://github.com/michzimny/teamy-diff-deals)
   - obsługa różnych rozkładów na różnych stołach
   - ukrywanie zapisów do momentu zagrania rozdania na wszystkich stołach
 - [teamy-playoff](https://github.com/emkael/jfrteamy-playoff)
   - generator drabinek knock-out/play-off
 - [teamy-ausbutler](https://github.com/emkael/jfrteamy-ausbutler)
   - znormalizowany ("Australijski") butler
 - [teamy-patton](https://github.com/emkael/patton)
   - obliczanie turniejów systemem Pattona
</div>
<div class="col">
### JFR Pary
 - instrukcje/poradniki:
   - [prowadzenie turnieju na IMP](doc/pary-impy.pdf)
   - [prowadzenie turnieju "barometrem"](doc/pary-barometr.pdf)
 - [pary-bidding-data](https://github.com/emkael/jfrpary-bidding-data)
   - wyświetlanie przebiegu licytacji zbieranego z BridgeMate'ów
 - [pary-virtual-table](https://github.com/emkael/jfrpary-virtual-table)
   - ukrywanie "wirtualnych" stolików w przypadku liczenia turnieju do znanej średniej
   - [instrukcja prowadzenia turnieju](https://emkael.github.io/2018/02/04/jfr-pary-virtual-table-tournament/)
 - [Zimny Goniec](https://michzimny.pl/zimny-goniec)
   - odpowiednik Gońca, poprawiający niektóre problemy z kompatybilnością z serwerami FTP
</div>
</div>

## Dydaktyka

<div class="row">
<div class="col">
### Kursokonferencje
#### [KKS IT 2018](http://kkt.pzbs.pl/kkt-2018/)
</div>
<div class="col">
### Artykuły / poradniki
 - [KoPS: instrukcja](http://jfr.pzbs.pl/kopsinstrukcja.html)
 - [diagnostyka zapytań wykonywanych do plików BWS](https://emkael.github.io/2018/02/28/debugging-queries-to-bws/)
</div>
</div>

## Materiały dla WZBSów i inne

<div class="row">
<div class="col">
### [TechSoup Polska](https://www.techsoup.pl/pl/item-details/904/program-techsoup-polska)
 - darmowy pakiet G Suite zawierający m.in. pocztę firmową i przestrzeń w chmurze
 - używany sprzęt komputerowy w świetnym stanie oraz z 2 letnią gwarancją
 - najnowsza wersja MS Office z dożywotnią licencją za 200 zł
 - Windows 10 Professional za 50 zł (do 50 licencji, jednorazowy zakup)
 - i inne
<div class="col">
### [GitHub PZBS](https://github.com/PZBS/)
 - loga PZBS w wysokiej rozdzielczości
 - inne publiczne repozytoria
</div>
</div>
