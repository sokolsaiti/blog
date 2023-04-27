---
title: "Votimi elektronik dhe rasti i Zvicrës"
date: 2019-03-08T17:08:38+02:00
draft: false # Set 'false' to publish
---
Tema e votimit elektronik është interesante.


Para disa ditëve Posta e Zvicrës bëri publik synimin e saj për t'i organizuar votimet në mënyre elektronike. <!--more-->
Kush ka njohuri mbi sistemin e politik të Zvicrës e din se atje për shumë çështje të interesit shoqëror organizohen referendumet në të cilët populli pyetet direkt.
Në dekadën e fundit vërehet një entuziazëm i shtuar për të zëvendësuar shumë shërbime konvencionale të bazuara në letër me ato elektronike, ka shumë nisma që kjo të bartet edhe te procesi i votimit.
Disa shtete federale të SHBA organizojnë votime në formë elektronike. Kjo realizohet nëpërmjet makinave të specializuara në të cilat votuesi i identifikuar paraprakisht e kryen votimin duke zjedhur njërin prej opcioneve në një prej makinave të cilat kanë ekran prekës (touchscreen).


Ka plot kritika ndaj kësaj mënyre të votimit, makinat e votimit zakonisht prodhohen nga kontraktues të cilët nuk kanë konsideratë për standardet e sigurisë prandaj edhe manipulimi elektronik i votave është më i lehtë. Komponentet të cilat përdoren në keto makina nuk janë të kualitetit të dëshirueshëm. Për shembull një votues e postoi këtë video gjatë zgjedhjeve të fundit në SHBA:

