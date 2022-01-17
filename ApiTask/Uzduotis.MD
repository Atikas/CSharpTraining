# Api uzduotis

Sukurti loginimo REST API kuris apima:
* 1. Log'o išvedimą į konsolę
* 2. Log'o išsiuntimą el.paštu (veikiančio paties el.laiško siuntimo implementuoti nereikia, užtenka principo)
* 3. Log'o įrašymą į failą
* 4. Log'o įrašymą į sql db (DB funkcionalumui naudoti EFcore ir localDB. Naudoti repository patterną). 
** Nepamirškite parinkti tinkamų duomenų tipų, kintamųjų ilgių ir entity validacijų. Komentaruose pagrįskite pasirinkimą.
** Lentelės spulpelių pavadinimams naudoti snake_case. Data entičiams naudoti PascalCase.
* 5. API konfigūracijoje (pvz. appsettings.json) nustatomas koks log įrašymo mechanizmas (1,2,3 ar 4) bus naudojamas (tik vienas iš jų) (Naudoti Options patterną).
** Turi būti realizuota api metodai:
**    - žinutės įrašymo,
**    - žinučių sąrašo skaitymo (jeigu pagal nustatymus žinutė įrašyta (failas ar db)),
**    - vienos žinutės skaitymo (jeigu pagal nustatymus žinutė įrašyta (failas ar db)).  
* 6. API grąžinamas rezultatas turi būti tik application/json arba application/xml


* Darbas vykdomas per GitHub taip, kad matytųsi asmens įdirbis (jei reikia dirbama skirtingose 'feature' šakose, o rezultatas merdžinamas į 'main')
* Turi būti realizuotas tik vienas endpoint'as "api/logs"
* Naudoti OOP architektūros principus (būtinas paveldėjimas ir polimorfizmas)
* Naudoti SOLID architektūros principus
* Naudoti DRY programavimo principus
* Naudoti TDD principus
* Naudoti OpenApi specifikacifikavimo mechanizmą (swashbuckle swagger). Api endpointas turi būti tinkamai dokumentuojamas. Naudoti Swagger UI.
* Būtina pasiekti minimalų REST API lygį 2 (LEVEL 2: Utilize Potential of HTTP as Application Layer Protocol.)
* Api modelis turi turėti validacijas (per atributą arba per servisą, kaip patogiau)
* Būtina naudoti dependency injection
* Rekomentuojama naudoti DTO patterną. Prisiminkite, kad DTO ir biznio modeliai gali ir nesutapti.

Objektas esantis propertyje "Properties" yra dinaminis (pateikta struktūra tik pavyzdinė ir ji kinta priklausomai nuo pranešimo)
LOG'o pranešimo (request) json DTO pavyzdys:
```
{
  "events": [
    {
      "Timestamp": "2016-11-03T00:09:11.4899425+01:00",
      "Level": "Information",
      "MessageTemplate": "Logging {@Heartbeat} from {Computer}",
      "RenderedMessage": "Logging { UserName: \"Mike\", UserDomainName: \"Home\" } from \"Workstation\"",
      "Properties": {
        "Heartbeat": {
          "UserName": "Mike",
          "UserDomainName": "Home"
        },
        "Computer": "Workstation",
        "Parameters": [],
        "Retries": 3
      }
    },
    {
      "Timestamp": "2016-11-03T00:09:12.4905685+01:00",
      "Level": "Information",
      "MessageTemplate": "Logging {@Heartbeat} from {Computer}",
      "RenderedMessage": "Logging { UserName: \"Mike\", UserDomainName: \"Home\" } from \"Workstation\"",
      "Properties": {
        "Heartbeat": {
          "UserName": "Mike",
          "UserDomainName": "Home"
        },
        "Computer": "Workstation",
        "Parameters": []
      }
    }
  ]
}
