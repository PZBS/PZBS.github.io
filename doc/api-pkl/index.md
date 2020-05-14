---
---

Kalkulator PKL - API
====================

API dostępne jest pod adresem: [http://pzbs.pl/sedziowie/pkl/api.php](http://pzbs.pl/sedziowie/pkl/api.php) i akceptuje parametry HTTP metod GET lub POST.

Parametry (standardowe)
-----------------------

| Parametr        | Opis               | Wartości |
| --------------- | ------------------ | -------- |
| type            | typ turnieju       | `1` = indywiduel, `2` = pary, `4` = teamy |
| contestants     | liczba uczestników | liczba całkowita dodatnia |
| title_sum       | suma WK            | liczba nieujemna |
| tournament_rank | ranga turnieju     | `0` = klubowy, `1` = okręgowy, `2` = regionalny, `3` = OTX, `4` = OTX\*, `5` = OTX\*\*, `6` = OTX\*\*\*, `7` = OTX\*\*\*\*, `101` = KMP, `102` = BridgeNET Lokalny |
| over39_boards   | liczba rozdań      | `0` = mniejsza niż 40, `1` = co najmniej 40 |

W standardowym trybie użycia API wszystkie powyższe parametry są obowiązkowe.

API przyjmuje również opcjonalne parametry:

| Parametr | Opis              | Wartości | Wartość domyślna |
| -------- | ----------------- | -------- | ---------------- |
| players  | liczba zawodników | liczba całkowita dodatnia | `contestants` \* `type` |
| version  | wersja regulaminu | patrz poniżej | `'2'` |
| boards   | liczba rozdań     | liczba całkowita nieujemna |

Paramter `players` służy do wyliczenia prawidłowego średniego WK dla turniejów teamów nieczteroosobowych. Jest on używany *tylko* do wyliczenia średniego WK, drugi składnik maksymalnej liczby PKL dla turnieju wciąż wyliczany jest zgodnie z pkt. 9 Regulaminu Klasyfikacyjnego - jako `contestants` \* `type`.

Parametr `boards` może przesłonić wartość parametru `over39_boards`, jest on poza tym **obowiązkowy** dla turniejów typu BridgeNET Lokalny (`tournament_rank` = `102`).

Parametr `version` pozwala na określenie wersji Regulaminu Klasyfikacyjnego (lub regulaminów zawodów) według którego wyliczane są PKLe. Dozowolone wartości:
 * `'1'` - Regulamin Klasyfikacyjny 01.11.2018, Regulamin KMP sprzed 01.01.2020
 * `'2'` - Regulamin Klasyfikacyjny 01.11.2018, Regulamin KMP od 01.01.2020
 * `'3'` (domyślna) - Regulamin Klasyfikacyjny od kwietnia 2020, Regulamin KMP od 01.01.2020, Regulamin BridgeNET Lokalny od 01.05.2020

Wartością domyślną jest **zawsze** wartość odpowiadająca bieżącemu stanowi prawnemu.

Parametry (zaawansowane)
------------------------

API akceptuje również parametry pozwalające ręcznie ustalić wagę turnieju, minimum PKL za pierwszej miejsce oraz parametry funkcji obliczającej PKL.

Wszystkie zaawansowane paramtery przekazywane są w zmiennej HTTP `manual`.

| Parametr | Opis              | Wartości | Wartość domyślna |
| -------- | ----------------- | -------- | ---------------- |
| manual[min_points]  | minimum PKL za pierwszej miejsce | liczba całkowita nieujemna | wynika z rangi turnieju i liczby rozdań |
| manual[tournament_weight] | waga turnieju | liczba całkowita dodatnia | wynika z rangi turnieju i liczby rozdań |
| manual[players_coefficient] | współczynnik zawodników | liczba nieujemna | 0.05 |
| manual[points_cutoffs] | parametry liniowych odcinków obniżki PKL | tablica par liczb z przedziału [0.0; 1.0] | [[0.0, 1.0], [0.02, 0.9], [0.2, 0.2], [0.5, 0.0]] |

W parametrze `manual[points_cutoffs]` poprzedniki każdej pary (odsetek najwyższych miejsc) tworzą ciąg rosnący, następniki (odsetek maksymalnej liczby PKL) tworzą ciąg nierosnący.

W przypadku podania zarówno parametru `manual[min_points]`, jak i `manual[tournament_weight]`, parametry `tournament_rank` i `over39_boards` przestają być wymagane.

Dla turniejów o randze KMP powyższe parametry, jak i parametr liczby rozdań, są ignorowane (ale API wciąż wymaga podania parametrów `over39_boards`).

Dla turniejów w randze BridgeNET Lokalny efekt podania tych parametrów jest nieokreślony, w szczególności nie ma gwarancji, że przy podaniu parametru `manual[min_points]` stanie się którakolwiek z poniższych rzeczy:
 * naliczenie za 1. miejsce podanej liczby PKL
 * naliczenie za 1. miejsce podanej liczby PKL zmodyfikowanej o czynnik wynikający z liczby rozdań, określony w Regulaminie BridgeNET Lokalny
 * naliczenie za 1. miejsce liczby PKL wynikającej z Regulaminu BridgeNET Lokalny, bez uwzględniania parametru `manual[min_points]`

Przykładowe zapytania do API
----------------------------

```
POST /sedziowie/pkl/api.php HTTP/1.1
Host: pzbs.pl
Content-Length: 350
Content-Type: application/x-www-form-urlencoded

type=2&contestants=125&title_sum=1230&tournament_rank=3&over39_boards=0&manual[players_coefficient]=0.05&manual[min_points]=0&manual[tournament_weight]=5&manual[points_cutoffs][0][0]=0.02&manual[points_cutoffs][0][1]=0.9&manual[points_cutoffs][1][0]=0.2&manual[points_cutoffs][1][1]=0.2&manual[points_cutoffs][2][0]=0.5&manual[points_cutoffs][2][1]=0
```

```
GET /sedziowie/pkl/api.php?type=2&contestants=125&title_sum=1230&tournament_rank=3&over39_boards=0&manual[players_coefficient]=0.05&manual[min_points]=0&manual[tournament_weight]=5&manual[points_cutoffs][0][0]=0.02&manual[points_cutoffs][0][1]=0.9&manual[points_cutoffs][1][0]=0.2&manual[points_cutoffs][1][1]=0.2&manual[points_cutoffs][2][0]=0.5&manual[points_cutoffs][2][1]=0 HTTP/1.1
Host: pzbs.pl

```

Oba zapytania są równoważne.

Format odpowiedzi
-----------------

API zwraca odpowiedź sformatowaną jako JSON.

Zwracany jest pojedynczy obiekt. Element `points` jest słownikiem indeksowanym kolejnymi liczbami naturalnymi i podaje liczby PKL za kolejne miejsca, a element `sum` to suma PKL w turnieju (w turnieju teamów - przy założeniu czterosobowych teamów).

Prawidłowa odpowiedź zwaracana jest z kodem HTTP 200 (OK). W przypadku błędów parametrów wejściowych, treść błędu zwracana jest łańcuchem tekstowym, a odpowiedź HTTP ma ustawiony kod 400 (Bad Request). W przypadku błędu serwera zwracany jest kod HTTP 500 (Internal Server Error).

Przykładowa odpowiedź
---------------------

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 939

{"sum":1626,"points":{"1":38,"2":37,"3":35,"4":34,"5":33,"6":32,"7":31,"8":29,"9":28,"10":27,"11":26,"12":25,"13":23,"14":22,"15":21,"16":20,"17":19,"18":18,"19":16,"20":15,"21":14,"22":13,"23":12,"24":10,"25":9,"26":8,"27":8,"28":8,"29":7,"30":7,"31":7,"32":7,"33":7,"34":6,"35":6,"36":6,"37":6,"38":6,"39":5,"40":5,"41":5,"42":5,"43":5,"44":4,"45":4,"46":4,"47":4,"48":4,"49":3,"50":3,"51":3,"52":3,"53":3,"54":2,"55":2,"56":2,"57":2,"58":2,"59":1,"60":1,"61":1,"62":1,"63":1,"64":1,"65":1,"66":1,"67":1,"68":1,"69":1,"70":1,"71":1,"72":1,"73":1,"74":1,"75":1,"76":1,"77":1,"78":1,"79":1,"80":1,"81":1,"82":1,"83":1,"84":1,"85":1,"86":1,"87":1,"88":1,"89":1,"90":1,"91":1,"92":1,"93":1,"94":1,"95":1,"96":1,"97":1,"98":1,"99":1,"100":1,"101":1,"102":1,"103":1,"104":1,"105":1,"106":1,"107":1,"108":1,"109":1,"110":1,"111":1,"112":1,"113":1,"114":1,"115":1,"116":1,"117":1,"118":1,"119":1,"120":1,"121":1,"122":1,"123":1,"124":1,"125":1}}

```
