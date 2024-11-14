# Tutorial: Come correlare due tabelle con PowerQuery

## Scenario:

* Hai due tabelle:

    * Tabella Clienti (che contiene informazioni sui clienti come nome, email, etc.)
    * Tabella Ordini (che contiene informazioni sugli ordini, come prodotto, quantità, data ordine, e l'ID cliente che corrisponde a quello nella tabella clienti).

* L'obiettivo è unire queste due tabelle, utilizzando l'ID Cliente come colonna comune.

## Passo 1: Caricare le tabelle in PowerQuery

* Apri Excel e carica le due tabelle in PowerQuery:
   * Se le tabelle sono già nel tuo foglio Excel, seleziona qualsiasi cella della tabella.
   * Vai alla scheda Dati di Excel, quindi clicca su Da tabella/Intervallo.
   * Nella finestra che appare, assicurati che l'opzione "La tabella ha intestazioni" sia selezionata e clicca su OK. Questo aprirà la tabella in PowerQuery.

Fai lo stesso per entrambe le tabelle (Tabella Clienti e Tabella Ordini).

## Passo 2: Correlare le tabelle (Unire)

* Nella finestra PowerQuery, dopo aver caricato la prima tabella (ad esempio "Clienti"), vai alla scheda Home.
* Clicca su Aggiungi Colonne e poi su Unisci Query.
* Verrà visualizzata una finestra di dialogo con l’elenco delle tabelle caricate. Seleziona la seconda tabella che desideri correlare (ad esempio, "Ordini").
* Nella seconda tabella, seleziona la colonna che corrisponde alla colonna dell'altra tabella (ad esempio, l'ID Cliente in entrambe le tabelle).
* Scegli il tipo di unione:
   * Inner Join: Mostra solo i dati che esistono in entrambe le tabelle (una corrispondenza perfetta tra le colonne).
   * Left Join: Mostra tutti i dati dalla prima tabella (Clienti) e quelli corrispondenti dalla seconda tabella (Ordini). I dati che non hanno corrispondenza nella seconda tabella verranno riempiti con valori nulli.
   * Right Join: Mostra tutti i dati dalla seconda tabella e quelli corrispondenti dalla prima tabella.
   * Full Outer Join: Mostra tutti i dati da entrambe le tabelle, con i valori mancanti riempiti da nulli.
   * (Per esempio, se desideri visualizzare tutti i clienti, anche quelli senza ordini, puoi scegliere Left Join.)
 * Clicca su OK per applicare l'unione. La tabella risultante avrà una nuova colonna che contiene una tabella interna con i dati della seconda tabella (Ordini) per ogni riga della prima tabella (Clienti).

## Passo 3: Espandere i dati uniti

Ora che le tabelle sono state correlate, la nuova colonna contiene tabelle annidate che includono i dati della seconda tabella. Devi espandere questi dati per ottenere tutte le informazioni nella stessa tabella.

* Nella colonna appena aggiunta (quella contenente la tabella annidata), vedrai un piccolo icona a forma di quadrato con due frecce (in alto a destra della colonna). Clicca su questa icona.
* Seleziona le colonne che desideri espandere dalla seconda tabella (ad esempio, Prodotto, Quantità, Data_Ordine).
* Puoi scegliere di rinominare le colonne durante questa fase, se necessario (ad esempio, potresti voler cambiare il nome di "Quantità" in "Quantità Ordine").
* Clicca su OK.

La tua tabella ora dovrebbe apparire con tutte le informazioni correlate provenienti dalle due tabelle, disposte in una struttura unica.

## Passo 4: Pulizia e formattazione dei dati
* Rimuovi le colonne non necessarie. Ad esempio, se la colonna dell'ID Cliente è presente in entrambe le tabelle e non è più necessaria, puoi rimuoverla.
* Clicca con il tasto destro sulla colonna da rimuovere e scegli Rimuovi.
* Modifica i tipi di dati, se necessario. Ad esempio, se la colonna "Data Ordine" è stata caricata come testo, dovrai cambiarne il tipo in Data.
* Seleziona la colonna, poi clicca su Tipo di dati nella barra superiore e scegli il tipo appropriato (es. Data, Numero, Testo).
* Aggiungi eventuali calcoli. Se desideri calcolare il totale dell'ordine, ad esempio, puoi aggiungere una colonna personalizzata che moltiplica la quantità per il prezzo unitario. Vai su Aggiungi Colonna > Colonna Personalizzata e inserisci la formula che ti serve.

## Passo 5: Caricare i dati in Excel
Una volta che le tue tabelle sono state correlate, e i dati sono pronti, clicca su Chiudi & Carica per caricare i dati trasformati in un nuovo foglio di lavoro Excel.

Ora, puoi utilizzare questi dati per analisi, creare grafici, o anche utilizzarli in un modello di Power BI se necessario.

Esempio pratico (Tabella Clienti + Tabella Ordini)
Tabella Clienti:
| ID_Cliente | Nome_Cliente   | Email               |
|------------|----------------|---------------------|
| 1          | Mario Rossi    | mario@email.com     |
| 2          | Lucia Bianchi  | lucia@email.com     |
| 3          | Marco Verdi    | marco@email.com     |

Tabella Ordini:
| ID_Ordine | ID_Cliente | Prodotto  | Quantità | Data_Ordine |
|-----------|------------|-----------|----------|-------------|
| 1001      | 1          | Laptop    | 1        | 2024-10-01  |
| 1002      | 2          | Monitor   | 2        | 2024-10-03  |
| 1003      | 3          | Mouse     | 1        | 2024-10-05  |

Tabella risultante dopo l'unione (Left Join):

| ID_Cliente | Nome_Cliente   | Email             | ID_Ordine | Prodotto  | Quantità | Data_Ordine |
|------------|----------------|-------------------|-----------|-----------|----------|-------------|
| 1          | Mario Rossi    | mario@email.com   | 1001      | Laptop    | 1        | 2024-10-01  |
| 2          | Lucia Bianchi  | lucia@email.com   | 1002      | Monitor   | 2        | 2024-10-03  |
| 3          | Marco Verdi    | marco@email.com   | 1003      | Mouse     | 1        | 2024-10-05  |

## Conclusione

Questo processo ti permette di correlare facilmente due tabelle in PowerQuery, unendo i dati basati su una colonna comune (come un ID Cliente o ID Ordine). Puoi applicare diverse trasformazioni, espandere i dati e fare calcoli personalizzati per ottenere una vista unificata dei tuoi dati. Con PowerQuery, il processo di integrazione e preparazione dei dati diventa molto più semplice e automatizzabile.

Se hai domande o bisogno di ulteriori chiarimenti su qualsiasi passaggio, fammi sapere!
