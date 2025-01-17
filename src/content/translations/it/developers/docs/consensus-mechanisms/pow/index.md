---
title: Proof of Work (PoW)
description: Spiegazione del consenso con il protocollo Proof of Work e il suo ruolo in Ethereum.
lang: it
incomplete: true
---

Ethereum, come Bitcoin, usa attualmente un protocollo di consenso chiamato **[Proof of Work (PoW)](https://wikipedia.org/wiki/Proof_of_work)**, che consente ai nodi della rete Ethereum di concordare sullo stato di tutte le informazioni registrate sulla blockchain Ethereum e impedisce alcuni tipi di attacchi economici.

Durante il prossimo anno, il Proof of Work sarà progressivamente dismesso a favore del **[Proof of Stake (PoS)](/developers/docs/consensus-mechanisms/pos)**. La transizione al Proof of Stake eliminerà anche il mining da Ethereum. [Maggiori informazioni sulla fusione.](/upgrades/merge/)

## Prerequisiti {#prerequisites}

Per comprendere meglio questa pagina, ti consigliamo innanzi tutto di leggere il materiale relativo alle [transazioni](/developers/docs/transactions/), [ai blocchi](/developers/docs/blocks/), e [ai meccanismi di consenso](/developers/docs/consensus-mechanisms/).

## Cos'è la Proof of Work (PoW)? {#what-is-pow}

Il Proof of Work è il meccanismo che consente alla rete decentralizzata di Ethereum di raggiungere il consenso o di giungere a un accordo su cose come i saldi degli account e l'ordine delle transazioni. Ciò impedisce agli utenti di "spendere due volte" le proprie monete e assicura che la catena di Ethereum sia estremamente difficile da attaccare o manipolare.

## Proof of Work e mining {#pow-and-mining}

Il Proof of Work è l'algoritmo sottostante che imposta la difficoltà e le regole per il lavoro che i miner devono svolgere. Il mining è il "lavoro" stesso. Si tratta dell'atto di aggiungere blocchi validi alla catena. Questo è importante perché la lunghezza della catena aiuta le rete a seguire la corretta catena Ethereum e a capire lo stato attuale di Ethereum. Più "lavoro" viene svolto, più è lunga la catena, più elevato è il numero di blocchi e più alta è la certezza che la rete si trovi allo stato delle cose attuale.

[Maggiori informazioni sul mining](/developers/docs/consensus-mechanisms/pow/mining/)

## Come funziona la Proof of Work di Ethereum? {#how-it-works}

Le transazioni di Ethereum vengono elaborate in blocchi. Ogni blocco ha una serie di attributi:

- difficoltà del blocco, ad esempio: 3.324.092.183.262.715
- un mixHash, ad esempio: `0x44bca881b07a6a09f83b130798072441705d9a665c5ac8bdf2f39a3cdf3bee29`
- nonce, ad esempio: `0xd3ee432b4fb3d26b`

Questi blocchi di dati sono correlati direttamente al Proof of Work.

### Il lavoro nel Proof of Work {#the-work}

Il protocollo di Proof of Work, detto Ethash, richiede che i miner attraversino un intenso processo di tentativi ed errori per trovare il nonce di un blocco. Solo i blocchi con un nonce valido possono essere aggiunti alla catena.

Quando compete per creare un blocco, un miner inserisce ripetutamente un set di dati, ottenibile solo tramite il download e l'esecuzione dell'intera catena (che è quello che fa il miner), attraverso una funzione matematica. Il set di dati viene utilizzato per generare un mixHash al di sotto di un nonce target, come dettato dalla difficoltà del blocco. Il miglior modo per farlo è tramite un processo di ripetuti tentativi ed errori.

La difficoltà determina il target per l'hash. Più basso è il target, più piccolo è il set di hash validi. Una volta generato, è incredibilmente facile per gli altri miner e client verificarne la bontà. Anche se una transazione dovesse cambiare, l'hash sarebbe completamente diverso, segnalando una potenziale frode.

L'hashing permette di individuare le frodi con facilità. Inoltre, il processo del Proof of Work costituisce anche un grande deterrente contro gli attacchi alla catena.

### Proof of Work e sicurezza {#security}

I miner sono incentivati a svolgere questo lavoro sulla catena principale di Ethereum. L'incentivo a iniziare una catena propria è molto ridotto per i miner, perché minerebbe il sistema. Le blockchain fanno affidamento sul fatto di avere un solo stato di riferimento, che è considerato l'unica fonte di verità. E gli utenti sceglieranno sempre la catena più lunga o più "pesante".

L'obiettivo della PoW è di estendere la catena. La catena più lunga è quella più credibile in termini di validità, perché è quella che racchiude in sé la maggior parte del lavoro computazionale eseguito. Nel sistema PoW di Ethereum è praticamente impossibile creare nuovi blocchi che cancellino transazioni o che ne creino di false, o mantenere una seconda catena. Questo perché un miner malevolo dovrebbe sempre risolvere il nonce del blocco più velocemente di chiunque altro.

Per creare costantemente blocchi malevoli ma validi, bisognerebbe avere più del 51% della potenza di mining della rete, per poter battere tutti gli altri. Servirebbe davvero un'enorme potenza di calcolo per essere in grado di affrontare questa quantità di "lavoro". E il costo dell'energia utilizzata potrebbe anche superare i guadagni ottenibili con un attacco.

### L'economia della Proof of Work {#economics}

Il Proof of Work è anche responsabile del rilascio di nuova valuta nel sistema e dell'incentivazione dei miner a fare il proprio lavoro.

I miner che creano correttamente un blocco sono premiati con due ETH appena coniati, ma non ricevono più tutte le commissioni sulle transazioni, poiché la commissione di base viene bruciata, mentre la mancia e la ricompensa del blocco vanno al miner. Un miner può ottenere anche 1,75 ETH per un blocco zio (uncle block), Con blocco zio si intende un blocco valido creato da un miner praticamente nello stesso momento in cui un altro miner estrae il blocco valido. Questa condizione in genere si verifica a causa della latenza della rete.

## Finalità {#finality}

Una transazione ha una "finalità" su Ethereum quando fa parte di un blocco che non può cambiare.

Dato che i miner lavorano in modo decentralizzato, è possibile che due blocchi validi vengano minati nello stesso momento. In questo caso, si crea una diramazione temporanea. Alla fine verrà accettata una sola catena (quella più lunga), creata quando verranno eseguiti il mining e l'aggiunta di un blocco successivo.

Per complicare ulteriormente le cose, le transazioni che erano state rifiutate sulla diramazione temporanea potrebbero essere state aggiunte alla catena accettata. Questo significa che la catena potrebbe essere annullata. Quindi la finalità si riferisce al tempo che occorre attendere prima di considerare una transazione irreversibile. Per Ethereum, il tempo raccomandato è di sei blocchi o poco più di 1 minuto. Dopo sei blocchi, si può affermare con una certa sicurezza che la transazione ha avuto successo. Si può anche aspettare più a lungo per avere una maggiore sicurezza.

La finalità è un aspetto da tenere a mente quando si progettano le dApp. Sarebbe controproducente in termini di user experience fornire informazioni errate sulla transazione, soprattutto se è di alto valore.

Ricorda che il periodo di tempo non include l'attesa che intercorre prima che la transazione venga prelevata da un miner.

## Consumo energetico del Proof of Work {#energy}

Una delle principali critiche mosse al Proof of Work riguarda la quantità di energia necessaria per mantenere la rete sicura. Per garantire la sicurezza e la decentralizzazione, il sistema Proof of Work di Ethereum consuma 73,2 TWh all'anno, l'equivalente del consumo energetico di un paese di medie dimensioni come l'Austria.

## Pro e contro {#pros-and-cons}

| Pro                                                                                                                                                                                                                                          | Contro                                                                                                                                                                                                   |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Il Proof of Work è neutrale. Non servono ETH per iniziare e le ricompense per i blocchi consentono di passare da 0 ETH a un saldo positivo. Con il [ Proof of Stake](/developers/docs/consensus-mechanisms/pos/) occorrono ETH per iniziare. | Il Proof of Work utilizza così tanta energia da risultare dannoso per l'ambiente.                                                                                                                        |
| Il PoW è un meccanismo di consenso testato e ben collaudato che mantiene Bitcoin ed Ethereum sicure e decentralizzate da molti anni.                                                                                                         | Chi desidera occuparsi di mining deve avere apparecchiature specializzate, con un conseguente notevole investimento iniziale.                                                                            |
| Rispetto alla Proof of Stake è relativamente facile da implementare.                                                                                                                                                                         | A causa della crescente richiesta di potenza di calcolo, alcuni i gruppi di mining potrebbero potenzialmente dominare l'attività di mining, portando così alla centralizzazione e a rischi di sicurezza. |

## Confronto con il Proof of Stake {#compared-to-pos}

Ad alto livello, il Proof of Stake ha lo stesso obiettivo del Proof of Work: permettere a una rete decentralizzata di raggiungere il consenso in totale sicurezza. Ma ci sono alcune differenze nei processi e nel personale:

- Il PoS scambia l'importanza della potenza di calcolo con gli ETH in staking.
- Il PoS sostituisce i miner con i validatori. I validatori fanno staking con i loro ETH per avere la possibilità di creare nuovi blocchi.
- I validatori non competono per creare blocchi, sono invece scelti casualmente da un algoritmo.
- La finalità è più chiara: in alcuni checkpoint, se i 2/3 dei validatori concordano sullo stato del blocco, questo è considerato definitivo. I validatori devono scommettere il loro intero stake su questo, per cui se dovessero provare a cospirare in seguito, perderebbero il loro intero stake.

[Ulteriori informazioni sul Proof of Stake](/developers/docs/consensus-mechanisms/pos/)

## Preferisci un approccio visivo all'apprendimento? {#visual-learner}

<YouTube id="3EUAcxhuoU4" />

## Letture consigliate {#further-reading}

- [Majority attack](https://en.bitcoin.it/wiki/Majority_attack)
- [On settlement finality](https://blog.ethereum.org/2016/05/09/on-settlement-finality/)

### Video {#videos}

- [Una spiegazione tecnica dei protocolli proof-of-work](https://youtu.be/9V1bipPkCTU)

## Argomenti correlati {#related-topics}

- [Mining](/developers/docs/consensus-mechanisms/pow/mining/)
- [Proof of Stake](/developers/docs/consensus-mechanisms/pos/)
