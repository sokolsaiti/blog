---
title: "Era diellore"
date: 2021-01-05T21:08:38+02:00
draft: false # Set 'false' to publish
---

Me 8 Dhjetor 2020, apo 5 javë pas ditës së zgjedhjeve në SHBA, kompania [FireEye](https://www.fireeye.com/) [njoftoi](https://investors.fireeye.com/static-files/05bd98cf-59b0-4af1-89f2-89e5c8f783f8) zyrtarisht agjencionin amerikan SEC (Securities Exchange Commision) se ishte cak i një sulmi kibernetik. SEC si një agjencion i pavarur është përgjegjës për sigurinë në sistemin bankar dhe tregjeve me letra në vlerë, ndërsa FireEye është një kompani e cila specializon në shitjen e produkteve të sigurisë në fushën e teknologjisë informative. Sipas FireEye, "lloji i sulmit, mënyra, siguria operacionale, teknikat si dhe disciplina e sulmuesit kibernetik" çojnë drejt konkludimit se bëhet fjalë për një sulm të sponzorizuar nga ndonjë shtet.  <!--more-->

Kompanitë sikurse FireEye ndërmjet tjerash kanë produkte apo shërbime nëpërmjet të cilave zhvillojnë të ashtuquajturin "penetration test" apo test të depërtimit për klientët e tyre. Objektivi i këtij lloji të testit është (duh) "depërtimi" në rrjet dhe IT sisteme të klientit duke simuluar sulme kibernetike të "aktorëve të këqinjë", në këtë mënyrë vlerësohet se sa janë të sigurta. Kompanitë të cilat operojnë në fusha si financa, pagesa elektronike, shëndetësi, telekomunikacion dhe institucionet shtetërore (posaçërisht ato në SHBA) kryesisht janë klientë të kompanive të tipit të FireEye. Në shumicën e rasteve entitete të tilla operojnë me të dhana konfidenciale dhe është në interesin e tyre që sigurinë e sistemeve kompjuterike ta mbajnë të përditësuar.

Raporti i FireEye dërguar SEC bën të ditur se cak i sulmit ndaj tyre ishin pikërisht këto produkte apo vegla të cilat ishin vjedhur (apo eksfiltruar) në mënyrë që mëpastaj të analizohen dhe të nxjerren konkluza lidhur me klientët e tyre. Përmbajtja e këtyre veglave dhe mënyra si të përdoren duhet të jetë poashtu konfidenciale, pra konfidencialiteti është imperativ në krejt fushën.


### SolarWinds

Analizat e mëtejshme treguan se infiltrimi në sistemet kompjuterike të FireEye është realizuar pëmes një softveri të quajtur SolarWinds. Ky softver zhvillohet nga një kompani me po të njejtin emër.

![Llogo e SolarWinds](https://i.snap.as/39FHJL0A.jpg)



Kompanitë të cilat punësojnë psh. mbi 1000 persona (duke përfshirë edhe FireEye) dhe që kanë shumë pajisje kompjuterike në rrjetet e tyre korporative, menaxhimi dhe monitorimi i kompjuterëve, serverëve, switchëve, routerëve, IP telefonisë e çkamos tjetër bëhet pakës problematik. Për këtë arsye produktet softverike si ai i SolarWinds janë atraktive sepse mundësojnë menaxhimin e IT infrastrukturës në mënyrë të centralizuar, për këtë arsye kjo kompani është furnizuese e shërbimeve për plot kompani rreth e përqark globit.

Në mënyrë që të arrihet menaxhimi dhe monitorimi nga një sistem qendror atëherë nevoitet që po ky sistem të ketë qasje në të gjithë pajisjet kompjuterike në rrjetin korporativ; pra, vendosja e një sistemi të tillë është (pakës klishe por) shpatë me dy teha. Kjo do të thotë se sado që kompania X ka praktika superbe të sigurisë kibernetike, çdo lëshim sado i vogël në SolarWinds i zhvlerëson ato praktika. 

Nëse i kthehemi sulmit në FireEye, hulumtimet e mëtutjeshme zbuluan se "akterët e këqinjë" e kishin komprometuar **qysh në Mars 2020(!)** një komponentë të SolarWinds që quhet Orion. Pastaj kjo komponentë e komprometuar është instaluar si përditësim normal përmbi instalimin ekzistues të SolarWinds, komprometimi në këtë rast konsiston në ndryshimet e bëra në funksionalitet. Këto ndryshime bëjnë të mundur që kjo komponentë përveç funksionalitetit bazik t'i ketë edhe tiparet e [Kalit të Trojës](https://en.wikipedia.org/wiki/Trojan_horse_(computing)) gjë e cila i mundëson sulmuesit që t'a kontrollojë këtë softver nga largësia duke i dërguar komanda të ndryshme. Në rastin konkret bëhet fjalë për komanda të cilat i mundësuan sulmuesit nga largësia të performojë operacione si:

* Transfer i fajllave
* Ekzekutim i fajllave
* Skenim i sistemit (mbledhja e informatave lidhur me hardverin dhe sistemin operativ)
* Restartimi i sistemit (kompjuterit)
* Ndalja e shërbimeve të ndryshme të sistemit operativ (psh të antivirusit)

Vlen të ceket se në sektorin e sigurisë kibernetike poashtu ekzistojnë softverë të cilët për detyrë kanë detektimin e trafikut të dyshimtë në rrjetet kompjuterike. Pra teorikisht nëse dikush do të kopjonte ndonjë fajll të madh ose kopjimin do t'a bënte nga një kompjuter intern në ndonjë destinacion të dyshimtë atëhere këto sisteme do t'a kishin detektuar këtë aktivitet të dyshimtë. Kjo lidhet me funksionalitetin e parë dhe të dytë në listën mëlartme, gjë e cila në rastin konkret nuk ka funksionuar. Pra, FireEye nuk ka qenë në gjendje të detektojë diçka të dyshimtë për një kohë te gjatë sepse sulmuesit kanë qenë në gjendje t'a maskojnë trafikun e tyre në rrjetë sikur të ishte trafik legjitim duke u prezentuar si trafik i SolarWinds-it. Kjo tregon se kanë harxhuar një kohë të konsiderueshme duke i analizuar mekanizmat e brendshëm funksional të SolarWinds-it.

### Si kanë arritur sulmuesit t'a "trojanizojnë" një softver legjitim?

Konsensusi është që sulmuesi(t) e kanë komprometuar "zinxhirin furnizues" gjatë procesit të zhvillimit të softverit, me fjalë tjera, e kanë modifikuar kodin burimor dhe pastaj e kanë kompajluar dhe në fund e kanë publikuar si përditësim legjitim nga serverët e kompanisë SolarWinds.

Dëmi i saktë i krejt kësaj storie ende nuk  dihet, mirëpo ajo çka dihet është se SolarWinds ka diku rreth 18000 klientë të cilëve u është distribuar përditësimi i komprometuar i Orion-it. Disa prej klientëve më me renome janë:

* Department of Homeland Security
* Department of Justice
* Department of Defence
* Banka të ndryshme
* Etj të ndryshme

Të shohim.

#solarwinds
#solarwindsOrion
#sunburst
