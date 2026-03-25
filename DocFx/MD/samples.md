# Samples

## No More Utils Folder
Diversamente da Astra RPG Framework, in questo package non troverete una cartella `Utils` tra i vari samples. Ho preso questa decisione perche' ritengo che sia piu' saggio e robusto lasciare che siate voi crearvi le vostre istanze. Questo perche' se costruite il vostro progetto attorno alle istanze che vi fornisco nei samples, e poi decidete di importare una nuova versione del package e reimportare i samples, rischiate di fare confusione su quali istanze di quale versione state attualmente usando per il vostro progetto. Lasciandovi creare a voi tutte le istanze degli oggetti del framework questa problematica viene completamente evitata.  
Inoltre, le istanze presenti nei samples della scena di esempio sono marchiati con un suffisso `(Astra Health Samples)` che li rende facilmente identificabili e distinguibili da eventuali istanze che potreste creare voi per il vostro progetto.

Se volete prendere ispirazione dalle istanze presenti nei samples, potete farlo tranquillamente, ma vi consiglio di creare nuove istanze per il vostro progetto, in modo da evitare qualsiasi confusione futura.

## Examples Folder - Overview
All'interno della cartella `Examples` troverete una scena di esempio: e' il vostro sandbox per provare le funzionalita' di Astra RPG Health. Rispetto a quella minimale di Astra RPG Framework, questa scena ha piu' contenuti e funzionalita' da esplorare.
La scena copre tutte le funzionalita' principali di Astra RPG Health:
- Health System
- Damage Types
- Damage Sources
- Damage Reduction
- Defense Penetration
- Healing System
- Heal and Damage Modifiers
- Passive Regeneration
- Resurrection System
- Event System
- Health Scaling Component
- Experience Collection System

### The Scene - Overview
![Screenshot of the sample scene](../images/AstraRPG/samples/scene-overview.png)  
_Sample scene as you enter in play mode_

Se aprite e avviate la scena di esempio, vedrete un combattente stilizzato sulla sinistra (Duelist) e un manichino sulla destra (Dummy). Senza troppe sorprese, potrete scatenare l'ira del vostro personaggio contro il povero manichino al fine di testare le funzionalita' di Astra RPG Health.
Prima di prendercela con il manichino, diamo un'occhiata al resto della scena. Sopra il duelist c'e' un pannello contenente il nome del personaggio, il livello, l'eventuale classe, l'health bar, e infine i valori delle statistiche del personaggio. Un analogo pannello e' presente sopra il manichino. Potete scorrere con la rotellina del mouse su questi pannelli per visualizzare tutte le statistiche. Noterete che a differenza della scena di esempio di Astra RPG Framework, in questa scena i pannelli non mostrano gli attributi. Questo perche' ho volontariamente escluso il loro utilizzo in questa scena, al fine di concentrarci sulle funzionalita' di Astra RPG Health. Se avessi incluso anche gli attributi, sarebbe stato piu' complesso ragionare ragionare sull'effetto delle formule di calcolo del danno, delle riduzioni, delle penetrazioni e cosi' via, dal momento che i valori delle statistiche sarebbero stati influenzati anche dagli attributi. Quindi, per semplicitá, in questa scena di esempio dovrete concentrarvi solo sulle statistiche.

