+++
title = "Kan Skycoin udsættes for 51% angreb?"
tags = [
    "Statement",
    "Obelisk",
    "Consensus",
]
bounty = 8
date = "2017-10-07"
categories = [
    "Statement",
]
+++

*Dette er et arkiveret indlæg fra bitcointalks tråd fra 16. februar 2015*

> Citat fra: **iamback** 16. februar, 2015, 09:28:38

> En ikke-PoW konsensus vil være dødsdømt fra start, fordi der ikke er tid nok til at løse problemerne og stole på løsningen før den globale økonomi kollapser i 2016. F.eks. det selviske mining angreb blev ikke opdaget (eller lad os sige bevist og anerkendt) før flere år efter Satoshi publicerede PoW. Derfor vil den seriøse handelsplads ikke stole på en ny ikke-PoW konsensus. I stedet har jeg designet et PoW system der løser mange af de problemer der plager Bitcoin, inklusiv ASIC økonomi. Der er hints i mit linkede indlæg ovenfor.

> Desuden har jeg en matematisk fornemmelse der siger mig, at for at undgå 51% angreb vil der altid opstå et andet sikkerhedshul.

Med Skycoin er 51% angreb ligegyldige. Netværket kan blive angrebet af tyve 51% angreb om dagen, og stort set alle vil være ligeglade.

Skycoin har anderledes strengere matematiske egenskaber end Bitcoin. Hvis du handler coins frem of tilbage mellem fem personer i et lukket netværk, vil 51% angrebet ikke påvirke nogle af dem. Du skal bruge en private key fra en i handelskæden for at skade nogen i et Skycoin 51% angreb. Der er ikke nogen transaktions bøjelighed i Skycoin. Næsten alle vil have samme outputs, samme balancer og samme transaktionshistorik på den originale kæde og den fork'ede kæde, på nær angriberen og folk der har handlet med denne. Hvis der er en fork af kæden, vil den bare kopiere transaktioner over fra de andre kæder.

51% angrebet vil kun påvirke folk der day trader med skumle typer og gambling sider. Det vil ikke påvirke handels transaktioner ret meget. Hvis en valutabørs følger de bedste sikkerhedsstandarder og holder brugernes wallets adskilt, vil det værste angreb være forholdsvis mildt.

Bitcoin flytter 100 millioner dollar om dagen i transaktions volumen. Den mængde i Bitcoin er omkring 200.000 Bitcoins. Bitcoin har transaktions bøjelighed, hvilket betyder at hvis nogen laver et 51% angreb og ruller transaktionerne fra den sidste time tilbage, vil omkring 4 millioner dollar og 10.000 Bitcoins i transaktions balancer blive ødelagte. En tilbagerulning for de sidste 24 timer kan lave skade for 100 millioner dollar og op til 200.000 Bitcoins. En angriber kan rulle enhver transaktion tilbage.

Med Skycoin kan angribere ikke påvirke eller ændre en transaktionskæde, uden at kende en private key for en adresse der er brugt i kæden af transaktioner. Så hvis fem banker handler frem og tilbage, og de alle har optimal wallet sikkerhed, vil de ikke engang opfatte 51% angrebet. Deres kontobalancer vil være de samme. Og det er med den hypotese, at 51% angreb overhoved er matematisk mulige, og der er nogen der gider ulejlige sig med at bruge så mange resurser på det og det tilmed lykkes.

Hvis nogle lykkes med at lave et 51% angreb på Skycoin (hvilket måske er muligt, men matematisk usandsynligt) vil forretningsejere stadig juble af glæde, for deres tab vil være meget mindre end hvis Visa tilbagekalder en transaktion de har modtaget. Mange butikker sælger bærbare computere med en profitmargin på mindre end 5%. Hvis en kunde hævder ikke at have modtaget computeren, vil Visa føre pengene tilbage til kunden, butikken får ikke computeren tilbage, og butikken skal betale en bøde på 500 kr. til Visa. Butikken skal sælge 25 computere for at tjene omkostningerne hjem for en enkelt svindler. Hvis en person stjæler et Visa kort og køber en bærbar med det, dækker Visa ikke omkostningerne, de bliver ført videre til butikken.

Skycoins konsensus algoritme og hovedbogen er adskilte. Konsensus systemet er et selvstændigt modul, som kan udskiftes efter behov. Hvis der om fem år kommer en bedre algoritme, kan vi bare skifte til den nye. Hovedbogen og brugernes kontobalancer vil være helt uændrede. 

Skycoin:

- Fixer eksisterende problemer med Bitcoin.
- Fremtidssikrer Bitcoin.
- Eliminerer den dødsspiral som Bitcoin har sat sig selv i.

Det er 100% sandt. Der er dog alvorlige kompromiser. For eksempel, hurtigere konsensus tider for Skycoin-agtig relationel konsensus betyder der skal færre noder til at udføre et DDoS angreb på netværket. Til gengæld kan folk reagere ved at fjerne noderne fra deres lister over sikre noder.

Der vil være problemer der skal løses.

## Skycoins Transaktions Struktur

https://github.com/skycoin/skycoin/blob/master/src/coin/transactions.go

En Skycoin transaktion er:

1) En liste af output hashes der bliver brugt
2) En liste af signaturer der sikrer de outputs der bliver brugt (signatur af hashen af den indre part af transaktionen)
3) En liste af outputs der skal laves

Coins kan ikke blive skabt eller destrueret. Antallet af indgående coins skal svare til det udgående antal. Transaktions gebyrer bliver betalt i "coin timer".

## Skycoin er født med Coinjoin support

Der er ikke nogen forskel på normale og coinjoin transaktioner.

- To personer vælger det output de vil bruge, og sender disse outputs til en remote server.
- Serveren laver en transaktion og krypterer rækkefølgen af outputs ind/ud, og sender til hver person.
- Hver person sender signaturen for deres outputs til serveren.
- Coinjoin serveren indsætter transaktionen i netværket.

- Coinjoin serveren kan ikke stjæle coins.
- Kun coinjoin serveren ved hvor mange personer der er involverede (1, 2, 4?).
- Kun coinjoin serveren ved hvem hvilke outputs tilhører.
- Der er ingen forskel på en coinjoin og en normal transaktion (de ser helt ens ud).

Signaturen i den n'te position tilhører adressen der ejer det n'te output. Den indre hash af transaktionen er hashed med hashen af det output der bliver brugt, og er derefter signeret med private key'en der ejer outputtet.

Det er derfor rigtig simpelt ift. andre coinjoin systemer.
