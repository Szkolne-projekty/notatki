# BazyS

## Osoba 1

```sql
-- Wyświetl wszystkie dane na temat klienta (lub klientów) o nazwisku Kowalski.
SELECT * FROM klienci WHERE klienci.NAZWISKO = "Kowalski";

-- Wyświetl nazwiska i imiona wszystkich klientów oraz marki i modele samochodów, jakie wypożyczali. Posortuj dane alfabetycznie według nazwisk klientów.
SELECT klienci.NAZWISKO, klienci.IMIE, samochody.MARKA, samochody.MODEL FROM klienci NATURAL JOIN wypozyczenia NATURAL JOIN samochody ORDER BY klienci.NAZWISKO;

-- Wyświetl wszystkie dane na temat samochodu o największej pojemności silnika z pośród samochodów wyprodukowanych w Japonii.
SELECT * FROM samochody WHERE samochody.KRAJ_PROD = "Japonia" ORDER BY samochody.POJ_SIL DESC LIMIT 1;

-- Wyzwalacz, który automatycznie doda datę wypożyczenia przy wstawianiu nowego wypożyczenia w tabeli wypożyczenia.
CREATE TRIGGER dodaj_date_wypozyczenia
BEFORE INSERT ON wypozyczenia
FOR EACH ROW
SET NEW.DATA_WYP = CURRENT_DATE;

-- Wyświetl marki samochodów oraz modele. Modele mają być wypisane małymi literami, kolumna ma mieć nie zmienioną nazwę.
SELECT samochody.MARKA, LOWER(samochody.MODEL) AS MODEL FROM samochody;

-- Wyświetl kraj produkcji, ilość samochodów danego kraju (ilosc) oraz najmniejszy koszt dnia (koszt_dnia) dla samochodów z danego kraju.
SELECT samochody.KRAJ_PROD, COUNT(*) AS ILOSC, MIN(samochody.KOSZT_DNIA) as NAJMNIEJSZY_KOSZT_DNIA FROM samochody GROUP BY samochody.KRAJ_PROD;
```

## Osoba 2

```sql
1. SELECT NR_REJ FROM SAMOCHODY WHERE MARKA = 'OPEL';

2. SELECT KLIENCI.NR_DOWODU, SAMOCHODY.NR_REJ, WYPOZYCZENIA.DATA_WYP, WYPOZYCZENIA.DATA_ZWR
FROM KLIENCI
JOIN WYPOZYCZENIA ON KLIENCI.ID_KLI = WYPOZYCZENIA.ID_KLI
JOIN SAMOCHODY ON WYPOZYCZENIA.ID_SAM = SAMOCHODY.ID_SAM
WHERE SAMOCHODY.NR_REJ LIKE 'KR%'
ORDER BY WYPOZYCZENIA.DATA_WYP DESC;


3. SELECT KLIENCI.*, WYPOZYCZENIA.DATA_WYP, WYPOZYCZENIA.DATA_ZWR
FROM KLIENCI
JOIN WYPOZYCZENIA ON KLIENCI.ID_KLI = WYPOZYCZENIA.ID_KLI
WHERE WYPOZYCZENIA.DATA_ZWR - WYPOZYCZENIA.DATA_WYP = (
    SELECT MAX(DATA_ZWR - DATA_WYP)
    FROM WYPOZYCZENIA);

4. CREATE TRIGGER TRIGGER_DODAJ_DATE_ZWROTU
BEFORE UPDATE ON WYPOZYCZENIA
FOR EACH ROW
SET NEW.DATA_ZWR = CURRENT_DATE;

5. SELECT ID_KLI, INITCAP(IMIE) AS IMIE, INITCAP(NAZWISKO) AS NAZWISKO, NR_DOWODU, MIEJSCOWOSC, ULICA
FROM KLIENCI;

6. SELECT SUM(KOSZT) AS SUMA_KOSZTOW
FROM WYPOZYCZENIA
WHERE SYSDATE BETWEEN DATA_WYP AND DATA_ZWR;
```

## Osoba 3

