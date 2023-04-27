---
title: "Analiza e “kodit burimor” të vaksinës së BioNtech/Pfizer"
date: 2020-12-27T21:08:38+02:00
draft: false # Set 'false' to publish
---

**Vërejtje:** *Verzioni origjinal i këtij shkrimi është botuar në gjuhën angleze nga Bert Hubert dhe mund të lexohet [këtu](https://berthub.eu/articles/posts/reverse-engineering-source-code-of-the-biontech-pfizer-vaccine/).* *Ky artikull është vetëm një përkthim.*

Mirësevini! Në këtë post do të shikojmë dhe analizojmë kodin burimor të vaksinës SARS-CoV-2 mRNA të prodhuar nga BioNtech/Pfizer. Këto fjalë mund të na duken të çuditshme në fillim, si mund të flasim për kod burimor të një lëngu i cili na injektohet në krah? <!--more-->

Pyetje me vend, le të fillojmë pra me një pjesë të vogël të po këtij kodi burimor të vaksinës së BioNtech/Pfizer e cila njihet edhe si  [BNT162b2](https://en.wikipedia.org/wiki/Tozinameran), edhe si Tozinameran, [por edhe si Comirnaty](https://twitter.com/PowerDNS_Bert/status/1342109138965422083).



![500 karakteret e para të mRNA në vaksinën BNT162b2 . Burimi: Organizata Botërore e Shëndetësisë](https://i.snap.as/jxoPO3od.png)
*500 karakteret e para të mRNA në vaksinën BNT162b2 . Burimi:* [*Organizata Botërore e Shëndetësisë*](https://mednet-communities.net/inn/db/media/docs/11889.doc)


"Shpirti" i vaksinës BNT162b mRNA e përmban kodin digjital në foton e sipërme. Është i gjatë 4284 karaktere, pra teorikisht ky kod do të mund të botohej në Twitter me disa cicërime konsekutive. Krejt në fillim të procesit të prodhimit të vaksinës, dikush e ka ngarkuar këtë kod në një printer të ADN (po tybe), i cili pastaj i transformon bajtat e diskut në molekula reale të ADN-së.

![Një Codex DNA BioXp 3200 printer i ADN](https://i.snap.as/5ybb87oV.jpg)
*Një [Codex DNA](https://codexdna.com/products/bioxp-system/) BioXp 3200 printer i ADN-së*

Nga një maqinë e tillë e vogël dalin sasi të vogla të ADN-së, të cilat pas një procesi të gjatë biologjik e kimik përfundojnë si ARN (për të cilin do të flasim më poshtë) në shiringën e vaksinës. Një dozë prej 30 mikrogramësh përmban saktësisht 30 mikrogramë ARN. Përveç kësaj, ARN  mbështillet me një shtresë të lipidit (yndyrës) e cila është një metodë e mençur për t'a futur ate në qelizat tona.

Kësisoji, ARN-ja në fakt është verzion i paqëndrueshëm i 'memories punuese' së ADN-së. Ndërsa ADN është sikur flash disku i biologjisë. ADN është shumë i qëndrueshëm, brenda tij ka mekanizma që mundësojnë përmirësimin e gabimeve dhe është i besueshëm. Por ashtu sikur kompjuterë që nuk e ekzekutojnë kodin direkt nga disku para se të ndodhë diçka, kodi së pari kopjohet në një medium më të shpejtë por që është më fragjil.

Për kompjuterët ky medium është RAM memoria, ndërsa për biologji ky medium është ARN. Ngjashmëria ndërmjet dy sistemeve është e habitshme.
Ndryshe nga flash disku, RAM memoria degradon shumë shpejt, përveç nëse tregohet një kujdes i veçantë duke i rifreskuar komponentet elektronike me rrymë. Arsyeja pse vaksina Pfizer / BioNtech mRNA duhet të ruhet në frigoriferë në temperatura shumë të ulëta është e njëjtë: ARN është një lule e brishtë.

Secili karakter i ARN-së peshon në rendin prej 0.53 · 10⁻²¹ gram, që do të thotë se ka 6 · 10¹⁶ karaktere në një dozë të vetme të vaksinës prej 30 mikrogramësh. Nëse kjo shprehet në bajtë kompjuterikë, kjo nënkupton rreth 25 petabajtë, megjithëse duhet të ceket se kjo përbëhet nga rreth 2000 miliardë përsëritje të të njëjtave 4284 karaktere. Përmbajtja reale informative e vaksinës është pak më shumë se një kilobajt. Vetë [SARS-CoV-2](https://www.ncbi.nlm.nih.gov/projects/sviewer/?id=NC_045512&tracks=[key:sequence_track,name:Sequence,display_name:Sequence,id:STD649220238,annots:Sequence,ShowLabel:false,ColorGaps:false,shoën:true,order:1][key:gene_model_track,name:Genes,display_name:Genes,id:STD3194982005,annots:Unnamed,Options:ShowAllButGenes,CDSProductFeats:true,NtRuler:true,AaRuler:true,HighlightMode:2,ShowLabel:true,shown:true,order:9]&v=1:29903&c=null&select=null&slim=0) përmban rreth 7.5 kilobajtë.

### Një histori e shkurtër

ADN është një kod digjiital. Për dallim nga kompjuterët, të cilët përdorin 0 dhe 1, sistemet biologjike përdorin A, C, G dhe U / T të cilat quhen nukleotide. Në kompjuterë ne i ruajmë 0 dhe 1 vlera të cilat mund të paraqiten si ngarkesa elektrike, ose si një rrymë, si një tranzicion magnetik, ose si një tension, ose si një modulim i një sinjali, ose si një ndryshim i refleksivitetit. Pra, 0 dhe 1 nuk janë diçka abstrakte, ato shfaqen si prezencë (ose mungesë) e elektroneve dhe në shumë mishërime të tjera fizike.

Në natyrë, A, C, G dhe U / T janë molekula, të ruajtura si zinxhirë në ADN (ose ARN). 

Në sistemet kompjuterike, një bajt përbëhet nga 8 bitë dhe bajti është njësia bazike e të dhënave që përpunohen nga ana e sistemeve kompjuterike.

Në natyrë, 3 nukleotide formojne një kodon dhe kodoni është njësi bazike përpunimit. Një kodon përmban 6 bitë të informacionit (2*3). 

Deri tash, gjithçka po duket bukur digjitale. Nëse dyshoni, atëherë [drejtojuni dokumentit të OBSH-së](https://mednet-communities.net/inn/db/media/docs/11889.doc) për ta parë vetë kodin digjiital.


### Pra çka BËN ky kod?


Ideja e vaksinës është të mësojmë sistemin tonë imunitar se si të luftojmë një patogjen, duke mos shkaktuar sëmundje në të vërtetë. Historikisht ky qëllim është arritur injektuar një virus të dobësuar ose të paaftë (të zbutur), plus një ‘ndihmës’ për të trembur sistemin tonë imunitar në mënyrë që të fillojë të veprojë. Kjo ishte një teknikë mjaftë 'analoge' e cila përdorte me miliarda vezë (ose insekte). Poashtu kërkonte shumë fat dhe shumë kohë në mënyrë që të ishte e suksesshme. Ndonjëherë përdorej edhe një virus totalisht tjetër.

Vaksina e llojit mRNA e arrin të njejtin objektiv (pra 'edukimin e sistemit tonë imunitar') por në një formë lazerike. Këtu e kam fjalën për të dy kuptimet - shumë precize por edhe shumë e fuqishme.

Kjo është mënyra se si funksionon. Injeksioni përmban material të paqëndrueshëm gjenetik që përshkruan proteinën e famshme në formë të gozhdës (Spike protein) që gjindet në SARS-CoV-2. Duke përdorur metoda të mençura, vaksina arrin t'a futë këtë material gjenetike në disa prej qelizave tona.

Këto qeliza mëpastaj  fillojnë të prodhojnë me zell të hatashëm SARS-CoV-2 proteina gozhdë (Spike protein). Kur organizmi konfrontohet me këto Spike proteina dhe shenjat tjera që tregojnë se qelizat janë 'kidnapuar' nga funksionimi normal, sistemi ynë imunitar zhvillon një përgjigje të fuqishme kundër tipareve të shumta të Spike proteinave DHE procesit të prodhimit.

Dhe kjo është ajo që na çon në vaksinën me efikasitet prej 95%.

### Kodi burimor!

[Le të fillojmë nga vetë fillimi, një vend shumë i mirë për të filluar](https://youtu.be/jp0opnxQ4rY?t=8). Dokumenti i OBSH-së e ka këtë fotografi të dobishme: 

![](https://i.snap.as/Lw24haWX.png)

Kjo është një lloj tabele e përmbajtjes. Do të fillojmë me 'kapakun', i cili në të vërtetë është i përshkruar si një kapelë e vogël. 

Ashtu sikur se nuk mund të hidhni opkodet (instruksionet të cilat i 'kupton' kompjuteri) në një fajll dhe pastaj ta ekzekutoni të njëjtin si EXE fajll ashtu edhe sistemi operativ biologjik kërkon header-ë (struktura në fajlla që japin indicie se për çfarë fajlli bëhet fjalë), linkerë (programe të cilat mundësojnë kompajlimin e kodit burimor) si dhe mënyra të caktuara të thirrjes së programeve tjera.

Kodi i vaksinës fillon me këto dy nukleotide vijuese:
```
GA
```

Kjo mund të krahasohet me çdo fajll ekzekutues (fajllat që kanë prapashtesën .EXE) në [sistemet operative DOS dhe Windows të cilët fillojnë me karakteret MZ](https://en.wikipedia.org/wiki/DOS_MZ_executable), apo edhe me UNIX skriptat që fillojnë me #!. Si në jetë ashtu edhe në sistemet operative, këto dy karaktere fillestare nuk ekzekutohen në asnjë mënyrë. Por ata duhet të jenë aty sepse përndryshe asgjë nuk ndodh, pra nuk ekzekutohen "fajllat" në qeliza dhe fajllat në sistemet kompjuterike.

'Kapaku' i mRNA-së [ka një numër funksionesh](https://en.wikipedia.org/wiki/Five-prime_cap#Function). Së pari, ai jep indikacion se kodi vijues vjen nga bërthama qelizore. Në rastin tonë sigurisht që nuk vjen nga bërthama qelizore sepse në fakt kodi ynë vjen nga një vaksinim. Por ne nuk kemi nevojë t’i themi qelizës këtë. Kapaku e bën kodin tonë të duket legjitim, i cili e mbron atë nga shkatërrimi.

Dy nukleotidet fillestare të `GA` janë gjithashtu kimikisht pak të ndryshme nga pjesa tjetër e ARN-së. Në këtë kuptim, `GA` ka disa sinjalizime jashtë brezit të përgjithshëm sinjalizues.


### "Regjioni i papërkthyer pesë-prim"


Pakës terminologji profesionale. Molekulat e ARN mund të lexohen vetëm në një drejtim. Në mënyrë konfuze, pjesa ku fillon leximi quhet 5' ose 'pesë-prim'. Leximi ndalet në 3’ ose 'tre-prim'.

Jeta përbëhet nga proteinat (ose gjëra të bëra nga proteinat). Dhe këto proteina janë të përshkruara në ARN. Kur ARN shndërrohet në proteina, ky proces quhet përkthim.

Këtu kemi regjionin 5' të papërkthyer (‘UTR’ - UnTranslated Region), kështu që kjo pjesë nuk përkthehet dhe nuk përfundon si proteinë:
```
GAAΨAAACΨAGΨAΨΨCΨΨCΨGGΨCCCCACAGACΨCAGAGAGAACCCGCCACC
```

Këtu hasim befasinë tonë të parë. Karakteret normale të ARN janë A, C, G dhe U. U njihet gjithashtu si 'T' në ADN. Por këtu gjejmë një Ψ, çka po ndodh?

Kjo është një pjesë jashtëzakonisht e zgjuar e vaksinës. Siç dihet, trupi ynë ka një antivirus sistem shumë të fortë. Për këtë arsye, qelizat tona janë jashtëzakonisht joentuziaste ndaj ARN së huaj dhe përpiqen me çdo ta shkatërrojnë atë para se të bëjë ndonjë gjë.

Ky është realisht një problem për vaksinën tonë - ajo duhet të kapërcejë sistemin tonë imunitar. Gjatë shumë viteve të eksperimentimit, u zbulua se nëse U në ARN zëvendësohet nga një molekulë pak e modifikuar, sistemi ynë imunitar humbet interesin për t'a shkatërruar atë. Nime.

Pra, në vaksinën BioNtech / Pfizer, çdo U është zëvendësuar nga 1-metil-3’-pseudouridilil, i shënuar me Ψ. Pika vërtet e zgjuar është se megjithëse ky zëvendësim Ψ qetëson sistemin tonë imunitar i cili në njëfarë mënyre mashtrohet, ai pranohet si një U normal nga pjesët përkatëse të qelizës.

Në sigurinë e sistemeve kompjuterike, ne gjithashtu e dimë këtë trik - ndonjëherë është e mundur të transmetohet një version pak i korruptuar i një mesazhi që ngatërron firewall-ët dhe zgjidhjet e sigurisë, por që në fakt pranohet nga serverat në backend - të cilat më pas mund të hackohen.

Tani jemi duke korrur përfitimet e kërkimeve shkencore të kryera në të kaluarën. [Zbuluesit](https://twitter.com/PennMedicine/status/1341766354232365059) e kësaj teknike duhej të luftonin për të financuar punën e [tyre](https://www.statnews.com/2020/11/10/the-story-of-mrna-hoë-a-once-dismissed-idea-became-a-leading-teçnology-in-the-covid-vaccine-race/) dhe më pas për tu pranuar. Të gjithë duhet të jemi shumë mirënjohës dhe jam i sigurt që [çmimet Nobel do të mbërrijnë në kohën e duhur](https://twitter.com/PowerDNS_Bert/status/1329861047168225281).


> Shumë njerëz kanë pyetur, a munden viruset të përdorin gjithashtu teknikën 
> për të mposhtur sistemin tonë imunitar? Me pak fjalë, kjo është
> jashtëzakonisht e vështirë. Jeta thjesht nuk ka makineri për të ndërtuar 
> nukleotide 1-metil-3’-pseudouridilil. Viruset mbështeten në makineritë e jetës > për të riprodhuar veten e tyre, dhe kjo formë e riprodhimit thjesht nuk është e 
> pranishme. Vaksinat e ARN-së degradohen shpejt në trupin e njeriut dhe nuk 
>  ka asnjë mundësi që ARN e modifikuar me Ψ akoma të jetë
> aty. ["Jo, me të vërtetë, vaksinat e ARN-së nuk do të ndikojnë në ADN-në tuaj"](https://www.deplatformdisease.com/blog/no-really-mrna-vaccines-are-not-going-to-affect-your-dna)
> është gjithashtu artikull i mirë.

Ok, të kthehemi në përsëri në 5' UTR (regjionin e papërkthyer). Çfarë funksioni kanë këto 51 karaktere? Si çdo gjë në natyrë, pothuajse asgjë nuk ka një funksion të qartë.

Kur qelizat tona kanë nevojë për të përkthyer ARN në proteina, kjo bëhet duke përdorur një makinë brendaqelizore që quhet ribozom. Ribozomi është si një printer 3D për proteina. Përbin një varg ARN dhe bazuar në atë lëshon një varg aminoacidesh, të cilat më pas palohen në një proteinë.

![](https://upload.wikimedia.org/wikipedia/commons/9/94/Protein_translation.gif)
*Burimi: Përdoruesi i Wikipedias Bensaccount*

Kjo është ajo që ne shohim të ndodhë në animacionin lart. Shiriti i zi në pjesën e poshtme është ARN. Shiriti që shfaqet në copën e gjelbër është proteina që formohet. Gjërat që fluturojnë brenda dhe jashtë janë aminoacide plus adaptorë për t'i bërë ato të përshtaten në ARN.

Ky ribozom duhet të ulet fizikisht në fijen e ARN-së në mënyrë që t'ia fillojë punës së përkthimit. Pasi të ulet, ai mund të fillojë të formojë proteina bazuar në ARN të mëtejshme që gllabëron. Nga kjo, ju mund të imagjinoni se nuk mund të lexojë ende pjesët ku ulet në fillim. Ky është vetëm një nga funksionet e UTR: zona e uljes së ribozomeve. UTR siguron ‘hyrjen’.

Përveç kësaj, UTR përmban edhe meta të dhëna (metadata): kur duhet të ndodhë përkthimi? Dhe sa duhet të ndodhë? Për vaksinën, ata morën sa më shumë 'përkthimi të ndodhë tani' UTR që mund të gjenin, të marrë nga gjeni alfa globin. Ky gjen dihet se prodhon shumë proteina. Në vitet e mëparshme, shkencëtarët tashmë kishin gjetur mënyra për të optimizuar edhe më tej këtë UTR (sipas dokumentit të OBSH), kështu që kjo nuk është alfa globina UTR. është më mirë.


### Peptidi sinjalizues i S glikoproteinës


Siç është theksuar, qëllimi i vaksinës është që qeliza të prodhojë sasi të bollshme të proteinës Gozhdë (Spike protein) të SARS-CoV-2. Deri tani, ne kemi hasur më së shumti meta të dhëna (metadata) dhe "konventë thirrjeje" në kodin burimor të vaksinës. Por tani ne hyjmë në territorin aktual të proteinave virale.

Megjithatë, kemi ende një shtresë të meta të dhënash. Pasi ribozomi (nga animacioni i shkëlqyeshëm më lart) ka prodhuar një proteinë, ajo proteinë duhet të shkojë diku. Kjo është e koduar në "peptidin sinjalizues i S glikoproteinës (extended leader sequence)".

Mënyra për ta parë këtë është se në fillim të proteinave ekziston një lloj etikete adrese - e koduar si pjesë e vetë proteinës. Në këtë rast specifik, peptidi sinjalizues thotë se kjo proteinë duhet të dalë nga qeliza përmes "retikulumit endoplazmatik". As terminologjia e Star Trek nuk është aq "fancy" sa kjo!

"Peptidi sinjalizues" nuk është shumë i gjatë, por kur shikojmë kodin, ka ndryshime midis ARN virale dhe asaj të vaksinës:

(Vini re që për qëllime krahasimi, unë kam zëvendësuar modelin e modës Ψ me një ARN të rregullt)

```
           3   3   3   3   3   3   3   3   3   3   3   3   3   3   3   3
Virus:   AUG UUU GUU UUU CUU GUU UUA UUG CCA CUA GUC UCU AGU CAG UGU GUU
Vaccine: AUG UUC GUG UUC CUG GUG CUG CUG CCU CUG GUG UCC AGC CAG UGU GUU
               !   !   !   !   ! ! ! !     !   !   !   !   !            

```

Atëherë çka po ndodh? Unë nuk e kam renditur ARN-në rastësisht në grupe me 3 shkronja. Tre karaktere të ARN-së përbëjnë një kodon. Dhe çdo kodon përfaqëson një aminoacid specifik. Peptidi sinjalizues në vaksinë përbëhet nga saktësisht të njëjtat aminoacide si në vetë virusin.

Atëherë, si ndodhi që ARN-ja është ndryshe?

Ekzistojnë 4³ = 64 kodone të ndryshëm, pasi që ARN ka 4 karaktere,  tre prej tyre në përbëjnë një kodon. Megjithatë ka vetëm 20 aminoacide të ndryshme. Kjo do të thotë që kodone të shumtë mund të përkthehen në të njëjtin aminoacid.

Jeta përdor tabelën e mëposhtme gati universale për mapimin e kodoneve të ARN-së në aminoacide:

![](https://i.snap.as/fj1oNJEo.png)
*[Tabela e kodoneve të ARN-së](https://en.wikipedia.org/wiki/DNA_and_RNA_codon_tables) (Wikipedia)*

Në këtë tabelë, ne mund të shohim se modifikimet në vaksinë (UUU -> UUC) janë të gjitha sinonime. Kodi i ARN-së së vaksinës është i ndryshëm, por të njëjtat aminoacide prodhohen dhe e njëjta proteinë del në fund.

Nëse shohim nga afër, shohim se shumica e ndryshimeve ndodhin në pozicionin e tretë të kodonit, të shënuar me një '3' më lart. Dhe nëse kontrollojmë tabelën universale të kodoneve, shohim se ky pozicion i tretë për të cilin prodhohet aminoacidi në realitet shpesh nuk ka fort rëndësi.

Pra, ndryshimet janë sinonime, por atëherë përse ekzistojnë? Nëse shikojmë nga afër, ne shohim se të gjitha ndryshimet përveç një çojnë në më shumë C dhe G.

Atëherë pse ndodh kjo? Siç u përmend më lart, sistemi ynë imunitar ka një pamje shumë të zbehtë të ARN-së ‘ekzogjene’, kodit të ARN-së që vjen nga jashtë qelizës. Për t'iu shmangur zbulimit, 'U' në ARN të vaksinës ishte zëvendësuar tashmë nga një Ψ.

Sidoqoftë, rezulton se edhe ARN me një sasi [më të lartë](https://www.nature.com/articles/nrd.2017.243) të G dhe C gjithashtu [shndërrohet në mënyrë më efikase në proteinat përkatëse](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1463026/).

Dhe kjo është arritur në ARN të vaksinës duke zëvendësuar shumë karaktere me G dhe C kudo që kjo ishte e mundur.

> Pakës jam fascinuar nga një ndryshim që nuk çoi në një shtesë C ose G, 
> modifikimin e CCA -> CCU. Nëse dikush e di arsyen, ju lutem më tregoni! Keni 
> parasysh se unë jam i vetëdijshëm që disa kodonë janë më të zakonshëm se të > tjerët në gjenomin njerëzor, por gjithashtu [kam lexuar se kjo nuk ndikon
 shumë në shpejtësinë e përkthimit](https://journals.plos.org/plosgenetics/article?id=10.1371/journal.pgen.1006024).


### Proteina gozhdë (Spike protein)


3777 karakteret e ardhshëm të ARN-së së vaksinës janë përmbajnë ngjashëm kodonë të optimizuar, pra për të shtuar shumë C dhe G. Pasi që nuk kemi shumë hapësirë, nuk do të rendis të gjithë kodin këtu, por ne do të zoomojmë në një pjesë jashtëzakonisht të veçantë. Kjo është pjesa që e bën vaksinën të funksionojë, pjesa që në të vërtetë do të na ndihmojë të kthehemi në jetën normale:

```
                  *   *
          L   D   K   V   E   A   E   V   Q   I   D   R   L   I   T   G
Virus:   CUU GAC AAA GUU GAG GCU GAA GUG CAA AUU GAU AGG UUG AUC ACA GGC
Vaccine: CUG GAC CCU CCU GAG GCC GAG GUG CAG AUC GAC AGA CUG AUC ACA GGC
          L   D   P   P   E   A   E   V   Q   I   D   R   L   I   T   G
           !     !!! !!        !   !       !   !   !   ! !              

```

Këtu shihen ndryshimet e zakonshme sinonime të ARN-së. Për shembull, në kodonin e parë shohim që CUU e virusit është ndryshuar në CUG të vaksinës. Kjo shton një ‘G’ tjetër të vaksinës, të cilën ne e dimë se ndihmon në rritjen e prodhimit të proteinave. Si CUU ashtu edhe CUG përkthehen aminoacidin ‘L’ ose Leucine, kështu që në fakt, në proteinë nuk ka ndryshuar asgjë.

Kur krahasojmë të gjithë proteinën Gozhdë (Spike protein) që është rezultat i   vaksinës, të gjitha ndryshimet janë sinonime si kjo .. përveç dy prej tyre, të cilat janë ndryshime të vërteta.

Kodoni i tretë dhe i katërt më lart paraqesin ndryshimet aktuale. Aminoacidet K dhe V atje të dy zëvendësohen nga ‘P’ ose Proline. Për aminoacidin ‘K’ kjo nevoiten tre ndryshime (‘!!!’) dhe për ‘V’ nevoiten vetëm dy (‘!!’).

**Rezulton se këto dy ndryshime rrisin efikasitetin e vaksinës jashtëzakonisht shumë.**

Po çka po ndodh këtu? Nëse shikoni një virus të vërtetë SARS-CoV-2 nën mikroskop, aty mund të vëreni proteinën gozhdë (Spike protein), paj, si një grup gozhdash:

![](https://i.snap.as/MFj6ivQC.jpg)
*[Virusi SARS](https://en.wikipedia.org/wiki/Severe_acute_respiratory_syndrome_coronavirus) (Wikipedia)*

Gozhdat janë të "montuara" në trupin e virusit ('proteina nukleoplazmide'). Por puna është që, vaksina jonë i gjeneron vetëm gozhda dhe nuk i "monton" në asnjëlloj trupi të virusit.

Rezulton se, proteinat gozhdë (Spike protein) të pa modifikuara, të pavarura, kolapsohen ose deformohen në një strukturë apo formë tjetër. Nëse kjo strukturë do të injektohej si vaksinë, kjo me të vërtetë do të bënte që organizmi yne zhvillojë imunitet ..  mirëpo imuniteti i zhvilluar do të ishte  vetëm kundër proteinave të deformuara gozhdë (që në fakt nuk janë me në formën e gozhdës).

Në anën tjetër virusi SARS-CoV-2 paraqitet me proteinën reale në formë të gozhdës (Spike protein). Prandaj vaksina nuk do të ishte efikase në këtë rast.

Atëherë çka të bëjmë? [Në vitin 2017 u përshkrua se si vendosja e një zëvendësimi të dyfishtë Proline në vendin e duhur](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5584442/) do të bënte që proteinat gozhdë të viruseve  SARS-CoV-1 dhe MERS të marrin formën e tyre 'normale' 'para fuzionit' (kapjes në qelizë), edhe pa qenë pjesë e të gjithë virusit. Kjo funksionon sepse Proline është një aminoacid shumë rigjid dhe stabil. Ai vepron si një lloj armature, duke stabilizuar proteinën në gjendjen apo formën që duhet t’i paraqitet sistemit imunitar (pra në formë të gozhdës).

[Njerëzit](https://twitter.com/goodwish916) që e [zbuluan](https://twitter.com/KizzyPhD) këtë duhet të ecin vërdallë duke bërë "qake" ndërmjet vete. Sasi të padurueshme të mendjemadhësisë duhet të burojë prej tyre. [Dhe e gjitha do të ishte e merituar](https://twitter.com/McLellan_Lab/status/1291077489566142464).


### Fundi i proteinës

Nëse lëvizim nëpër pjesën e mbetur të kodit burimor, hasim disa modifikime të vogla në fund të proteinës gozhdë (Spike protein):

```
          V   L   K   G   V   K   L   H   Y   T   s             
Virus:   GUG CUC AAA GGA GUC AAA UUA CAU UAC ACA UAA
Vaccine: GUG CUG AAG GGC GUG AAA CUG CAC UAC ACA UGA UGA 
          V   L   K   G   V   K   L   H   Y   T   s   s          
               !   !   !   !     ! !   !          ! 
```

Në fund të proteinës hasim në një  ‘stop’ kodon, këtu i shënuar me një shkronjë të vogël 's'. Kjo është një mënyrë e sjellshme për të thënë që proteina duhet të mbarojë këtu. Virusi origjinal përdor stop kodonin UAA, vaksina përdor dy stop kodone UGA, helbete.


### Regjioni i papërkthyer 3'

Ashtu sikurse ribozomi kishte nevojë për një "uvertyrë" (e cila gjendet në regjionin fillestar 5') në mënyrë që të fillojë procesin e prodhimit të proteinave, i njëjti ka nevojë edhe për një "epilog" i cili gjendet në fund të proteinës në konstruktin që quhet 3' UTR (UnTranslated Region).

Shumë gjëra mund të shkruheshin në lidhje me 3' UTR, por këtu citoj [atë që thotë Wikipedia](https://en.wikipedia.org/wiki/Three_prime_untranslated_region): "Regjioni i papërkthyer  3' luan një rol vendimtar në shprehjen e gjeneve duke ndikuar në lokalizimin, stabilitetin, eksportin dhe efikasitetin e përkthimit të një mRNA... **pavarësisht nga dija jonë aktuale e 3' UTR-ve, ato janë ende mistere** ".

Ajo që dimë është se 3’-UTR të caktuara janë shumë të suksesshme në promovimin e shprehjes së proteinave. Sipas dokumentit të OBSH-së, vaksina BioNtech / Pfizer 3’-UTR u zgjodh nga "the amino-terminal enhancer of split (AES) mRNA and the mitoçondrial encoded 12S ribosomal RNA to confer RNA stability and high total protein expression". Komenti im për këte është, shumë mirë.

![](https://i.snap.as/AkBosB8n.jpg)

### Fundi AAAAAAAAAAAAAAAAAAAAAA

Fundi i mRNA është i poliadeniluar. Kjo është një mënyrë "fancy" e të thënurit se përfundon me plot AAAAAAAAAAAAAAAAAAA. Edhe mRNA është lodhur nga viti 2020 si duket.

mRNA mund të ripërdoret shumë herë, por kur ndodh kjo atëherë ajo humb disa nga A'të në fund të saj. Nëse humb shumë A, atëherë mRNA nuk është më funksionale dhe thjeshtë injorohet. Në këtë mënyrë, bishti ‘poli-A’ është njëfarë mbrojtje nga degradimi.

Mjaft studime janë bërë për të gjetur se cili është numri optimal i A-ve në fund për vaksinat e mRNA. Në literaturën e hapur kam lexuar se kjo arriti kulmin në rreth 120.

Vaksina BNT162b2 përfundon me:

```
                                     ****** ****
UAGCAAAAAA AAAAAAAAAA AAAAAAAAAA AAAAGCAUAU GACUAAAAAA AAAAAAAAAA 
AAAAAAAAAA AAAAAAAAAA AAAAAAAAAA AAAAAAAAAA AAAAAAAAAA AAAA

```

Këtu janë 30 A, pastaj një “10 lidhës nukleotidik” (GCAUAUGACU), i ndjekur nga 70 A të tjerë.

Unë mendoj se ajo që ne shohim këtu është rezultat i optimizimit të mëtejshëm nga ana e krijuesit të vaksinës për të rritur edhe më shumë shprehjen e proteinave.


### Përmbledhje

Nga kjo, ne tash e dimë përmbajtjen e saktë të ARN-së të vaksinës BNT162b2, dhe për shumicën e pjesëve ne e kuptojmë pse ato gjinden në vaksinë:

* 'kapaku' për tu siguruar që ARN e vaksinës duket si ARN i rregullt qelizor
* Regjion 5' i papërkthyer që është i ditur dhe është efikas
* Peptidi sinjalizues me kodonë të optimizuar i cili ka për detyrë t'a dërgojë proteinën gozhdë (Spike protein) në vendin e duhur (kopjuar 100% nga virusi)
* Proteina gozhdë (Spike protein) origjinale poashtu me kodonë të optimizuar e cila përmban dy ndryshime me 'Proline' në mënyrë që të ketë formën e duhur
* Regjion 3' i papërkthyer që është i ditur dhe është efikas
* Një bisht pak a shumë misterioz më plot A dhe një 'lidhës'

Optimizimi i kodoneve shton shumë G dhe C në mRNA. Ndërkohë, përdorimi i Ψ (1-metil-3’-pseudouridilil) në vend të U ndihmon në evitimin e sistemit tonë imunitar, kështu që mRNA qëndron rreth e rrotull mjaft kohë, në mënyrë që të mund të ndihmojmë në trajnimin e sistemit tonë imunitar.