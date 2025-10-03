# Utilizzare Web Services ISTAT in Power Query

In questo tutorial vedremo come recuperare i dati di popolazione da un Web Service pubblico di ISTAT utilizzando Power Query.

---

## Prerequisiti
1. **Excel o Power BI Desktop** installati sul tuo computer.
2. Accesso a Internet per interrogare il web service.

---

## Obiettivo
Il nostro obiettivo è recuperare i dati della popolazione per comune e regione attraverso il web service ISTAT e trasformarli in una tabella utilizzabile in Power Query.

---

## URL del Web Service
Per questo esempio, utilizzeremo il seguente endpoint:

https://raw.githubusercontent.com/linotelera/powerbi/refs/heads/main/esercizio1/ordini.json

Questo endpoint restituisce i dati in formato JSON.

---

## Codice M per Power Query

Copia e incolla il seguente codice **M** in Power Query per recuperare e trasformare i dati:

```m
let
    // URL del Web Service ISTAT
    url = "https://raw.githubusercontent.com/linotelera/powerbi/refs/heads/main/esercizio1/ordini.json",

    // Recupera i dati dal web service
    WebServiceResponse = Web.Contents(url),

    // Decodifica la risposta JSON
    JsonResponse = Json.Document(WebServiceResponse),

    // Converte i dati JSON in una tabella
    DatiTabella = Table.FromList(JsonResponse, Splitter.SplitByNothing(), {"Data"}, null, ExtraValues.Error),

    // Espande i dettagli dei comuni e delle regioni
    EspandiDati = Table.ExpandRecordColumn(DatiTabella, "Data", {"CodiceComune", "Comune", "Regione", "PopolazioneTotale"}),

    // Rinomina le colonne per chiarezza
    RinominaColonne = Table.RenameColumns(EspandiDati, {
        {"CodiceComune", "Codice Comune"},
        {"Comune", "Nome Comune"},
        {"Regione", "Nome Regione"},
        {"PopolazioneTotale", "Popolazione Totale"}
    }),

    // Rimuove righe vuote o non valide
    FiltraDatiValidi = Table.SelectRows(RinominaColonne, each [Popolazione Totale] <> null)
in
    FiltraDatiValidi
```

## Istruzioni Dettagliate per Usare il Codice

### 1. Aprire Power Query
#### In Excel:
1. Vai nella barra multifunzione e clicca su **Dati**.
2. Scegli **Recupera e Trasforma Dati** > **Da Altre Origini** > **Query Vuota**.

#### In Power BI Desktop:
1. Vai su **Home**.
2. Clicca su **Editor di Query** > **Nuova Sorgente** > **Query Vuota**.

---

### 2. Incollare il Codice
1. Nella finestra di Power Query, clicca su **Visualizza Avanzata** (in alto a sinistra).
2. Cancella il codice preesistente e incolla il codice **M** fornito in questo tutorial.
3. Premi **OK** per confermare.

---

### 3. Trasformare i Dati
Dopo aver eseguito il codice:
- Vedrai una tabella con colonne come **Codice Comune**, **Nome Comune**, **Nome Regione** e **Popolazione Totale**.
- Se necessario, puoi applicare trasformazioni aggiuntive (es. filtri o calcoli personalizzati).

---

### 4. Caricare i Dati
#### In Excel:
1. Clicca su **Chiudi e Carica** nella barra multifunzione.
2. I dati verranno caricati in un nuovo foglio di lavoro.

#### In Power BI Desktop:
1. Clicca su **Chiudi e Applica**.
2. I dati verranno caricati nel modello di dati di Power BI.

---

## Risultato Atteso
La tabella risultante avrà un aspetto simile a questo:

| Codice Comune | Nome Comune  | Nome Regione | Popolazione Totale |
|---------------|--------------|--------------|---------------------|
| 010001        | Comune A     | Regione X    | 1000               |
| 010002        | Comune B     | Regione X    | 2000               |

---

## Suggerimenti
- Puoi modificare il codice per filtrare i dati di una regione o comune specifico.
- Puoi aggiungere calcoli personalizzati, come la densità di popolazione o il confronto tra comuni.
- Combina questi dati con altre fonti per analisi avanzate.

---

Se hai bisogno di ulteriori dettagli o vuoi esplorare altri web services ISTAT, fammi sapere! 😊