```sql
1.WyĹwietl nazwy marek i modeli samochodĂłw oraz miesiÄczny koszt ich wypoĹźyczenia (tej kolumnie nadaÄ nazwÄ koszt_miesiaca).

SELECT marka, model, koszt_dnia*31 AS koszt_miesiaca FROM samochody JOIN wypozyczenia;

2.WyĹwietl numery dowodĂłw osobistych, numery rejestracyjne samochodĂłw oraz daty wypoĹźyczeĹ dla wszystkich klientĂłw, ktĂłrzy wypoĹźyczali samochody zarejestrowane w wojewĂłdztwie Krakowskim (numery rejestracyjne zaczynajÄce siÄ od KR). Posortuj dane wedĹug data wypoĹźyczenia w kolejnoĹci odwrotnej.

SELECT nr_dowodu, nr_rej, data_wyp FROM wypozyczenia NATURAL JOIN klienci NATURAL JOIN samochody WHERE nr_rej LIKE "KR%" ORDER BY data_wyp DESC;

3.WyĹwietl wszystkie informacje o samochodach, ktĂłre zostaĹy wypoĹźyczone przez tego samego klienta, ktĂłry wypoĹźyczyĹ Opla Calibre.

SELECT * FROM samochody NATURAL JOIN wypozyczenia WHERE id_kli IN (SELECT id_kli FROM wypozyczenia
WHERE id_sam IN (SELECT id_sam FROM samochody WHERE marka = 'opel' AND model = 'calibra'));

4.Wyzwalacz ktĂłre automatycznie doda osobÄ ktora edytuje i datÄ edycji do tabeli obsluga przy edycji uĹźytkownika (tabele stworzyÄ: id_obsluga, kto, kiedy).

CREATE TABLE obsluga ( id_obsluga INT AUTO_INCREMENT PRIMARY KEY, kto VARCHAR(255), kiedy TIMESTAMP DEFAULT CURRENT_TIMESTAMP);

CREATE TRIGGER edycja_uzytkownika_trigger AFTER UPDATE ON obsluga FOR EACH ROW BEGIN INSERT INTO obsluga (kto, kiedy) VALUES (USER(), NOW()); END;;

5.WyĹwietl marki i modele samochodĂłw oraz koszt godzinowy wypoĹźyczenia samochodu (nadaj kolumnie nagĹĂłwek: koszt_godziny).

SELECT marka, model, ROUND(KOSZT_DNIA/24, 2) AS koszt_godziny FROM samochody JOIN wypozyczenia;

6.WyĹwietl daty najbliĹźszych poniedziaĹkĂłw, przypadajÄcych po dacie wypoĹźyczenia dla kaĹźdego samochodu.

SELECT ID_SAM, DATA_WYP, MIN(DATE_ADD(DATA_WYP, INTERVAL (7 - WEEKDAY(DATA_WYP)) DAY)) AS NajblizszyPoniedzialek FROM WYPOZYCZENIA GROUP BY ID_SAM, DATA_WYP
```

## Osoba 4

```sql
1. Wyświetl nazwiska, imiona i identyfikatory klientów sortując nazwiska w kolejności alfabetycznej.

SELECT klienci.nazwisko, klienci.imie, klienci.id_kli FROM klienci GROUP BY nazwisko;

2. Wyświetl nazwiska, imiona klientów i miejscowości oraz modele samochodów, dla samochodów wyprodukowanych w Niemczech i dla klientów zamieszkałych poza Warszawą.

SELECT klienci.nazwisko, klienci.imie, klienci.miejscowosc, samochody.model FROM klienci, samochody WHERE samochody.kraj_prod = "Niemcy" AND klienci.miejscowosc !="Warszawa";

3. Wyświetl marki i modele samochodów wyprodukowanych w tym samym kraju, w którym wyprodukowano najnowszy samochód w wypożyczalni.

SELECT samochody.marka, samochody.model FROM samochody WHERE samochody.kraj_prod = "Japonia";

4. Wyzwalacz które automatycznie doda nowym samochodom koszy wypożyczenia 100.

CREATE TRIGGER wyzwalacz AFTER INSERT ON samochody FOR EACH ROW BEGIN DECLARE i INT DEFAULT 0;
DECLARE id_sam INTEGER;
SET id_sam = NEW.ID_SAM;
WHILE i < 100 DO INSERT INTO wypozyczenia (ID_SAM, ID_KLI, DATA_WYP, DATA_ZWR, KOSZT) VALUES (id_sam, NULL, NULL, NULL, NULL);
SET i = i + 1;
END WHILE;
END;

5. Wyświetl liczby miesięcy, jakie upłynęły pomiędzy data wypożyczenia a datą obecną. Kolumnie nadaj nazwę LICZBA_MIESIECY.

SELECT wypozyczenia.id_sam, datediff(CURDATE(), DATA_WYP) / 30 AS LICZBA_MIESIECY FROM wypozyczenia;

6. Wyświetl daty ostatnich dni miesiąca, przypadających po dacie zwrotu dla każdego samochodu.

SELECT wypozyczenia.id_sam, wypozyczenia.data_zwr, LAST_DAY(DATE_ADD(DATA_ZWR, INTERVAL 1 day)) AS DATA_OST_DNIA_MIES FROM wypozyczenia;
```

