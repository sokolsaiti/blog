---
title: "Si të listohen fajllat në një direktorium direkt nga Oracle Databaza?"
date: 2019-12-14T21:08:38+02:00
draft: false # Set 'false' to publish
---

Siq e thash në postimin e kaluar në skenaret të cilët involvojnë futjen e të dhanave nëpërmjet një numri të madh të tekst fajllave strategjia e futjes së tyre nëpërmjet External Tables të Oracle është më e lehta.
Mirëpo, kur shkruajmë PL/SQL kod për t'i përpunuar ato fajlla na duhet të dijmë se cilët janë ata fajlla që duhet të futen në databazë. Fatkeqësisht PL/SQL paketa `UTL_FILE` e cila vjen e parainstaluar në Oracle Databazë nuk e ofron këtë mundësi. <!--more-->
Pra shikuar nga perspektiva e databazës ne nuk dijmë se çka përmban një direktorium i caktuar sepse nuk ekziston funksioni `LIST_FILES`.

![](https://i.snap.as/PfNHNzP.png)


Për t'a evituar këtë problem na duhet njëfare **reference** e cila do të ishte e qasshme nga databaza dhe e cila do të përmbante informatat e nevojshme për listën e fajllave në direktoriumin prej të cilit po mendojmë që t'i fusim në databazë.
Kjo **referencë** më së miri do të ishte një tabelë me emrat e fajllave. Realisht edhe kjo tabelë duhet të jetë një *External Table* e cila do të bazohej në një tekst fajll që përmban emrat e fajllave. Natyrisht se ky tekst fajll do të duhej të popullohej me të dhana disi. 
Për këtë punë në ndihmë na vjen Sistemi Operativ, për shembull nëse Oracle Databaza është e instaluar në ndonjë *NIX sistem atëherë një shell skripte e vogël mund të përdoret për ta arritur këtë qëllim. Skripta në fjalë mund të duket kështu, pra për cdo fajll i cili mbaron me `.CSV` printoje:

```bash 
for file in /path/to/files/to/import/*.csv
do
  echo "$file"
done
```

Kjo skriptë e thjeshtë mund të ruhet në një fajll `list_files.sh` dhe pastaj mund të bëhet schedule me `cron` që të ekzekutohet çdo minutë psh: 
```bash
1 * * * * /path/to/file_list.sh > /path/to/external/table/fl_source.txt
```
Në këtë mënyrë kjo skriptë ekzekutohet çdo minutë dhe përmes shprehjes `>` shkruan gjithçka që printon në fajllin (të cilin poashtu e rikrijon) `fl_source.txt`. 

Nëse Oracle Databaza është e instaluar në Windows sistem atëhere PowerShell skripta do të dukej kështu 

```powershell
Get-ChildItem -Path F:\path\to\files\to\import\*.csv -Name
``` 
e cila pastaj bëhet schedule me Task Scheduler të Windows. Duhet me pasë parasysh se këto skripta janë shume të thjeshta dhe nuk e marrin parasysh situaën kur kemi *overlapping* në ekzekutim (sidomos në Linux), për t'a evituar këtë problem duhet me u shkru ni mekanizëm sinkronizimi me `lock` fajlla psh.

Duke pasur `fl_source.txt` tani mund të krijohet External Tabela: 

```sql
CREATE TABLE FILE_LIST 
(
  FILE_NAME VARCHAR2(50) 
) 
ORGANIZATION EXTERNAL 
( 
  TYPE ORACLE_LOADER 
  DEFAULT DIRECTORY DATA_PUMP_DIR 
  LOCATION 
  ( 
    'file_list_source.txt' 
  ) 
);
``` 

Kjo tabelë azhurnohet çdo minut duke i falënderuar `cron`-it ose Task Schedulerit, tash nëse dojmë me ditë se çka përmban direktoriumi prej të cilit dojmë me i importu fajllat në databazë mjafton vetëm një 

```sql
SELECT file_name from FILE_LIST;
``` 
(natyrisht me 1 minutë vonesë).

Kjo mënyrë mund të duket primitive në fillim, mirëpo është mjaft efektive kur të dhanat importohen nga fajllat e thjeshtë.