Oltre ai pannelli delle statistiche, noterete che sono presenti anche dei pulsanti con una o due icone alla loro sinistra. Questi rappresentano le abilita' che ogni personaggio puo' utilizzare. E si', anche il dummy in questo caso ha voce in capitolo e puo' vendicarsi dei sopprusi subiti nei vari videogiochi negli ultimi decenni.  
Ogni personaggio ha 3 abilita'; ogni riga di icona/e + 2 pulsanti costituisce una abilita' a se'. Per ciascuna abilita', il primo pulsante ne contiene il nome ed e' il punto d'attivazione. Il pulsante alla sua destra e' un toggle che definisce se l'abilita' effettuera' un colpo critico o meno. Infine, l'icona, o le icone, alla sinistra del nome dell'abilita' rappresentano i tipi di danno che i vari effetti dell'abilita' possono infliggere, o una cura se l'effetto dell'abilita' e' di guarigione. Una singola icona significa che l'abilita' ha un singolo effetto, mentre due icone indicano che l'abilita' ha due o piu' effetti. Nel caso vi fossero, 3 o piu' effetti, solo le icone dei primi 2 effetti saranno mostrate.
Le icone che troverete saranno in tutto 4:
- Una spada arancione, che rappresenta il danno fisico
- Una fiamma viola, che rappresenta il danno magico
- Uno scudo bianco perforato, che rappresenta il danno puro
- Una croce verde, che rappresenta la guarigione

La spada, la fiamma e lo scudo perforato rappresentano quindi effetti di danno, e sono associate ai rispettivi damage types. La croce verde rappresenta invece un effetto di guarigione.

> [!WARNING]
> Ci tengo a specificare che l'implementazione data per le abilita' in questa scena di esempio e' semplicistica e non rappresenta un sistema di abilita' completo. Era necessario introdurre un ability system minimale per poter dimostrare le funzionalita' di Astra RPG Health, ma non considerate questa implementazione come un punto di riferimento per la creazione di un sistema di abilita' piu' complesso.  
> Sara' responsabilita' di un futuro package di estensione di Astra fornire un sistema di abilita' completo e flessibile. Per ora, considerate questa implementazione come un semplice strumento per testare le funzionalita' di Astra RPG Health.

Noterete inoltre che appena sopra la testa del duelist ci sono un paio di pulsanti, che recitano "\[D\] Next Hero" e "\[A\] Previous Hero". Questi pulsanti vi permettono di cambiare il vostro personaggio. Alternativamente ai pulsanti potete utilizzare i tasti D e A sulla tastiera. Oltre al duelist, che si focalizza su abilita' che arrecano danno fisico e di guarigione, ci sono altri 2 personaggi, ognuno con un focus diverso. Il secondo personaggio, l'Assassin, si focalizza su abilita' che arrecano danno fisico e puro, talvolta con scaling sulla salute del nemico. Il terzo personaggio, il Mage, si focalizza su abilita' che arrecano danno magico.