## Osoba 5

```sql
1. Wyświetl marki, modele, pojemność silnika oraz koszt dnia wszystkich samochodów, których pojemność jest równa co najmniej 1,4 l. a koszt dnia mniejszy od 80 zł

SELECT marka, model, poj_sil, koszt_dnia
FROM samochody
WHERE poj_sil >= 1.4 AND koszt_dnia< 80;

2. Wyświetl koszty wypożyczenia oraz nazwiska klientów.

SELECT klienci.nazwisko, wypozyczenia.koszt
FROM klienci
JOIN wypozyczenia ON klienci.id_kli= wypozyczenia.id_kli;

3. Wyświetl nazwy tych producentów (ich marki), którzy produkują samochody których średnia pojemność silnika jest większa niż średnia pojemność silnika dla wszystkich samochodów w bazie.

SELECT marka
FROM samochody
GROUP BY marka
HAVING AVG(poj_sil) > (SELECT AVG(poj_sil) FROM samochody);

4. Wyzwalacz które automatycznie podliczy koszt wypożyczenia samochodu po oddaniu i
wpisze w koszt.

DELIMITER //
CREATE TRIGGER update_cost_trigger BEFORE UPDATE ON wypozyczanie
FOR EACH ROW
BEGIN
  SET NEW.KOSZT = DATEDIFF(NEW.DATA_ZWR, NEW.DATA_WYP) * NEW.KOSZT_DNIA;
END;
//
DELIMITER ;

5. Wyświetl ilość samochodów wyprodukowanych w Niemczech.

SELECT COUNT(*) AS ilosc
FROM samochody
WHERE kraj_prod= 'Niemcy';

6. Wyświetl z tabeli WYPOZYCZENIA sumę kosztów wypożyczenia dla wszystkich samochodów, które są aktualnie wypożyczone (wykorzystaj funkcji sysdate).

SELECT SUM(koszt) AS suma_kosztow
FROM wypozyczenia
WHERE data_zwr> now();
```

## Osoba 6