![Votimi](https://i.imgur.com/x8Mwu0g.gif)

Pra shihet qartë se ai don ta votojë kandidatin e tij të preferuar ndërsa makina votuese ka ide të veta. Videoja më lartë është vetëm një prej plot dobësive të kësaj mënyre të të votuarit.

Një aspekt tjetër negativ është se pajisjet në fjalë nuk kanë specifikacione transparente dhe publike, pra nuk dihet se si funksionojnë dhe kur funksionojnë çfarë protokole të sigurisë përdorin. Një anekdotë thotë se shteti i Nevadës i detyron kasinot që t'i publikojnë specifikacionet e slot makinave në Las Vegas ndërsa për ato të votimit nuk ka kurfarë detyrimi.

Në Zvicër votimet elektronike planifikohen të bëhen online, pra shtetasit mund të votojnë përmes shfletuesit (browserit) në pajiset e tyre personale. Për dallim nga mentaliteti mbretërues në SHBA, Posta Zvicerane [ka ftuar publikisht](https://www.evoting-blog.ch/en/pages/2019/public-hacker-test-on-swiss-post-s-e-voting-system) IT ekspertët që për një periudhë të caktuar të zhvillojnë sulme kundër sistemit i cili parashihet të menaxhojë procesin e votimit,ka publikuar një pjesë të kodit burimor të sistemit softverik për votim. 

## Sa është i sigurtë softveri?

Votimi në këtë mënyrë i ka sfidat e veta.

Së pari sistemi supozon se përdoruesi i fundit apo votuesi qëndron pas një pajisjeje të sigurtë, kjo praktikisht nuk është e mundshme. Kompjuterët personalë (posaçërisht ata që punojnë me MS Windows) kanë një rrezik lartë të infektimit me [viruse](https://en.wikipedia.org/wiki/Computer_virus), [malware](https://en.wikipedia.org/wiki/Malware), [trojanë](https://en.wikipedia.org/wiki/Trojan_horse_(computing)) ose [rootkit](https://en.wikipedia.org/wiki/Rootkit). Pra me fjalë tjera, barra e mirëmbajtjes së një ambienti të pastër në pajisje elektronike ju delegohet shtetasve. Infektimi eventual i këtyre pajisjeve do të mund të ndikonte në procesin e votimit, pra në një skenar hipotetik edhe pse votuesi e zgjedh një opcion, sistemi i infektuar (posaçërisht ai i infektuar me rootkit) dërgon një opcion tjetër në sistemin e votimit. Shtrohet pyetja, kush do të ishte i interesuar për manipulime të tilla? Ka plot akterë te tillë, sidomos akterë shtetërorë.

Rasti i [Stuxnet](https://en.wikipedia.org/wiki/Stuxnet) - edhe pse nuk ka të bëjë me procesin e votimit elektronik - tregon shumë qartë se akterët e ndryshëm pas të cilëve qëndrojnë institucionet shtetërore janë në gjendje të lansojnë sulme të sofistikuara kibernetike. Përmes këtyre sulmeve pastaj mund t'i anashkalojnë mbrojtjet e vendosura nga aplikacioni për votim për shembull. 

## Po hardveri?

Sulmet hipotetike ndaj kompjuterëve personalë nuk kufizohen me ato softverike, kompjuterët personalë mund të komprometohen edhe nëpërmjet modifikimit të hardverit nga akterët dashakëqinjë. Në kushte normale, pajisjet të cilat përdoren për punë të ndjeshme duhet të kalojnë nëpër një proces të certifikimit i cili kryesisht bëhet nga ndonjë autoritet shtetëror. Qëllimi i këtij procesi është që të vërtetohet fakti se pajisja në fjalë i përmbush standardet e sigurisë dhe funksionon si duhet. Në tregun e pajisjeve për konsumatorë, zakonisht nuk ka certifikime të këtij lloji dhe kompjuterët personalë janë më të lëndueshëm ndaj sulmeve hardverike.

Si mund të vendoset kali i trojës në nivel hardverik? Modifikimi i hardverit me qëllim të komprometimit të tij apo degradimit të punës normale hipotetikisht mund të realizohet gjatë fazës së prodhimit. Ky punim akademik tenton që të simulojë një sulm të tillë duke i modifikuar qarqet integrale gjatë fazës së prodhimit të tyre. Në fund të punimit konkludohet se edhe pse sulme të tilla janë shumë te vështira për t'u realizuar prap se prap janë të mundshme, poashtu modifikimi i bëhet nën nivel të tranzistorëve dhe si i tillë është vështirë i detetektueshëm.

Modifikimet e tilla mund të ndikojnë në degradim të operacioneve kriptografike të cilat janë esenciale për sisteme të ndijshme si ai për votim elektronik.

## Zvicra

Hulumtuesit e sigurisë veçse kanë gjetur lëshime në sistemin e votimit elektronik që parashihet të përdoret në Zvicër. Sipas tyre, sistemi aktual ka futur kompleksitet të panevojshëm në kodin burimor të tij dhe duke qenë gjendja kështu e bën të mundur më të lehtë manipulimin e votave. Në votimin klasik me letra, konfidencialiteti i votuesit arrihet duke votuar prapa perdes dhe duke e futur votën në kuti të votimit dhe pastaj vota e hedhur përzihet në mënyrë natyrale. Kështu, nuk është e mundur të dihet se kush ka votuar për kë.

Në ambient elektronik kjo nuk është e mundshme, sepse i gjithë trafiku ndërmjet pajisjeve elektronike është i rregulluar në bazë të protokoleve që kërkojnë rend dhe besueshmëri (shih TCP protokolin psh. https://en.wikipedia.org/wiki/Transmission_Control_Protocol). Sistemet kompjuterike janë sisteme deterministike dhe si te tilla nuk lejojnë hapësirë për rastësi ([randomness](https://en.wikipedia.org/wiki/Randomness)), rastësia duhet të arrihet përmes metodave dhe komponenteve shtesë. Pikërisht këtu, sistemi i votimit elektronik në Zvicër fut në lojë diçka që quhet "mixer". Nga vetë emri lihet të kuptohet se funksioni i tij është të "përzijë" diçka, në këtë rast votat elektronike, në këtë mënyrë kjo komponentë mëton të simulojë të njëjtën gjë sikurse kutia fizike e votimit. Pra përzierjen e votave në mënyrë që të ruhet konfidencialiteti i votuesve.

Në [studimin](https://people.eng.unimelb.edu.au/vjteague/SwissVote) e tyre hulumtuesit e sigurisë kanë zbuluar dobësi në komponentin në fjalë, sipas tyre është e mundur të manipulohen votat dhe kjo të mos detetktohet fare. Kjo vetvetiu është brengosëse përkundër faktit se dobësitë e tilla mund të korrigjohen nga autoritetet Zvicerane.

Poashtu njëra nga anëtaret e ekipit në disa postime të saj në Twitter thekson edhe dobësitë e JavaScript librarive që ekzekutohen lokalisht në shfletues (browser) të klientit, funksioni i të cilave është të gjenerojnë entropi për operacione kriptografike.

[There is an entire javascript package dedicated to collecting entropy in that codebase.](https://twitter.com/SarahJamieLewis/status/1097584389750284289)

Me fjalë tjera, delegimi i menaxhimit të demokracisë procesit të votimit elektronik nuk është ide e mençur.