### The Hierarchy - Overview
Se date ora un'occhiata alla gerarchia della scena vedrete che, oltre gli oggetti principali di default, contiene:
- l'entita' dummy
- il canvas del dummy (pannello delle statistiche e pannello delle abilita')
- una sezione con le entita' dei tre personaggi giocabili (duelist, assassin e mage). Il duelist e' attivo all'avvio della scena, mentre gli altri due personaggi sono disattivati. Cambiando personaggio con i pulsanti "\[D\] Next Hero" e "\[A\] Previous Hero", ciclerete tra questi tre personaggi, attivandone uno alla volta e disattivando gli altri due.
- una sezione con i canvas dei tre personaggi giocabili (pannello delle statistiche e pannello delle abilita' per ciascun personaggio). Anche in questo caso, il canvas del duelist e' attivo all'avvio della scena, mentre gli altri due canvas sono disattivati.
- Un oggetto `HeroSelector`. Questo oggetto ha come figli i game object che rappresentano i pulsanti "\[D\] Next Hero" e "\[A\] Previous Hero".
- Un oggetto `PopupCanvas`, che contiene due sotto-oggetti: `DamagePopupManager` e `HealPopupManager`. Questi oggetti sono responsabili della creazione dei popup di danno e guarigione che appaiono sopra la testa dei personaggi quando subiscono danno o ricevono guarigione.

**Ciascuna entita' ha i componenti Astra `EntityCore`, `EntityClass`, `EntityStats`, e il nuovo `EntityHealth` nell'oggetto radicale.** Il manichino non possiede una classe. Questa scelta non e' per discriminare il nostro amico legnoso, ma semplicemente perche' semplifica il cambiamento delle statistiche del manichino al fine di agevolare il testing delle funzionalita' del package. In questo modo, se voleste cambiare l'Armor per vedere come cambia la riduzione del danno in real-time, non dovete andare ad operare attraverso la Growth Formula associata a quella statistica nella classe del manichino, ma potete semplicemente modificarne il valore attraverso `EntityStats`. Semplice ed efficace.

Ogni entita' (compreso il dummy) ha inoltre due sotto-oggetti: `Visuals` e `Skills`. Il primo contiene tutti gli oggetti responsabili della rappresentazione visiva del personaggio (sprite e health bar per il dummy, sprite e sprite dell'attacco per i personaggi del giocatore), mentre il secondo serve per specificare le abilita' del personaggio.

Gli oggetti relativi ai canvas delle entita' hanno invece i seguenti sotto-oggetti: un `HeroPanel` responsabile di mostrare il pannello con nome, livello, classe, health bar e statistiche del personaggio, e uno `SkillsPanel`, che contiene i pulsanti e le icone relativi alle abilita' del personaggio.

### The Project Files - Overview

Nell'esplorer delle risorse, nei samples del package, oltre la scena di esempio, avrete queste cartelle:
- **Art**: Contiene tutte le risorse artistiche utilizzate nella scena di esempio.
- **Instances**: Questa e' la cartella piu' importante, in quanto contiene tutte le istanze degli oggetti forniti da Astra RPG Health. Vi ritroverete a interagire molto con queste istanze per testare le funzionalita' del package, e potrete prendere ispirazione da esse per creare le vostre istanze personalizzate per il vostro progetto.
- **Prefabs**: Contiene i prefab di tutti gli oggetti presenti nella scena di esempio.
- **Resources**: Contiene l'istanza di configurazione di Astra RPG Health per la scena di esempio.
- **Scripts**: Contiene tutti gli script utilizzati nella scena di esempio.


> [!WARNING]
> Una nota in merito a `Resources`. Come spiegato in [Global Settings](./workflows/package-configuration.md#global-settings), Astra RPG Health utilizza un'istanza di `AstraRpgHealthConfigSO` per configurare le sue funzionalita' nel vostro progetto Unity. Questa specifica istanza fornita nei samples e' stata configurata per la scena di esempio. La scena funziona sin da subito perche la risorsa di configurazione, chiamandosi esattamente `Astra Rpg Health Config`, viene automaticamente caricata da Astra RPG Health all'import del package e assegnata nella configurazione globale del package.
>
> Quando andrete a creare la vostra istanza `AstraRpgHealthConfigSO` di configurazione per il vostro progetto, dovrete assegnarla manualmente alla configurazione globale di Astra RPG Health, come spiegato in [Project Settings](./workflows/package-configuration.md#project-settings) attraverso le project settings, o in alternativa, come spiegato in [Manual Configuration](./workflows/package-configuration.md#manual-configuration-alternative-to-project-settings), assegnandola direttamente all'istanza `AstraRpgHealthGlobalSettings` presente nella cartella `Assets/Resources` (questa cartella resources e' collocata radicalmente negli Assets, non nei samples del package).
>
> Se non assegnate la vostra istanza di configurazione alla configurazione globale di Astra RPG Health, il package continuera' ad utilizzare la configurazione dei samples, creando confusione e potenziali problemi di configurazione.

### Instances Folder
Ora ci concentreremo sulla cartella `Instances`, che e' quella piu' rilevante per voi.

#### Spare objects: Default Damage Calculation Strategy and Lifesteal Config
Partiamo da due oggetti sfusi: `Default Damage Calculation Strategy` e `Lifesteal Config`. Il primo rappresenta la [strategia di calcolo del danno](./workflows/damage.md#damage-calculation-strategy) utilizzata di default nella scena. Il secondo rappresenta la [configurazione del lifesteal](./workflows/lifesteal.md#lifesteal-config); tutti i tipi di danno utilizzano la stessa stat `Lifesteal` per il calcolo del lifesteal.

#### Statistics and Stat Sets
Nella cartella `Stats` trovate tutte le istanze delle `Stat` e degli `StatSet` utilizzati nella scena di esempio. Potete esplorare voi nel dettaglio le statistiche e gli stat set, l'unica cosa che sottolineo e' che l'`Hero Stat Set` e' lo stat set utilizzato da tutti e 4 i personaggi della scena di esempio (duelist, assassin, mage e dummy).

#### Classes
Nella sottocartella `Classes` trovate tutte le classi per i 3 personaggi giocabili e tutte le relative growth formula che definiscono la progressione delle loro statistiche. C'e' anche una cartella `Common` che contiene alcune utilita' condivise da piu' classi. Ad esempio, la `200% Const Critical Multiplier GF` e' una growth formula che restituisce un moltiplicatore di 200% per i colpi critici a tutti i livelli. Solitamente un gioco utilizza un moltiplicatore fisso per tutte le entita' a tutti i livelli, quindi non ha senso duplicare questa growth formula in ogni classe, ma e' piu' efficiente creare un'unica istanza singola e condividerla tra tutte le classi che ne hanno bisogno.

#### Damage Sources
Nella sottocartella `Damage Sources` trovate tutte due damage sources: `Skill` e `Environmental`. La scena non fa uso di danni ambientali, ma la damage source e' utilizzata nella [Experience Collection](./workflows/experience-collection.md), in particolare nella strategia `Environmental Kill Exp Strategy`. Quindi, sebbene non sia testabile nella scena, ha valore di esempio per mostrarvi come creare e configurare una strategia multipla che usa sia la direct kill che la environmental kill strategies.

#### Damage Types
Nella sottocartella `Damage Types` trovate i tre tipi di danno utilizzati nella scena di esempio: Physical, Magical e True, e due cartelle contenenti le tre varianti di Damage Reduction Functions e Defense Reduction Functions. Attualmente, sia physical che magical damage utilizzano la formula logaritmica per la riduzione del danno sulla base della statistica difensiva, e la riduzione percentuale per la penetrazione della statistica difensiva. Le ho fornite tutte e tre per agevolarvi il testing qualora voleste sostituire le formule al volo.

#### Events
In `Events` invece trovate tutte le istanze degli eventi di gioco utilizzate dalla scena di esempio. Tutte le istanze appartengono ad Astra RPG Health eccetto per `Entity Leveled Up Game Event` e `Entity Leveled Down Game Event`.
Questi eventi sono stati collegati come [global events](./workflows/package-configuration.md#global-events) nella configurazione `AstraRpgHealthConfigSO`.

Tutte le comunicazioni tra i vari oggetti della scena di esempio vengono gestite attraverso questi eventi.

#### Experience Collection
Nella cartella `Experience Collection` ci sono tutte le istanze e le strategie utilizzate per la raccolta dell'esperienza nella scena di esempio. Come menzionato in precedenza, la scena di esempio non prevede l'utilizzo di danni ambientali, ma ho comunque incluso una strategia `Environmental Kill Exp Strategy` per mostrarvi come creare e configurare una strategia multipla che utilizza sia la direct kill che la environmental kill strategies.

#### Heal Sources
A differenza delle damage sources, nella scena di esempio vengono usate tutte e 4 le `HealSourceSO` che trovate nella cartella `Heal Sources`:
- `HP Regeneration`: utilizzata dagli eventi di rigenerazione passiva della salute
- `Lifesteal`: utilizzata dagli effetti di lifesteal
- `Resurrection`: utilizzata dalla cura applicata alla resurrezione di un'entita'
- `Skill`: utilizzata dalle abilita' che hanno effetti di guarigione

#### Game Actions
In `Game Actions` trovate `On Death Game Actions` e `On Resurrection Game Actions`. Queste sono utilizzate per definire il comportamento delle entita' in risposta alla loro morte e resurrezione rispettivamente. Tratteremo meglio questo argomento piu' tardi in questa pagina.

#### Skills
Infine, nella cartella `Skills` trovate tutte le istanze delle abilita' utilizzate nella scena di esempio, suddivise per personaggio. Ogni abilita' ha una propria istanza di `SkillSO`, e una `ScalingFormula` con uno o piu' `ScalingComponent` associati. Alcune abilita', come menzionato prima, possono avere piu' di un effetto. In tal caso, hanno una scaling formula per ogni effetto.

#### Passives
Nella cartella `Passives` trovate le istanze di oggetti necessari per il funzionamento delle abilita' passive implementate per la scena di esempio. Vedremo le abilita' passive piu' avanti in [Implementing Custom Passive Abilities](#implementig-custom-passive-abilities).

## Interacting with the Scene
Ora che abbiamo esplorato la scena di esempio, la gerarchia e i file di progetto, vi do alcune informazioni su alcune configurazioni specifiche che meritano due parole in piu'.

### Casting Skills to Deal Damage and Heal
Le skill della sample scene si possono riassumere, dal punto di vista tecnico, come dei costruttori di `PreDamageContext` e `PreHealContext` che instradano questi contesti verso le entita' bersaglio. Il bersaglio processerà questi contesti nei suoi metodi `heal` e `TakeDamage`. Il calcolo dei danni che avviene all'interno di `TakeDamage`, come abbiamo visto nei workflows, passa attraverso la pipeline del calcolo del danno. La pipeline usa la strategia che è stata configurata a livello di configurazione `AstraRPGHealthConfigSO`.  
Quando l'entità viene curata o subisce danni, invocherà i rispettivi Global Events configurati anch'essi nella configurazione del package. E gli heal e damage pop-up managers che trovate nella hierarchy sono in ascolto di questi due eventi rispettivamente. Quando ricevono l'evento, creano un pop-up sopra la testa del personaggio bersaglio che mostra l'ammontare di danno subito o guarigione ricevuta. I pop up del danno avranno colori e icone diverse in base al tipo di danno inferto. Le icone (e il colore) combaceranno con quelle che vedete alla sinistra dell'abilità che avete lanciato.

![Casting Skills](../images/AstraRPG/samples/casting-skills.gif)  
_Casting Skills and Damage and Heal Pop-Ups_

Se andate in hover sopra un pulsante di un'abilita', vedrete comparire un tooltip che mostra una descrizione dell'abilita'. Se tenete premuto il tasto `Alt` mentre il tooltip e' visibile, vedrete comparire i dettagli dello scaling dei vari effetti dell'abilita'. Queste descrizioni dovrebbero aiutarvi a prevedere l'ordine di grandezza dei danni e delle cure che i vari effetti dell'abilita' possono infliggere, e a capire come il level up dei personaggi influenzino la potenza delle loro abilita'.

![Tooltip]()  
_Collapsed tooltip_

![Tooltip with details]()
_Expanded tooltip with details_

Se premete sul pulsante "Don't crit", il testo cambiera' in "Do crit", e l'abilita' che lancerete da quel momento in poi infliggera' un colpo critico. Il pop-up di un danno critico ha un icona personalizzata in alto a destra, e appare cosi:  
![Critical Hit Pop-Up](../images/AstraRPG/samples/critical-hit-pop-up.png)

### Messing Around with Damage Types and Damage Calculation Strategy
Qui potete sbizzarrirvi e giocare con varie impostazioni per cambiare radicalmente il modo in cui il danno viene calcolato. Partiamo con l'osservare la configurazione dei tipi di danno:
| Damage Type | Defensive Stat | Damage Reduction Function | Defense Penetration Stat | Defense Penetration Function | Flat Damage Modifier Stat | Percentage Damage Modifier Stat | Ignores Barrier | Ignores Generic Perc. Dmg Modifiers | Ignores Generic Flat Dmg Modifiers |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Physical | Armor | Logarithmic DR | Armor Penetration | Percentage DP | Physical Flat Dmg Mod | Physical Percentage Dmg Mod | ✘ | ✘ | ✘ |
| Magical | Magic Resist | Logarithmic DR | Magic Penetration | Percentage DP | Magical Flat Dmg Mod | Magical Percentage Dmg Mod | ✘ | ✘ | ✘ |
| True | None | None | None | None | None | None | ✔ | ✔ | ✔ |

Potete notare che il danno fisico e magico utilizzano entrambi la stessa formula logaritmica per la riduzione del danno e la stessa per la penetrazione della difesa, ma chiaramente utilizzano statistiche diverse per la riduzione e penetrazione. Il true damage invece non ha nessuna statistica difensiva associata, quindi non subisce nessuna riduzione. Non avendo statistiche difensive associate, non ha neanche penetrazione della difesa.  
Oltre alle statistiche difensive e alle relative formule di riduzione e penetrazione, danno fisico e magico definiscono anche delle statistiche per modificatori flat e percentuali per lo specifico tipo di danno. Rimando alla documentazione dei [Damage Type's Damage Modifiers](./workflows/damage.md#damage-types-damage-modifiers) per maggiori dettagli su come funzionano queste statistiche e su come vengono utilizzate nella pipeline del calcolo del danno. Potete testare l'impatto di queste statistiche modificando i loro valori nell'`EntityStats` del Dummy. **Ricordatevi inoltre che l'ordine di applicazione dei modificatori flat e percentuali è definito nella strategia di calcolo del danno configurata. Nella scena di esempio la trovate sotto `Examples/Instances/Default Damage Calculation Strategy`.** La sua configurazione iniziale e':
1. Apply Critical Multiplier
2. Apply Defenses
3. Apply Barrier
4. Apply Percentage Damage Modifiers
5. Apply Flat Damage Modifiers

Potete ovviamente riordinare questi step come preferite per vedere come cambia il risultato finale del danno in base all'ordine di applicazione degli step.

Per concludere le osservazioni sui tipi di danno, potete osservare che il true damage ignora sia i modificatori flat che quelli percentuali, oltre che la barrier. Questo significa che il danno, oltre a non venir ridotto, non puo' neanche venire amplificato. **L'unica meccanica che modifica il valore del true damage e' il moltiplicatore del critico.**

C'e' un'ultima cosa che merita due parole in merito a questo argomento, ed e' la configurazione delle statistiche per i flat e percentage damage modifiers (vale sia per quelli damage-type specific che per quelli generici). Le statistiche per i percentage damage modifiers sono configurate diversamente da quelle flat. Se aprite la statistica `Physical Dmg Perc Mod` nell'inspector, noterete infatti che ha minimum value di -100, mentre la statisticha `Physical Dmg Flat Mod` **non** ha un minimum value. Questo perche' una percentuale di modificatore del danno non puo' mai superare il -100% (completa negazione del danno), mentre un modificatore flat puo' teoricamente ridurre il danno di un qualsiasi valore.  
E' responsabilita' dello step dei flat damage modifiers nella pipeline del calcolo del danno assicurarsi che il danno finale non scenda sotto lo zero a causa di un flat damage modifier che supera il valore del danno.  
Un'osservazione che potreste sollevare e' "E se un'entita' ha il generic damage percentage modifier a `-70`% e il damage-type specific percentage modifier a `-50`%? In questo caso, il danno subira' una riduzione totale del 120%, no?". Corretto! Tuttavia, come spiegato in [ApplyPercentageDmgModifiersStep](./workflows/damage.md#applypercentagedmgmodifiersstep), il costrutto usato internamente dalla pipeline del calcolo del danno limita inferiormente a 0 le trasformazioni del damage amount. Quindi, in questo caso, il danno finale sara' 0, e il danno verra' prevenuto con `DamagePreventionReason.PipelineReducedToZero`.  
Pertanto, anche se non impostaste un limite inferiore di -100% alle statistiche dei percentage damage modifiers, il sistema si assicurerebbe comunque che il danno non scenda sotto lo zero a causa di modificatori percentuali, tuttavia, e' piu' semanticamente corretto e piu' chiaro impostare un limite di -100% a queste statistiche. Questo sarebbe utile anche al momento della creazione di interfacce di gioco per la visualizzazione di queste statistiche, in quanto un giocatore potrebbe essere confuso nel vedere un modificatore del danno del -150%, non sapendo che in realta' il danno non puo' scendere sotto lo zero.

### Playing with Passive HP Regeneration
Nella scena di esempio la rigenerazione passiva della salute e' abilitata per tutti i personaggi, ma potete disabilitarla togliendo la spunta da `Passive Health Regeneration` nell'`EntityHealth` dell'entita' in questione. Di default inoltre verranno mostrati dei popup curativi per ogni tick di rigenerazione passiva. Se questi popup vi danno fastidio, potete disabilitarli in questo modo:
1. Dalla hierarchy aprite il game object `PopupCanvas`
2. Selezionate il game object `HealPopupManager`
3. Nell'inspector, nel componente `Heal Popup Manager`, espandete la sezione `Hea; Sources To Ignore` e premete il pulsante `+`. Trascinate qui la Heal Source `HP Regeneration HS` che trovate in `Examples/Instances/Heal Sources`.

In questo modo, il `Heal Popup Manager` ignorerà tutti gli eventi di guarigione che hanno come fonte di guarigione `HP Regeneration`, e quindi non creerà pop-up per i tick di rigenerazione passiva.

Gia' da questo semplice esempio risulta chiaro il valore di creare e utilizzare heal source differenti. Cure che provengono da meccaniche diverse possono sollevare casi d'uso diversi.

Ho configurato il tick rate della rigenerazione a 1 secondo. Se voleste invece cambiare il tick-rate della rigenerazione passiva, potete farlo modificando il valore `Passive HP Regeneration Interval` nell'istanza di configurazione `Astra Rpg Health Config` che trovate in `Examples/Resoures`. Rimando anche alla documentazione sulla [Package Configuration | Health Regeneration](./workflows/package-configuration.md#health-regeneration) e sulla [Healing | Passive Health Regeneration](./workflows/healing.md#passive-health-regeneration) per i dettagli.  

Per modificare la vita rigenerata passivamente, dovete modificare il valore della statistica `Passive Regeneration`. Per i tre personaggi giocabili, questa statistica e' controllata attraverso le Growth Formula associate alla rispettive classi, mentre per il Dummy potete modificarla direttamente attraverso `EntityStats`.

> [!WARNING]
> Ricordatevi che, come menzionato in [Passive Health Regeneration Stat (HP/10s)](./workflows/package-configuration.md#passive-health-regeneration-stat-hp10s) in Package Configuration, il valore di questa statistica rappresenta la quantita' di salute rigenerata ogni 10 secondi. Quindi, se volete che un personaggio rigeneri passivamente 5 HP al secondo, dovrete impostare il valore di `Passive Regeneration` a 50, non a 5.

### Health Scaling Component

### Death and Resurrection

### Experience Collection

### Implementig Custom Passive Abilities

Nonostante questo package non si occupa di definire costrutti di alto livello per le abilita' e le passive (e sara' responsabilita' di una futura estensione del framework farlo), e' comunque possibile implementare certe abilita' passive per i vostri personaggi in maniera semplice e veloce usando i costrutti di questo package e quello base. Di seguito alcuni esempi.

#### Passive Ability (Duelist) - Excellent Recovery
*Implementation difficulty: easy*

Il duelist ha un'abilita' passiva che aumenta la rigenerazione passiva della salute del 400% al livello 10, e del 1000% al livello 20.

L'implementazione di questa abilita' e' molto semplice: ho creato una GrowthFormula specifica per il Duelist per la statistica `Passive Reg Heal Perc Mod`, ovvero la statistica che rappresenta il modificatore percentuale alla rigenerazione passiva della salute che e' stata assegnata alla Heal Source `HP Regeneration`. La growth formula restituisce un valore di 0% fino al livello 9, un valore di 400% dal livello 10 al livello 19, e un valore di 1000% dal livello 20 in poi.

#### Passive Ability (Assassin) - Vengence In Death
*Implementation difficulty: medium*

L'assassin ha un'abilita' passiva che fa si che quando subisce un danno fatale, contrattacca il nemico infliggendogli l'80% dei danni letali ricevuti come danno fisico. Questo danno e' un colpo critico garantito.

L'implementazione di questa abilita' e' leggermente piu' complessa della precedente. Per ottenere l'effetto descritto possiamo ricorrere alla [`CounterDamageOnDeathGameActionSO`](./workflows/game-actions.md#counterdamageondeathgameactionso) fornita dal package. Questa Game Action, prende in input un parametro di tipo `entityDiedContext`, lo stesso contesto che viene passato dagli eventi di morte. Pertanto attraverso un `EntityDiedGameEventListener` possiamo intercettare la morte di un'entita', e lanciare questa Game Action passando il contesto di morte intercettato. La Game Action utilizza il `DamageResolutionContext` contenuto nel contesto di morte per risalire all'ammontare di danno che ha causato la morte dell'entita', e infligge un danno pari all'80% di questo ammontare al colpevole del danno letale (moltiplicato per il moltiplicatore del critico dell'Assassin).  
Tuttavia c'e' un problema, noi non vogliamo attivare la Game Action alla morte di una qualunque entita', ma solo alla morte dell'Assassin. Qui entrano in gioco gli [Extra Events](./workflows/entity-health.md#extra-events). Possiamo creare un `EntityDiedGameEvent` specifico per comunicare la morte dell'Assassin soltanto, e assegnarlo nell'`EntityHealth` dell'Assassin come `Extra Death Event`. In questo modo, quando l'Assassin muore, oltre a lanciare il `Entity Died Game Event` globale, lancerà anche questo evento extra specifico. Quindi, invece di ascoltare il `Entity Died Game Event` globale con il nostro `EntityDiedGameEventListener`, ascolteremo questo evento extra specifico per l'Assassin. In questo modo, la nostra Game Action verrà attivata solo quando muore l'Assassin, e non alla morte di altre entita'.

#### Passive Ability (Sorcerer) - Glass Cannon
*Implementation difficulty: medium*
Lo sorcerer ha un'abilita' passiva che aumenta del 75% il moltiplicatore dei colpi critici, ma ogni volta che subisce danno subisce anche il 15% del suo Magic Power come danno magico extra.

L'implementazione di questa abilita' e' un po' l'unione delle due precedenti. Per aumentare il moltiplicatore dei colpi critici, basta creare una Growth Formula specifica per il Sorcerer per la statistica `Critical Multiplier`, che restituisce un valore di 275% a tutti i livelli. Per quanto riguarda il secondo effetto, ovvero subire danno magico extra pari al 15% del Magic Power ogni volta che subisce danno, possiamo ricorrere sempre alla `CounterDamageOnDeathGameActionSO` per infliggere danno magico extra ogni volta che il Sorcerer subisce danno. Tuttavia, a differenza dell'Assassin, vogliamo che questa game action bersagli il Sorcerer anziche' chi ci ha inflitto danni. Per l'ammontare di danno, usiamo una `ScalingFormula` dedicata. Infine, anche in questo caso, non vogliamo che questa game action venga attivata ogni volta che un'entita' subisce danno, ma solo quando a subire danno e' lo Sorcerer. Anche in questo caso, possiamo ricorrere agli Extra Events. Ho creato un evento dedicato per comunicare quando lo Sorcerer subisce danno, e l'ho assegnato come `Extra Damage Taken Event` nell'`EntityHealth` dello Sorcerer.