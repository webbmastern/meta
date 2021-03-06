 SMAB: Statusrapport 3/3
==========================

## Changelog

  * 7/2:  reviderade dokumentet för att matcha förändringar i projektets
          utveckling och förlopp. (Jonas, John, Emil)
  * 13/2: lade till rubrikerna *Dokumentation* och *Träning*, justerade
          formuleringar och lade till skisser.
  * 3/3:  Updaterade research delen genom att lägga till vad vi efterforskat om 
          gif-parsers och livestreamingtjänster.


## Sales pitch

  Playhouse är ett projekt som går ut på att göra om en byggnad till en stor
  interaktiv display där man kan visa såväl animationer som spela enklare spel
  genom ett webbgränssnitt.


## Projektbeskrivning

  Vi ska skapa ett system för att styra färgade lampor som ska sitta i
  fönster så att byggnaden blir en enorm skärm.  Skärmen ska kunna visa
  animationer och användas för att spela spel.  Det ska gå att i ett senare
  skede koppla elektroniska instrument (exempelvis synth) så att de utöver
  att spela upp ljud också ändrar lamporna.  När skärmen är i spelläge så kan
  spelare ställa sig i en kö i ett webbgränssnitt, där de sedan eventuellt
  paras ihop med andra spelare för att kunna spela ett spel.


## Mål

  Att via ett webbgränssnitt låta användare spela ett spel där spelplanens
  pixlar består av fönster på en byggnad.  Vid en högre belastning ska
  spelarna ställas i kö.  Spelplanen ska visas för användaren med hjälp av en
  videoström av byggnaden och en virtuell spelplan för att minska problem med
  tidsfördröjning av videoströmmen.  Libido ska kunna ställa in vilket spel
  som användarna kan spela samt om det istället ska visas en animation på
  husfasaden samt hur denna animation ser ut.  Vi har också som mål att man i
  framtiden kan utvidga projektet för att hantera byggnader med speciella
  former.  Under detta projekt begränsar vi oss dock till rektangulära
  fasader.


## Förutsättningar (externa)

  * Vi måste använda lampor (troligtvis Hue) som ska belysa fönstren inifrån.
    - Kunden måste tillhandahålla hårdvara att arbeta med
  * Interaktiv display.
  * Kösystem för spelare när de väntar.
  * Videoström av byggnaden som spelklienter kan se.


## Proof-of-concept

  En demonstration av spelet tic-tac-toe demonstrerades den 29e januari i KTHs
  lokaler på en fasad med nio fönster efter önskemål från kund utav detta.
  Detta demo bekräftar att projektidén med lampor i fönster fungerar som
  tänkt.


## Roller

  * Projektledare: Emil
  * Projektsekreterare: Markus
  * Kundrelationer: Arvid
  * Scrum Master: Emil
  * Product Owner: Arvid
  * Kvalitetssäkring: Alla
  * Utveckling: Alla


## Gruppmedlemmar

   Namn                   | Mail
  ------------------------|-----------------
   John Eriksson          | johne2@kth.se
   Arvid Fahlström Myrman | arvidfm@kth.se
   Jonas Höglund          | jhoglun@kth.se
   Hannes Leskelä         | hleskela@kth.se
   Christian Lidström     | clid@kth.se
   Mattias Palo           | mpalo@kth.se
   Markus Videll          | mvidell@kth.se
   Tomas Wickman          | tomaswic@kth.se
   Emil Öhman             | emiloh@kth.se


## Utvecklingsmetod

  Vi har bestämt oss för att jobba enligt den agila utvecklingsmetoden Scrum
  efter att ha jämfört olika metoder gäntemot varandra och mot de
  förutsättningar som gruppen har.  Detta beslut grundar sig på jämförelsen på
  http://www.nada.kth.se/~karlm/mvk/mvk09_lec3.pdf, som vi tycker verkar vara
  en tillförlitlig källa.

  Vi har valt att använda väldigt korta sprints för att få mer finkornig
  kontroll över vad som görs och snabbt kunna hantera problem som uppstår om
  något tar längre tid än beräknat eller blir försenat.  Gruppmedlemmarna är
  överens om att de snabbare sprintsen ger ökad effektivitet i arbetet.


## Planering

