---
title: "Agentic TotChef: Architetture software, Patterns, and Best Practices"
date: 2999-02-16T00:00:00+00:00
description: "L'articolo esplora l'architettura software, i design pattern e le best practice per progettare agenti AI scalabili e manutenibili, utilizzando un caso di studio chiamato 'TotChef' che genera menù settimanali per una bambina di 1 anno."
tags: [AI, GenAI, Agent, Ollama, Python]
---

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

Con questo articolo condividerò un esercizio eseguito con lo scopo di provare alcuni _agentic design pattern_.
L'esercizio si basa su un piccolo software d'esempio chiamato **[Agentic TotChef](https://github.com/org-carmelolg-private-labs/agentic-totchef)**, che si pone come obiettivo la generazione 
di un menù settimanale per una bambina di 1 anno tenendo conto di ciò che mangia all'asilo nido, dal ricettario di famiglia e da ciò che è disponibile in casa.

L'esercizio mi ha aiutato a capire limiti e vantaggi tra cui:
- L'utlizzo di SLM (Small Language Model) in modo da contenere i costi ed ottenere risultati soddisfacenti
- L'adozione di design pattern e best pratice per progettare agenti AI con un buon grado di performance

# Small Language Model: limiti e vantaggi

Se è vero che i grandi modelli linguistici (LLM) come GPT-5, Gemini, Claude, Grok e simili offrono capacità straordinarie, 
è altrettanto vero che i Small Language Model (SLM) stanno guadagnando terreno grazie alla loro efficienza e costi ridotti.

I SLM, come quelli offerti da Ollama, sono progettati per essere più leggeri e meno costosi, rendendoli ideali per applicazioni specifiche 
che non richiedono la potenza di un LLM di grandi dimensioni.

Tra i vantaggi:
- **Costi ridotti**: I SLM sono generalmente più economici da utilizzare rispetto agli LLM, rendendoli accessibili anche per progetti con budget limitati.
- **Efficienza**: I SLM possono essere più veloci nel generare risposte, soprattutto quando si tratta di compiti specifici che non richiedono una comprensione profonda del contesto.
- **Personalizzazione**: Con l'aggiunta di un contesto specifico è possibile ottenere risultati più pertinenti e accurati, sfruttando al meglio le capacità del SLM.

Tuttavia, è importante riconoscere i limiti dei SLM, come la capacità di comprendere contesti complessi o di generare risposte creative.
Quindi la scelta tra LLM e SLM dipende dalle esigenze specifiche del progetto e dagli obiettivi che si vogliono raggiungere.

Nel mio caso, per il progetto TotChef, ho optato per **qwen3-8b**, che si è dimostrato sufficiente per generare menù settimanali accurati e pertinenti.
Ovviamente parliamo di requisiti di complessità medio-bassi e hardware limitato. 
In ogni caso quanto basta per arrivare ad un risultato soddisfacente con tempi di risposta accettabili.

# Agentic Design Patterns: cosa sono

Durante una sessione di lettura intensiva mi sono imbattuto su un libro molto interessante: [Agentic Design Pattern di Antonio Gulli](https://search.worldcat.org/it/title/1547934185), Eng Director in Google. Il libro descrive una serie di design pattern per progettare agenti AI, con un focus particolare su come strutturare il flusso di lavoro degli agenti, gestire la memoria, e interagire con l'ambiente esterno.

Mentre lo leggevo il mio pensiero è andato subito alla [GoF](https://en.wikipedia.org/wiki/Design_Patterns) e alla loro idea di standardizzare la produzione di codice sorgente. In un certo senso, i design pattern di Agentic Design Pattern rappresentano un tentativo di standardizzare la progettazione di agenti AI, fornendo soluzioni collaudate a problemi comuni che si presentano durante lo sviluppo di agenti.

Sul mio progetto di esempio, [Agentic TotChef](https://github.com/org-carmelolg-private-labs/agentic-totchef), non avevo molta manovra per utilizzare più design pattern, ho messo in pratica i primi due:
- **Prompt Chaining**: questo pattern prevede la suddivisione di un compito complesso in una serie di passaggi più semplici, ognuno dei quali è gestito da un agente AI specifico.
- **Parallelization**: questo pattern prevede l'esecuzione di più agenti AI in parallelo per completare un compito, migliorando così le prestazioni e riducendo i tempi di risposta.

Per me è stato un gioco divertente, ma anche un modo per capire meglio i limiti e i vantaggi di questi design pattern, e come possono essere applicati in progetti reali per migliorare la manutenibilità degli agenti AI.


# Agentic TotChef: Architettura software

[Agentic TotChef](https://github.com/org-carmelolg-private-labs/agentic-totchef) è un giochino e l'ho sviluppato per diversi motivi:
- testare i design pattern di Agentic Design Pattern
- capire se con un SLM era possibile ottenere risultati soddisfacenti
- scrivere codice _boilerplate_ (quello che in immagine ha un colore di sfondo viola) per la progettazione di [OAIA - OrchestrAI Architecture](https://github.com/carmelolg/OAIA) un template da riutilizzare per progetti futuri.

{{< figure src="../totchef-arch.png" alt="Agentic TotChef Architecture">}}

![Agentic TotChef Architecture](https://github.com/carmelolg/it-is-worth-a-coke/blob/925a8ed5780db0abd3cb9e282680add8cfec3eea/content/posts/%5BAI%5D%20Agentic%20Flow%20Architecture/totchef-arch.png?raw=true)

La parte più interessante di questa piccolissima architettura software è il file **Runner**, descritto in dettaglio nel box verde a destra: qui sono rappresentate tutte le chiamate verso **qwen3-8b** e le interazioni tra i vari agenti.

In particolare, è possibile notare come il design pattern di **Prompt Chaining** sia stato utilizzato per suddividere il compito complesso di generare un menù settimanale in una serie di passaggi più semplici, ognuno dei quali è gestito da un agente AI specifico. 

Il design pattern di **Parallelization** è stato invece utilizzato per eseguire in parallelo due step non dipendenti tra loro:
- il recupero dei pasti della mensa scolastica e conseguente creazione di un menù dei pranzi dal lunedì al venerdì
- la creazione di un menù dei pasti serali per tutta la settimana e per tutto il weekend tenendo conto di ciò che è disponibile in casa e del ricettario di famiglia.

Mentre il primo mi ha consentito di arrivare ad un output sicuramente migliore rispetto ad un altro tipo di progettazione, il secondo mi ha permesso di aumentare lo speedup del processo di generazione del menù settimanale, riducendo i tempi di risposta e migliorando l'esperienza utente.

**Nota**: non ho menzionato la piccola applicazione web che permette di chattare con TotChef semplicemente perché non presenta particolari elementi di interesse dal punto di vista architetturale: si tratta solo di un’interfaccia utile a testare gli output degli agenti AI nei vari step.

# Agentic TotChef: snippet di codice

> In questo esempio di codice sorgente Python, ogni oggetto che definisce uno step (ad esempio `KindergartenMenuStep`) implementa un metodo `execute` che si occupa di eseguire lo step specifico, interagendo (tramite `LLMExecutor`) con _qwen3-8b_ e restituendo un oggetto `StepResult` che contiene l'output dello step e informazioni sul suo stato di esecuzione.

[Il codice completo lo trovate qui](https://github.com/org-carmelolg-private-labs/agentic-totchef/)

```python
# Step 1: Kindergarten menu
kg_step = KindergartenMenuStep()
kg_step_output: StepResult = StepResult(step_id=kg_step.step_id, result="")
# Step 2: Home menu
home_step = HomeMenuStep()
home_step_output = StepResult(step_id=home_step.step_id, result="")

# Execute both steps in parallel
with ProcessPoolExecutor() as executor:
    futures = [
        executor.submit(kg_step.execute),
        executor.submit(home_step.execute)
    ]

    for future in futures:
        single_result = future.result()
        if single_result is not None and single_result.is_success():
            if single_result.step_id == kg_step.step_id:
                kg_step_output: StepResult = single_result
            elif single_result.step_id == home_step.step_id:
                home_step_output: StepResult = single_result

# Step 3: Merge menus
merge_step = MergeMenuStep()
merge_step_output: StepResult = merge_step.execute(kg_step_output.result, home_step_output.result)

# Step 4: Shopping list
shopping_list_step = ShoppingListStep()
shopping_list_output: StepResult = shopping_list_step.execute(merge_step_output.result)

# Add step that create a Markdown file with the merged menu and shopping list
create_md_step = CreateMarkdownStep()
create_md_output: StepResult = create_md_step.execute(merge_step_output.result, shopping_list_output.result)
if create_md_output is not None and create_md_output.is_success():
    TotChef.log_element(f"Markdown created: {create_md_output.result}")
else:
    TotChef.log_element("Failed to create markdown file")
```

L'output sarà un file Markdown con il menù settimanale e la lista della spesa.

<details>
    <summary>Qui un esempio</summary>

    # Weekly Menu and Shopping List
    ## Menù

    | Day       | Lunch                                                                 | Dinner                                                                 |
    |-----------|------------------------------------------------------------------------|------------------------------------------------------------------------|
    | Monday    | First Course: Penne al ragù<br>Main Course: Omelette al forno<br>Side: Carote prezzemolate | First Course: Riso sugo e piselli<br>Main Course: Nasello con carote in padella<br>Side: Zucchine |
    | Tuesday   | First Course: Minestrina in brodo vegetale<br>Main Course: Spezzatino di tacchino in umido<br>Side: Purea di patate | First Course: Pasta al ragù<br>Main Course: Polpette di carne<br>Side: Fagiolini |
    | Wednesday | First Course: Passato di lenticchie con pasta<br>Main Course: Stracchino<br>Side: Costine all'olio | First Course: Pasta alla zucca<br>Main Course: Orata in friggitrice ad aria<br>Side: Costine |
    | Thursday  | First Course: Risotto alla parmigiana<br>Main Course: Bocconcini di pollo alla pizzaiola<br>Side: Finocchi lessi | First Course: Pasta alla crema di ceci<br>Main Course: Philadelphia<br>Side: Verza |
    | Friday    | First Course: Farfalle al pomodoro<br>Main Course: Filetto di pesce al limone<br>Side: Broccoli all'olio | First Course: Pasta e patate<br>Main Course: Formaggio fresco<br>Side: Cavolo nero |
    | Saturday  | First Course: Pasta al pomodoro<br>Main Course: Polpette di ceci<br>Side: Zucchine | First Course: Riso sugo e piselli<br>Main Course: Ricotta fresca<br>Side: Spinaci |
    | Sunday    | First Course: Pasta al cavolo nero<br>Main Course: Frittata<br>Side: Fagiolini | First Course: Pasta alla crema di zucchine<br>Main Course: Orata in friggitrice ad aria<br>Side: Cavolfiore |

    ## Shopping List

    ### Fruits and Vegetables  
    - Carote: 1 kg  
    - Zucchine: 1 kg  
    - Fagiolini: 1 kg  
    - Broccoli: 1 kg  
    - Finocchi: 1 kg  
    - Cavolfiore: 1 kg  
    - Cavolo nero: 1 kg  
    - Spinaci: 1 kg  
    - Piselli: 1 kg  
    - Verza: 1 kg  
    - Patate: 1 kg  
    - Lenticchie: 1 kg  
    - Riso: 1 kg  
    - Cipolle: 1 kg  
    - Aglio: 1 kg  
    - Prezzemolo: 1 mazzetto  
    - Basilico: 1 mazzetto  
    - Timo: 1 mazzetto  
    - Zafferano: 1 cucchiaino  

    ### Proteins (Meat, Fish, Eggs, etc.)  
    - Manzo: 1 kg  
    - Tacchino: 1 kg  
    - Pollo: 1 kg  
    - Pesce (filetto): 1 kg  
    - Orata: 1 kg  
    - Uova: 12 pezzi  
    - Stracchino: 200 g  
    - Philadelphia: 200 g  
    - Formaggio fresco: 200 g  
    - Ricotta fresca: 200 g  
    - Bocconcini di pollo: 1 kg  

    ### Carbohydrates (Pasta, Rice, Bread, etc.)  
    - Penne: 500 g  
    - Farfalle: 500 g  
    - Pasta alla crema di ceci: 500 g  
    - Pasta alla zucca: 500 g  
    - Pasta al cavolo nero: 500 g  
    - Pasta alla crema di zucchine: 500 g  
    - Riso: 1 kg  
    - Pane: 1 kg  

    ### Lacteos (Milk, Cheese, Yogurt, etc.)  
    - Latte: 1 litro  
    - Yogurt greco: 1 litro  
    - Formaggio grattugiato: 100 g  
    - Burro: 100 g  

    ### Legumes  
    - Ceci: 500 g  
    - Lenticchie: 1 kg  
    - Fagioli: 500 g  

    ### Other (Oils, Spices, etc.)  
    - Olio d'oliva: 1 litro  
    - Sale: 1 kg  
    - Pepe nero: 100 g  
    - Zucchero: 1 kg  
    - Aceto balsamico: 100 ml  
    - Senape: 100 ml  
    - Panna: 200 ml  
    - Salsa di soia: 100 ml  
    - Vino bianco: 1 litro  
    - Olio per friggere: 500 ml  
    - Farina: 500 g  
    - Cioccolato fondente: 100 g  
    - Cacao in polvere: 100 g  
    - Caffè: 100 g  
    - Zucchero di canna: 1 kg  
    - Miele: 100 g
</details>

# Conclusioni
In questo articolo ho condiviso un esercizio dedicato alla sperimentazione di alcuni agentic design pattern utilizzando un SLM, qwen3-8b, per generare un menù settimanale adatto a una bambina di un anno.

L’esperimento mi ha permesso di individuare punti di forza e limiti di questi pattern, mostrando come possano essere adottati in contesti reali per aumentare la manutenibilità e la robustezza degli agenti AI.

In particolare, il design pattern di **Prompt Chaining** si è rivelato efficace per scomporre un compito complesso in una sequenza di passaggi più gestibili, ciascuno affidato a un agente specializzato. Il pattern di **Parallelization**, invece, ha consentito di eseguire in contemporanea due step indipendenti, migliorando le prestazioni e riducendo sensibilmente i tempi di risposta.

Lo _speedup_ ottenuto grazie a questa architettura è stato significativo (circa 1.5x per questo caso d’uso) considerando che solo i due step più onerosi vengono eseguiti in parallelo.
Le implementazioni precedenti, prive di una chiara separazione dei compiti e basate su agenti monolitici, hanno invece mostrato comportamenti indesiderati come loop infiniti e allucinazioni.

Per lo sviluppo di [Agentic TotChef](https://github.com/org-carmelolg-private-labs/agentic-totchef) ho utilizzato Python, ma gli agentic design pattern sono concetti agnostici rispetto al linguaggio e possono essere applicati a qualsiasi tipologia di agente o modello AI.

Questo progetto mi ha anche permesso di esplorare più a fondo il mondo del vibe-coding, grazie ai preziosi suggerimenti di **[@gregoriolagamba](https://gregoriolagamba.github.io/), Solution Architect in Plenitude**, che mi ha introdotto a strumenti di programmazione agentica direttamente su GitHub.