```sql
Zadanie 1  -  Wyświetl wszystkie informacje z tabeli WYPOŻYCZENIA w kolejności od najbardziej do najmniej kosztownego.

SELECT * FROM WYPOZYCZENIA ORDER BY KOSZT DESC;


Zadanie 2  -  Wyświetla nazwy miejscowości, z których pochodzą klienci oraz sumy kosztów wypożyczeń przez klientów z danej miejscowości. Posortuj otrzymane dane w kolejności od najmniejszego do największego kosztu.

SELECT KLIENCI.MIEJSCOWOSC, SUM(WYPOZYCZENIA.KOSZT) FROM KLIENCI NATURAL JOIN WYPOZYCZENIA GROUP BY KLIENCI.MIEJSCOWOSC ORDER BY SUM(WYPOZYCZENIA.KOSZT);


Zadanie 3  -  Wyświetl nazwiska i imiona klientów, marki, modele samochodów i kraje produkcji, dla tych osób które wypożyczyły samochody, których koszt wypożyczenia, w ramach poszczególnych krajów produkcji, jest największy.

SELECT KLIENCI.NAZWISKO, KLIENCI.IMIE, SAMOCHODY.MARKA, SAMOCHODY.MODEL, SAMOCHODY.KRAJ_PROD, MAX(WYPOZYCZENIA.KOSZT) FROM SAMOCHODY NATURAL JOIN KLIENCI NATURAL JOIN WYPOZYCZENIA GROUP BY SAMOCHODY.KRAJ_PROD;


Zadanie 4  -  Wyzwalacz który automatycznie doda datę produkcji 2000 przy wstawianiu nowego samochodu.

CREATE TRIGGER dodajrok BEFORE INSERT ON SAMOCHODY FOR EACH ROW SET NEW.ROK_PROD = 2000;


Zadanie 5  -  Wyświetl różnicę pomiędzy najmniejszym a największym kosztem dnia.

SELECT MAX(SAMOCHODY.KOSZT_DNIA) - MIN(SAMOCHODY.KOSZT_DNIA) AS ROZNICA FROM SAMOCHODY;


Zadanie 6  -  Wyświetl całkowity koszt wypożyczenia dla poszczególnych wypożyczeń, uwzględniając podatek VAT oraz rabat wyokości 5% od ceny z Vatem.

SELECT WYPOZYCZENIA.ID_WYP, (WYPOZYCZENIA.KOSZT + 0.23 * WYPOZYCZENIA.KOSZT) - 0.05 * (WYPOZYCZENIA.KOSZT + 0.23 * WYPOZYCZENIA.KOSZT) AS OSTATECZNY_KOSZT FROM WYPOZYCZENIA;
```

## Osoba 7

Brak zadania 4 i 6

```sql
1. SELECT * FROM samochody WHERE KRAJ_PROD = 'Niemcy' AND ROK_PROD >= 1995;

2. SELECT KLIENCI.NAZWISKO, SAMOCHODY.MARKA, SAMOCHODY.MODEL FROM KLIENCI NATURAL JOIN WYPOZYCZENIA NATURAL JOIN SAMOCHODY WHERE WYPOZYCZENIA.DATA_ZWR != CURRENT_DATE;

3. SELECT * FROM KLIENCI NATURAL JOIN WYPOZYCZENIA WHERE WYPOZYCZENIA.DATA_WYP > 2006-01-02 AND WYPOZYCZENIA.DATA_WYP < 2006-12-30;

4. nie mam

5. Wyświetl markę oraz średnią pojemność silnika dla danej marki z tabeli SAMOCHODY
   SELECT MARKA, AVG(POJ_SIL) FROM SAMOCHODY GROUP BY MARKA;

6. nie mam
```

## Osoba 8

Brak zadania 4

```sql
1. Wyświetl marki, modele, pojemność silnika oraz koszt dnia wszystkich samochodów, których pojemność jest równa co najmniej 1,4 I. a koszt dnia mniejszy od 80 zł.

SELECT marka, model, poj_sil, koszt_dnia FROM samochody WHERE poj_sil>1.4 AND koszt_dnia<80;

2. Wyświetl koszty wypożyczenia oraz nazwiska klientów.

SELECT WYPOŻYCZENIA. KOSZT, KLIENCI.NAZWISKO FROM WYPOŻYCZENIA JOIN KLIENCI ON WYPOŻYCZENIA.ID KLI = KLIENCI.ID_KLI;

3. Wyświetl nazwy tych producentów (ich marki), którzy produkują samochody których średnia pojemność silnika jest większa niż średnia pojemność silnika dla wszystkich samochodów w bazie.

SELECT MARKA FROM SAMOCHODY GROUP BY MARKA HAVING AVG (POJ_SIL)> (SELECT AVG(POJ_SIL) FROM SAMOCHODY);

5. Wyświetl ilość samochodów wyprodukowanych w Niemczech.

SELECT COUNT(*) AS niem_samochody FROM SAMOCHODY WHERE KRAJ PROD = 'NIEMCY';

6. Wyświetl z tabeli WYPOŻYCZENIA sumę kosztów wypożyczenia dla wszystkich samochodów, które są aktualnie wypożyczone (wykorzystaj funkcji sysdate).

SELECT SUM(KOSZT) AS suma FROM WYPOZYCZENIA WHERE DATA ZWR IS NULL AND DATA_WYP <= sysdate();
```
