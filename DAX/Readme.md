# Introduzione a DAX (Data Analysis Expressions) in Power BI

DAX (Data Analysis Expressions) è un linguaggio di formula usato in Power BI, Analysis Services e Power Pivot in Excel per creare calcoli personalizzati e misure. In questo tutorial introduttivo, esploreremo i concetti base e alcuni esempi pratici.

## Cos'è DAX?

DAX è un linguaggio di formule progettato per il calcolo e l'analisi dei dati in modelli tabulari. Con DAX puoi:

- Creare colonne calcolate.
- Creare misure.
- Filtrare e aggregare dati.
- Implementare logiche complesse nei tuoi report.

## Concetti Base

### 1. Colonne calcolate
Una colonna calcolata è una colonna aggiuntiva in una tabella, i cui valori sono calcolati da una formula DAX. Le colonne calcolate vengono calcolate a livello di riga.

**Esempio:** Creare una colonna che calcola il 20% di tasse su un valore.
```DAX
TaxAmount = Sales[Amount] * 0.2
```

### 2. Misure
Le misure sono formule dinamiche utilizzate per calcoli aggregati come somma, media o conteggio. A differenza delle colonne calcolate, le misure si calcolano solo quando sono necessarie.

**Esempio:** Calcolare il totale delle vendite.
```DAX
TotalSales = SUM(Sales[Amount])
```

### 3. Filtri
DAX offre funzioni per applicare filtri personalizzati. Una funzione comune è `CALCULATE`, che permette di modificare il contesto del filtro.

**Esempio:** Calcolare il totale delle vendite solo per il 2023.
```DAX
Sales2023 = CALCULATE(SUM(Sales[Amount]), Sales[Year] = 2023)
```

### 4. Funzioni di aggregazione
DAX include funzioni come `SUM`, `AVERAGE`, `MIN`, `MAX` e `COUNT` per lavorare con dati numerici.

**Esempio:** Calcolare la media delle vendite.
```DAX
AverageSales = AVERAGE(Sales[Amount])
```

### 5. Funzioni di logica
DAX supporta espressioni condizionali con funzioni come `IF` e `SWITCH`.

**Esempio:** Classificare i prodotti in base alle vendite.
```DAX
SalesCategory = IF(Sales[Amount] > 1000, "High", "Low")
```

### 6. Funzioni di tempo
Per analisi temporali, DAX offre funzioni come `DATEADD`, `TOTALYTD`, `PREVIOUSYEAR`, ecc.

**Esempio:** Calcolare il totale cumulativo delle vendite annuali.
```DAX
TotalYTD = TOTALYTD(SUM(Sales[Amount]), Calendar[Date])
```

## Best Practices

1. Usa nomi descrittivi per colonne e misure.
2. Evita calcoli complessi direttamente in tabelle visive; usa le misure.
3. Sperimenta il contesto di riga e filtro per capire come influiscono sui tuoi calcoli.
4. Utilizza la documentazione e le community per approfondire.

## Esempio Pratico

Supponiamo di avere una tabella `Sales` con le seguenti colonne:
- `Date`
- `Amount`
- `Year`

Creiamo una misura per calcolare il totale delle vendite e un'altra per calcolare il totale delle vendite dell'anno corrente.

**Misure:**
```DAX
TotalSales = SUM(Sales[Amount])
SalesCurrentYear = CALCULATE(SUM(Sales[Amount]), YEAR(Sales[Date]) = YEAR(TODAY()))
```

Questi calcoli possono essere utilizzati in una visualizzazione per mostrare il confronto tra il totale generale e quello dell'anno corrente.

---

## Risorse Utili

- [Documentazione ufficiale DAX](https://learn.microsoft.com/en-us/dax/)
- [Microsoft Learn - Introduzione a Power BI](https://learn.microsoft.com/en-us/training/powerbi/)
- [Guida alle funzioni DAX](https://learn.microsoft.com/en-us/dax/dax-function-reference)
- [Community Power BI](https://community.powerbi.com/)
- [Video tutorial su YouTube](https://www.youtube.com/results?search_query=dax+power+bi+tutorial)
- [DAX.Guide](https://dax.guide/) Referimento linguaggio DAX

