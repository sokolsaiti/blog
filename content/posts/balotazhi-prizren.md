---
title: "Numrat e Balotazhit në Prizren"
date: 2021-11-19T15:08:38+02:00
draft: false # Set 'false' to publish
---

Pas publikimit të rezultateve preliminare të Balotazhit në Prizren, thash t’i mbledhi të dhanat në nji Excel fajll edhe të shoh se cili vendbanim si ka votu.

KQZ tregohet tepër e keqe në kuptimin e lehtësisë së leximit të të dhanave që i publikon. Për shembull vendvotimet identifikohen me një kod i cili është krijuar qysh kur OSBE pati organizuar regjistrimin e popullsisë pas luftës, në vend se të jipen emrat e vendbanimeve ose të lagjeve. Kësisoji, kur i lexon rezultatet krijohet njëfarë ndjenje steriliteti.

Në mënyrë që t’i identifikoj vendbanimet me kodet e tyne m’u desht t’i performoj disa akrobacione duke përdorë vegla të ndryshme.

Së pari, të dhanat e balotazhit nuk ishin publikuar ende në formën standarde që i publikon KQZ, por këtu kisha pakës fat sepse duke e analizuar web faqen e rezultateve pashë që i gjithë rezultati po kthehet si JSON objekt nga API (i cili është zhvilluar nga një firmë maqedone) serveri i KQZ-së.

```json
{
    "57": {
        "ElectionUnitId": 615,
        "PoliticalEntityId": 10,
        "Votes": 89,
        "VotesPercent": 22.14,
        "Seats": 0
    }
}
```

Hapi i dytë ishte të korelohet `ElectionUnitId `me ID-në e definuar nga OSBE-ja për bashkësitë lokale (2001A psh). Përsëri përgjigja mund të gjendet në HTML strukturën e web faqes ku `ElectionUnitId `është definuar si `data `atribut në dropdown-in që përmban listën e vendvotimeve me ID të OSBE-së.

![](https://i.snap.as/ELncH02j.jpg)

Me pak magji, këtë JSON edhe të dhanat nga HTML struktura i shnëdrojmë nw CSV duke e përdore librarinë **[pandas](https://pandas.pydata.org/ "pandas")** në **Python**.

`PoliticalEntityId `në këtë rast tregon për cilin kandidat bëhet fjala, numri 7 është Mytaher Haskuka ndërsa numri 10 është Shaqir Totaj.

Këta dy CSV fajlla pastaj i importova në një databazë të **[PostgreSQL](https://www.postgresql.org/)** ku mëpastaj mund të manipulohen më lehtë me SQL. Sidoqoftë mua më mjaftoi vetëm një `JOIN.`

Rezultati është ky Excel fajll: [https://onedrive.live.com/view.aspx?resid=3CF3F387DCE15279!1618&ithint=file%2Cxlsx&authkey=!AN3fZBrv4Oo9oQc](https://onedrive.live.com/view.aspx?resid=3CF3F387DCE15279!1618&ithint=file%2cxlsx&authkey=!AN3fZBrv4Oo9oQc)

Në te shihet se në plot vendvotime, Mytaher Haskuka ka humbë vota në Balotazh në krahasim me Rundin e Parë. Në anen tjeter kandidati i PDK-së ka rritje drastike, dicka qe i atribuohet ndihmës nga LDK, Nisma, AAK etj.