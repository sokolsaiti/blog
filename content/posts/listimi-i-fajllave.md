---
title: "A mund të listohen fajllat në një direktorium direkt nga Oracle Databaza? "
date: 2019-12-13T21:08:38+02:00
draft: false # Set 'false' to publish
---

Një kompani tipike mesatare e cila si biznes kryesor e ka atë të IT-së përmban në vete sisteme të ndryshme softverike. Zakonisht nëse kompania në fjalë ka një strukturë më korporative, kjo reflektohet edhe në zgjidhjet softerike të cilat ajo i përdorë. <!--more-->

Psh nëse kemi të bëjmë me një bankë athëherë tendenca për të blerë softver shkon kah firmat e mëdhaja si Microsoft, IBM, Oracle apo Red Hat ndërsa nëse kemi të bëjmë me startup psh atëherë softveri i përdorur ka më shumë tendencë të jetë [FOSS](https://en.wikipedia.org/wiki/Free_and_open-source_software).

Shpesh ndodh që brenda kompanisë njerëzit e arsyeshëm dojnë që nga këto sisteme të ndryshme t'i integrojnë të dhanat në një mënyrë dhe nga ato t'i nxjerrin raportet e nevojshme të cilat do të ndihmonin biznesin ditor.
Natyrisht, në tregun softverik ekzistojnë zgjidhje të tilla të cilat si tipar kryesor e kanë integrimin e të dhanave që "prodhohen" nga sistemet e IT-së. 

![Image source: https://en.wikipedia.org/wiki/File:Datawarehouse.png](https://i.snap.as/jX4Y4K0.png)

Në mungesë të sistemeve të specializuara për integrim të të dhanave njeriut i mbetet të kthehet në mekanizmat bazikë apo njësinë elementare të sistemeve kompjuterike. Në tekst fajll. 

Oracle Databaza e ka një koncept të tabelave të bazuara në tekst fajlla me strukturë të definuar mirë. Këto tabela quhen [External Tables](https://docs.oracle.com/en/database/oracle/oracle-database/12.2/sutil/oracle-external-tables-concepts.html), arsyeja pse quhen kështu sepse përmbajtja e tyre bazohet në *të dhana të jashtme* të cilat gjenden në tekst fajll e jo në data fajllat e menaxhuara nga databaza. Kur themi *tekst fajlla me strukturë të definuar mirë* e kemi fjalën për [CSV](https://en.wikipedia.org/wiki/Comma-separated_values) ose [TSV](https://en.wikipedia.org/wiki/Tab-separated_values).

Në shumë skenare kur dojmë që t'i fusim të dhanat e sistemeve tjera në databazë i përdorim Tabelat e Jashtme External Tables). Procedura tipike e futjes së dhanave parasheh që të vijnë plot fajlla të cilat futen një nga një në databazë në mënyrë programatike. Në rastin e Oracle mënyra më tipike është shkruarja e [PL/SQL](https://en.wikipedia.org/wiki/PL/SQL) programeve, PL/SQL është një "shtojcë" e Oracle mbi [ANSI SQL](https://en.wikipedia.org/wiki/SQL) e cila jep mundësinë e shkruarjes së kodit procedural. 

Oracle nëpërmjet PL/SQL ofron shumë [paketa](https://docs.oracle.com/en/database/oracle/oracle-database/12.2/arpls/index.html) të cilat ua lehtësojnë punën programerëve duke i abstrahuar shumë gjëra që kanë të bëjnë me qasjen në resurset e sistemit kompjuterik. 

Njëra prej këtyre paketave është edhe `UTL_FILE`, kjo paketë në veti përmban disa procedura dhe funkcione të cilat janë të nevojshme për t'i manipuluar fajllat. Zakonisht këto procedura/funkcione i imitojnë komandat bazike (system calls) të sistemeve operative si psh: `open`, `read`, `write`, `seek`, `close` etj.

Një funksion i cili i mungon paketës UTL_FILE është ai i listimit të fajllave në një direktorium të dhënë. Që ky kufizim të anashkalohet na nevoitet ndihma e Sistemit Operativ (në pjesën e dytë). 