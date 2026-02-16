---
title: "Agentic TotChef: Architetture software, Patterns, and Best Practices"
date: 2026-02-16T00:00:00+00:00
description: "L'articolo esplora l'architettura software, i design pattern e le best practice per progettare agenti AI scalabili e manutenibili, utilizzando un caso di studio chiamato 'TotChef' che genera menù settimanali per una bambina di 1 anno."
tags: [AI, GenAI, Agent, Ollama, Python]
---

<!-- Durante una sessione di lettura intensiva mi sono imbattuto su un libro molto interessante: Agentic Design Pattern di Antonio Gulli, Eng Director in Google. -->
# Introduzione

Lo sviluppo di codice sorgente coadiuvato da sistemi di intelligenza artificiale è ormai in crescita esponenziale.
Le capacità degli LLM forniti da vari provider consentono, anche in modalità [Zero-Shot Learning](https://www.promptingguide.ai/techniques/zeroshot), di generare codice sorgente di qualità con un livello di astrazione e complessità elevato.
I risultati, che ritengo sorprendenti, arrivano dall'utilizzo dei cosiddetti **Agent AI** (in modalità [ReAct](https://www.promptingguide.ai/techniques/react) e aiutati da [Server MCP](https://modelcontextprotocol.io/docs/getting-started/intro)), migliorando la produttività degli sviluppatori.

Ma fermiamoci un attimo. Mentre il mondo è coperto di entusiasmo e aspettative, è importante ricordare che la generazione di codice sorgente da parte di un LLM (in modalità agentica e non) 
**è solo una parte del processo di sviluppo software**. La richiesta di Software Architect è destinata a rimanere alta per scongiurare il rischio di creare software 
che, seppur funzionante, sia poco performante, difficile da mantenere, scalare ed estendere. 

A tutti noi è capitato di partecipare a progetti software che, seppur funzionanti, avevano un debito tecnico enorme e difficile da contenere. 
Il tempo e i costi spesso hanno influenzato negativamente la qualità del software, portando a soluzioni _quick and dirty_ che, sebbene risolvessero il problema immediato, 
aumentavano le percentuali di codice sorgente non performante e a volte anche esposto a vulnerabilità.

**La domanda è: in una fase in cui le tecnologie stanno evolvendo rapidamente, possiamo permetterci ancora una volta lo stesso errore?** 

**La risposta deve essere no**, anche perché, oltre al debito tecnico, in questo caso ci sono dei costi attivi (provider di servizi AI, DB vettoriali, ...) da considerare non indifferenti.

Utilizzando agenti AI senza una solida base di progettazione software, si corre il rischio di andare a braccio progettando sistemi che funzionano, ma che non sono scalabili e manutenibili.
Tra i rischi troviamo:
- "over-engineering", ovvero progettare sistemi troppo complessi per risolvere problemi semplici, con conseguente aumento dei costi attivi del progetto. 
- performance inadeguate dovute ad una progettazione non ottimale degli Agent AI, che potrebbe portare a tempi di risposta più lunghi e a un'esperienza utente insoddisfacente.

# Obiettivo

Con questo articolo condividerò un esercizio eseguito con lo scopo di provare alcuni _agent design pattern_.
L'esercizio si basa su un piccolo software d'esempio chiamato **Agentic TotChef**, che si pone come obiettivo la generazione 
di un menù settimanale per una bambina di 1 anno tenendo conto di ciò che mangia all'asilo nido, dal ricettario di famiglia e da ciò che è disponibile in casa.

L'esercizio mi ha aiutato a capire limiti e vantaggi tra cui:
- L'utlizzo di SLM (Small Language Model) in modo da contenere i costi ed ottenere risultati soddisfacenti
- L'adozione di design pattern e best pratice per progettare agenti AI con un buon grado di performance

# Small Language Model: limiti e vantaggi

Se è vero che i grandi modelli linguistici (LLM) come GPT-5, Gemini, Claude, Grok e simili offrono capacità straordinarie, 
è altrettanto vero che i Small Language Model (SLM) stanno guadagnando terreno grazie alla loro efficienza e costi ridotti.

I SLM, come quelli offerti da Ollama, sono progettati per essere più leggeri e meno costosi, rendendoli ideali per applicazioni specifiche 
che non richiedono la potenza di un LLM completo.

Tra i vantaggi:
- **Costi ridotti**: I SLM sono generalmente più economici da utilizzare rispetto agli LLM, rendendoli accessibili anche per progetti con budget limitati.
- **Efficienza**: I SLM possono essere più veloci nel generare risposte, soprattutto quando si tratta di compiti specifici che non richiedono una comprensione profonda del contesto.
- **Personalizzazione**: Con l'aggiunta di un contesto specifico è possibile ottenere risultati più pertinenti e accurati, sfruttando al meglio le capacità del SLM.

Tuttavia, è importante riconoscere i limiti dei SLM, come la capacità di comprendere contesti complessi o di generare risposte creative.
Quindi la scelta tra LLM e SLM dipende dalle esigenze specifiche del progetto e dagli obiettivi che si vogliono raggiungere.

Nel mio caso, per il progetto TotChef, ho optato per **qwen3-8b**, che si è dimostrato sufficiente per generare menù settimanali accurati e pertinenti.
Ovviamente parliamo di requisiti di complessità medio-bassi e hardware limitato. 
In ogni caso quanto basta per arrivare ad un risultato soddisfacente con tempi di risposta accettabili.

# Agentic Design Patterns: un approccio per progettare agenti AI scalabili e manutenibili



# TotChef: Architettura software

![Agentic TotChefArchitecture](../../totchef-arch.png)

# Conclusioni
