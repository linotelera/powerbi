# Integrazione dei Dati ISTAT in Power BI

Questo tutorial guida all'importazione e visualizzazione dei dati ISTAT sulla popolazione residente utilizzando Power BI. Verranno utilizzati dataset pubblici disponibili su [demo.istat.it](https://demo.istat.it).

---

## 1. Scarica i Dati ISTAT
1. Accedi al portale [demo.istat.it](https://demo.istat.it).
2. Cerca il dataset relativo alla popolazione residente.
3. Esporta i dati in formato **CSV** o copia il link per il formato **JSON/API**.

---

## 2. Importa i Dati in Power BI
1. Apri Power BI Desktop.
2. Vai su **Ottieni dati** e scegli l'opzione corretta:
   - **Per file CSV**:
     - Seleziona il file dal computer.
     - Visualizza l'anteprima dei dati e clicca su **Carica**.
   - **Per file JSON/API**:
     - Seleziona **Web** e incolla il link JSON/API fornito da ISTAT.
     - Conferma e procedi al caricamento dei dati.

---

## 3. Pulizia e Trasformazione dei Dati
Utilizza Power Query per modificare e preparare i dati per l'analisi:
1. **Rimuovi colonne inutili**: Elimina i campi che non ti servono per il report.
2. **Raggruppa dati**: Somma la popolazione residente per ogni regione.
   - Esempio: Raggruppa per **Regione** e calcola la somma di **Popolazione Residente**.
3. **Filtra**: Isola solo i dati delle regioni o dei comuni che ti interessano.

### Esempio di Script Power Query:
```M
= Table.Group(
    Source, 
    {"Regione"}, 
    {{"Popolazione Totale", each List.Sum([Popolazione Residente]), type number}}
)
```

## 4. Creazione del Report

### Tabelle
1. Aggiungi una **visualizzazione tabella**.
2. Mostra le seguenti colonne:
   - Comune
   - Regione
   - Popolazione Residente
3. Ordina la tabella per **Popolazione Residente** in ordine decrescente.

### Mappe
1. Aggiungi una **visualizzazione mappa**:
   - **Campo di localizzazione**: Regione o Comune.
   - **Colore o Dimensione**: Valori di **Popolazione Residente**.
2. Configura la mappa per evidenziare le differenze territoriali.