### Aktiviteter

  * Utveckla lampserver
    - Implementera JSON-API

  * Utveckla spelbackend
    - API för spelmoduler
    - Implementera tic-tac-toe som spelmodul
    - Implementera fyra-i-rad

  * Utveckla spelfrontend
    - Sätta upp websocket-kommunikation

  * Utveckla kösystem

  * Utvärdera
    - Lampteknik (lampräckvidd mm)
    - Möjlighet att använda GIF
    - Design av eget filformat?
    - Inbäddning av videoström i spelfrontend

  * Dokumentera
    - Lampinstallation
    - Projektets arkitektur (separat)
    - Installation av komponenter


### Beroendegraf mellan komponenter

  ![Komponentberoendegraf](https://github.com/smab/meta/raw/master/deliverable/task-dependencies.png)


### Milstolpar (och tidsplan)

Milstolpar under projektets gång redovisas nedan.  Milstolparna
MS1 och MS2 har uppnåtts under tidigt skede i projektet och visas därmed ej
nedan.

* MS3 (Februari 2014)
  - [lampor] Lampserver kan styra bryggor och lampor för att ändra specifika
    lampor.
  - [webserver] Fungerande kösystem med turordning.
  - [frontend] Början på UI för kösystem/spel, kösystem fungerar och kopplad
    till server.

* MS4 (Mars 2014)
  - [config] Stöd för: spelkonfiguration med fyra i rad och tre i rad,
    möjlighet att spara inställningar till server.
  - [frontend] Fungerande spelgränssnitt, frontend klar.

Planeringen är preliminär, och är tänkt att ta hänsyn till vilka uppgifter som
beror på vilka, och potentiella risker som är associerade med olika moment.


## Forskning

  Vi har satt upp en gemensam testplats och en testrigg med nio lampor.
  Riggen är i KTHs lokaler, och vi har satt upp en kamera som streamar
  lampornas status.  Tellsticktekniken återanvänds för att kontrollera
  eltillförseln till riggen, så att lamporna kan stängas av när de inte
  används.  Lamporna kan kontrolleras utifrån, vilket gör det möjligt att
  testa ändringar utifrån.

  Efter att ha utvärderat Hue-lamporna så har vi kommit fram till att dessa är
  betydligt bättre lämpade för vårt ändamål än tekniken Tellstick.  Fördelar
  med Hue-tekniken är bland annat bättre stabilitet, starkare lampor, bättre
  stöd för olika färger samt färdiga APIer som vi kan kommunicera med.  Vi har
  beslutat oss för att skriva backenden i Python, och har implementerat kod
  för att kommunicera med Hues lampservrar över HTTP via deras REST-API som
  använder JSON.

  Som nämndes ovan så implementeras webbackenden i Python, mer specifikt har
  vi bestämt oss för webbserverbiblioteket Tornado.  Detta beslut grundar sig
  på att Tornado enligt jämförelser och designfilosofi har som mål att klara
  höga belastningar samt bra inbyggt stöd för tekniker så som websockets som
  vi ämnar att använda.

  Vi har arbetat med idén att använda GIF-animationer för lagring av våra
  animationer, där tanken är att vi slipper skriva ett eget verktyg för att
  skapa animationer då det redan finns kompetenta sådana som vi funnit efter 
  en del efterforskningar.  Istället tänker vi lägga större vikt på 
  lampserverkomponenten och att få animationer att synkroniseras bra.  Vi har
  kollat på ett par olika animationsverktyg och konstaterat att det verkar
  finnas tillräckligt bra sådana tillgängliga. En del tekniska bekymmer 
  kvarstår, så som skillnaden på färgspektrum för GIF och våra Hue-lampor.
  Vi har hittat gif-verktyg som verkar passa våra behov bra. Då det enda vi
  egenligen eftersöker är ett enkelt gränssnitt för att skapa simpla animationer
  så spelar det inte så stor roll om det saknar en del funktionalitet. Likt
  livstreamingtjänsen så kommer det i slutändan inte vara vi som kommer behöva tilhandahålla
  ett gifanimeringsverktyg utan vi ska bara tillföra möjligheten att kunna ladda upp gifanimationer
  till servern så att denna spelar upp animationen till lamporna. Vi har dock genomfört en
  del forskning inom verktyg och kommit fram till att Asesprite verkar som ett lämpligt verktyg
  för att utföra de tester som vi behöver utföra. Det är dessutom
  släppt med öppen källkod på programmet vilket vi tycker är ett plus.
  
  Vi har diskuterat olika livestreamingtjänster inom gruppen som verkar 
  lämpliga, men det är svårt att dra några slutsater i detta skede då det 
  ligger utanför våran arbetsbeskrivning att implementera en streamingtjänst.
  Men att på ett enkelt sätt tillhandahålla möjligheten att implementera en 
  livestreaming på våran hemsida känns som en relevant och överkomlig uppgift.
  
  De livestreamingtjänster som vi diskuterat inom gruppen är som följer med sin för/nackdelar:
  
  XSplit*
  -Betallösning
  -Endast Windows

  OBS (Open Broadcaster Sowftware)*
  -Gratis
  -Windows, Linux kommer släppas

  FFSplit*
  -Gratis
  -Windows

  Wirecast
  -Betallösning
  -Windows, Macintosh

  FFmpeg
  -Gratis
  -Windows, Macintosh, Linux
  -Kommandorad
  -Massa bra info, bla om tidsfördröjning och hur man kopplar ihop med twitch. https://
   trac.ffmpeg.org/wiki/StreamingGuide
 
 Simple Screen Recorder
 -Gratis
 -http://www.maartenbaert.be/simplescreenrecorder/live-streaming/
 -Kommandorad, och vanligt
 -Kan vara buggigt


## Scenarier, krav och behov

### Scenarier

  Glenn ska inviga en byggnad i centrala Göteborg och vill ha något spektakulärt
  Han bestämmer sig för att anlita Libido Music för att installera lampor och
  göra någon cool show. Libido kommer och installerar lampor i Glenns byggnad
  samt gör en demo. Showen görs av Libido hos deras kontor vid Karlaplan och
  visas på något sätt upp på invigningsdagen.

  Karl-Bertil går förbi en cool byggnad i stan med massa lampor på. Han ser en
  liten informationsskylt framför byggnaden som säger att om han går in på
  example.com så kan han spela ett spel där han använder byggnaden som en stor
  skärm. Han skriver in addressen och hamnar i en kö. Det står att han har plats
  10 av 11.  Till slut kommer han att paras ihop med någon annan spelare och de
  kan på ett enkelt sätt spela något spel.


### Krav

Användaren måste kunna

  * Skapa en animation
    - Tänder lampor i olika färger och styrkor
    - Sätta färg, styrka, tidsfördröjning på lampor.

  * Spela enkla spel
    - Minst ett spel. Tic-tac-toe, 4-i-rad...
    - Mot varandra
    - Spelare hamnar i en kö

  * Libido/byggnadsägaren ska ha möjlighet att enkelt administrera
    installationen.
    - Byta spel samt konfigurera färgval
    - Byta animation
    - Skärmsläckare (dvs animation) om ingen spelar?

Se även tidigare avsnitt om projektets externa förutsättningar.


### I mån av tid

  * Stöd för olika form på fasader
    - I dagsläget förutsätter vi rektangulära husfasader, men i praktiken kan
      många aktuella hus ha ickerektangulär fasad.  I sådana fall är det
      önskvärt att på något sätt kunna ange utseendet på fasaden.

  * Förenkla hopkoppling mellan lampor och bryggor
    - Idag behöver man koppla samman lampor med bryggor genom att skruva i en
      i taget och köra ett program mellan varje lampa.  Det skulle förenkla
      installation av lampor i byggnad avsevärt om man kunde skruva i alla
      lampor på en gång och sedan via ett gränssnitt mappa lamporna till
      pixlar.
    - För att verifiera att allt satts upp i rätt ordning vore det användbart
      med ett testprogram som lyser upp lamporna enligt ett förbestämt
      mönster, ex. rad för rad och kolumn för kolumn.


## Teknologi och arkitektur

  Vår applikation har två sorters användare: dels vår klient, som behöver kunna
  skapa animationer etc., och dels vanliga personer som ansluter via en
  webbläsare för att spela. För att kunna hantera flera spelare implementerar vi
  ett kösystem, då det inte går att spela flera spelomgångar samtidigt. När en
  spelare har nått längst fram i kön kommer spelaren att få se något gränssnitt
  där den kan spela själva spelet samt livevideo som visar den faktiska
  byggnaden där lamporna är installerade.

  Detta innebär att det behövs någon sorts webbserver som har som funktion att
  skicka individuella sidor till användaren, samt som hanterar kö- och
  spellogiken. Vi har bestämt oss för att använda Python tillsammans med
  webbservermjukvaran Tornado, se diskussion under Research tidigare i
  dokumentet.

  Vi behöver också någon komponent så hanterar kommunikation med de bryggor som
  i sin tur kommunicerar direkt med lamporna. Vi ansåg att det vore lämpligt att
  implementera webbkomponenten och lampkommunikationskomponenten som två
  separata servrar.

  Då vi behöver kunna visa livevideo från byggnaden kommer vi också att behöva
  kunna kommunicera med någon server som är kopplad till en kamera.  Detta är
  tänkt att ske via en streamingtjänst, exempelvis Bambuser.


### Arkitekturdiagram

  ![Komponentdiagram](https://github.com/smab/meta/raw/master/deliverable/component_diagram.png)


## Risker

  Risk | Åtgärd | Sann. | Impact
  -----|--------|-------|----------
  Kommunikation mellan bryggor och lampor är opålitlig (väldigt stor fördröjning, tappar signaler, etc.) | Fixa eventuella buggar; Använda fler bryggor vid behov; Programmera egen brygga | Hög | Hög
  Kommunikation mellan lampservern och bryggorna är bristfällig (för långsam/opålitlig) | Fixa eventuella buggar; Fixa diverse tekniska problem med anslutning | Medel | Hög
  Lamporna stör varandra när de har olika färger (t.ex. två fönster inom samma rum) | Skärmar mellan lamporna; Begränsa så att lampor i samma rum alltid har samma färg | Låg | Medel
  Problem med ihopkopplingen av delsystem(lamp- och webbserver etc.) (interna protokoll matchar inte, inkorrekt data, etc.) | Fixa eventuella buggar | Medel | 11/10
  Webbservern och/eller webbgränssnittet är instabila | Fixa eventuella buggar | Medel | Medel
  Webbservern får fler besökare än den kan hantera (överbelastning, stort intressen, DoS) | Köra webbserver i molnet (Amazon eller liknande); Optimera koden lite; Stäng av spel och spela animation istället (ej interaktiv dock); Iptables-magi? (droppa paket) | Låg | Medel
  Osynkade animationer (lampor byter färg i varierande hastigheter så att lamporna är i osynk med varandra) | Använda fler bryggor; Begränsa animationerna så att de inte är för beroende av perfekt synk | Medel | Medel
  Webbkamerastreaming fungerar dåligt (lamporna syns dåligt, dålig bildkvalitet, laggigt, ingen bild alls, kameran ramlar ner) | Fixa eventuella buggar; Bättre Internetuppkoppling; Bättre kamera; Bättre kamerainstallation | Medel | Medel
  Huset syns dåligt i webbkameran p.g.a väderleksförhållanden eller liknande, t.ex. regn eller dimma. | [Bättre väder][1]; Stänga av Playhouse när det är dålig sikt | Låg | Låg

[1]: http://en.wikipedia.org/wiki/Weather_modification


## Dokumentation

  Dokumentation av kodbasen görs successivt under utvecklingen, så att
  framtida utvecklare kan ta över och fortsätta projektet.  Själva
  arkitekturen och installation av komponenter måste också dokumenteras.
  Dokumentation av arkitekturen finns i begränsad mån i detta dokument i
  dagsläget, men bör migreras till ett separat dokument och göras mer
  fullständig.


## Träning

  Vårt projekt involverar två sorters användare: de som installerar lamporna
  och bestämmer vad som visas, och slutanvändare som interagerar med
  installationen genom spel via en spelfrontend.  Det senare är
  förhoppningsvis intuitivt (spelarna antas känna till reglerna för tre-i-rad
  och fyra-i-rad).  Den förstnämnda gruppen behöver dock någon form av guide,
  inte minst för installationen av lampor.  Det nuvarande systemet för
  installation är temporärt; vi planerar att dokumentera uppsättningsprocessen
  när vi har fått ett bättre system på plats.  Även hur man ställer in
  animation och väljer spel bör dokumenteras, men för detta ändamål bör det
  räcka med en relativt kort hjälptext i själva gränssnittet.


# Appendix A: Skisser

  I detta appendix inkluderas skisser på de olika gränssnitt olika typer av
  användare kan se, som berör projektet.

## Konfiguration

  ![Konfiguration](https://github.com/smab/meta/raw/master/deliverable/images/sketch-config.png)


## Spel
  Vi har just nu flera idéer på hur spelgränssnittet kan se ut.  Skisser på
  desas inkluderas nedan.

  ![Spelfrontend: förslag 1](https://github.com/smab/meta/raw/master/deliverable/images/sketch-game-1.png)

  ![Spelfrontend: förslag 2](https://github.com/smab/meta/raw/master/deliverable/images/sketch-game-2.jpg)
