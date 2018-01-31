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

> En ikke-PoW konsensus vil være dødsdømt fra start, fordi der ikke er tid nok til at løse problemerne og stole på løsningen før den globale økonomi kollapser i 2016. F.eks. det selviske mining angreb blev ikke opdaget (eller lad os sige bevist og anerkendt) før flere år efter Satoshi publiserede PoW. Derfor vil den seriøse handelsplads ikke stole på en ny ikke-PoW konsensus. I stedet har jeg designet et PoW system der løser mange af de problemer der plager Bitcoin, inklusiv ASIC økonomi. Der er hints i mit linkede indlæg ovenfor.

> Desuden har jeg en matematisk fornemmelse der siger mig, at for at undgå 51% angreb vil der altid opstå et andet sikkerhedshul.

Med Skycoin er 51% angreb ligegyldige. Netværket kan blive angrebet af tyve 51% angreb om dagen, og stort alle ville være ligeglade.

Skycoin har anderledes strengere matematiske egenskaber end Bitcoin. Hvis du handler coins frem of tilbage mellem fem personer i et lukket netværk, vil 51% angrebet ikke påvirke nogle af dem. Du skal bruge en private key fra en i handelskæden for at skade nogen i et Skycoin 51% angreb. Der er ikke nogen transaktions bøjelighed i Skycoin. Næsten alle vil have samme outputs, samme balancer og samme transkationshistorik på den originale kæde og den forkede kæde, pånær angriberen og folk der har handlet med denne. Hvis der er en fork af kæden, vil den bare kopiere transaktioner over fra de andre kæder.

51% angrebet vil kun påvirke folk der day trader med skumle typer og gambling sider. Det vil ikke påvirker handels transaktioner ret meget. Hvis en valutabørs følger de bedste sikkerhedsstandarder og holder brugernes wallets adskilt, vil det værste angreb være forholdvis mildt.

Bitcoin flytter 100 millioner dollar om dagen i transaktions volumen. Den samlede mængde i Bitcoin er omkring 200.000 Bitcoins. Bitcoin har transaktions bøjelighed, hvilket betyder at hvis nogen laver et 51% angreb og ruller transaktionerne fra den sidste time tilbage, vil omkring 4 millioner dollar og 10.000 Bitcoins i transaktions balancer blive ødelagte. En tilbagerulning for de sidste 24 timer kan lave skade for 100 millioner dollar og op til 200.000 Bitcoins. En angriber kan rulle enhver transaktion tilbage.

In Skycoin, they cannot affect or modify a transaction chain without knowing a
private key for an address used in that chain of transactions. So if five
banks are just trading back and forth between each other for settlement and
they all have good wallet security, the 51% attack would not even be noticed.
Their balances are the same. That is assuming, the 51% attack is even
mathematically possible, that someone bothers expending the resources to
attempt it and that it succeeds.

If someone manages to 51% attack Skycoin (which may be possible, but is
mathematically unlikely) merchants will sing and dance with great rejoicement
because losses will be so much less than for a Visa charge back. Many
merchants sell laptops and make less than 5% margin on each laptop. Someone
claims they didnt get the laptop and the merchant loses $1000, does not get
the laptop back AND has to pay Visa an $80 fee. The company has to sell 25
laptops to make back the cost of the loss of a single fraud. If someone steals
a credit card and buys a laptop with it, Visa does not take the loss, Visa
pushes the loss on to the merchant.

The Skycoin consensus algorithm and the ledger are separate. The consensus
system is modular and can be swapped out. If there is a better algorithm five
years from now, we can just swap out the consensus for the new one. The ledger
and coin balances will be completely unchanged.

Skycoin:

- fixes existing problems with Bitcoin
- future-proofs Bitcoin
- eliminates the death spiral conditions that Bitcoin has engineered in

It is 100% true. There are severe tradeoffs. For example, faster
consensus times for Skycoin-type relational consensus means that a smaller
number of nodes are required to DDoS the network. However, people can react
and remove the nodes from their trust lists.

There will be issues and they will need to be worked out.

## Skycoin Transaction Structure

https://github.com/skycoin/skycoin/blob/master/src/coin/transactions.go

A Skycoin transaction is:

1) A list of output hashes, being spent
2) A list of signatures authorizing the outputs to be spent (signature of hash
   of inner part of transaction)
3) A list of outputs to be created

Coins cannot be created or destroyed. The number of coins in has to equal
number of coins out. Transaction fees are in "coinhours".

## Skycoin supports Coinjoin natively

There is no difference between normal and coinjoin transactions.

- Two people choose the outputs they want to spend, the outputs they want to
  create, send to remote server.
- The server creates a transaction and scrambles orders of outputs in/out.
  Then sends it to each person
- Each person sends the signatures for their outputs to the server
- The coinjoin server injects the transaction into the network

- The coinjoin server cannot steal the coins
- Only the coinjoin server knows how many people are involved (1, 2, 4?)
- Only the coinjoin server knows which outptus belong to who
- There is no difference between coinjoin and normal transactions (they look
  exactly the same)

The signature in the `i`th slot is for the address owning the `i`th output. The
inner hash of the transaction is hashed with hash of output being spent, then
this is signed with the private key owning the output.

So it is very simple compared to other coinjoin systems.
