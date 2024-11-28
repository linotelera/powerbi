# Esempi Avanzati con Power Query e Tabelle Pivot in Power BI

Di seguito trovi una serie di esempi avanzati per sfruttare al meglio Power Query e le tabelle pivot in Power BI, utili per analisi sofisticate.

---

## Esempio 1: Unione di Tabelle e Creazione di Campi Personalizzati

### Scenario
Hai due tabelle, `Vendite` e `Promozioni`, e vuoi calcolare il fatturato netto considerando sconti promozionali.

### Step-by-step con Power Query:
1. **Importa le tabelle** `Vendite` e `Promozioni` in Power BI.
2. **Unisci le tabelle**:
   - Vai su **Trasforma Dati** > **Unisci Query**.
   - Collega `Vendite` e `Promozioni` sulla colonna `ID Prodotto`.
   - Scegli una **Join Esterna Sinistra** per mantenere tutte le vendite, anche quelle senza promozioni.
3. **Crea una colonna calcolata**:
   - Usa Power Query per aggiungere una colonna `Sconto Netto`:
     ```M
     if [Sconto] = null then 0 else [Fatturato] * [Sconto]
     ```
   - Aggiungi una nuova colonna per calcolare il **Fatturato Netto**:
     ```M
     [Fatturato] - [Sconto Netto]
     ```

### Analisi con Tabelle Pivot:
1. Inserisci una tabella pivot e seleziona:
   - **Righe**: `Prodotto`
   - **Valori**: `Fatturato Netto`, `Sconto Netto`.
2. Filtra i dati per promozioni attive o categorie di prodotti.

---

## Esempio 2: Normalizzazione dei Dati

### Scenario
La tua tabella `Vendite` include valori di `Fatturato` molto diversi per negozi di dimensioni differenti. Vuoi normalizzare i dati per confrontarli in modo equo.

### Step-by-step con Power Query:
1. **Aggiungi una media globale**:
   - Vai su **Trasforma Dati** > **Gruppo per**.
   - Raggruppa i dati per `Negozio` e calcola la **Media Fatturato**.
2. **Unisci i risultati alla tabella principale**:
   - Usa la funzione di merge per aggiungere il campo `Media Fatturato` alla tabella `Vendite`.
3. **Crea un campo normalizzato**:
   - Aggiungi una colonna calcolata:
     ```M
     [Fatturato] / [Media Fatturato]
     ```

### Analisi con Tabelle Pivot:
1. Usa la tabella normalizzata per confrontare negozi.
2. Crea un grafico che mostri il **Fatturato Normalizzato** per ciascun negozio.

---

## Esempio 3: Creazione di Indicatori KPI

### Scenario
Vuoi creare un KPI che indichi se un negozio ha raggiunto il suo obiettivo di vendita.

### Step-by-step con Power Query:
1. **Aggiungi una colonna obiettivo**:
   - Importa una tabella `Obiettivi` con il fatturato target per ogni negozio.
   - Unisci la tabella `Obiettivi` alla tabella `Vendite`.
2. **Calcola lo scostamento**:
   - Aggiungi una colonna calcolata:
     ```M
     [Fatturato] - [Obiettivo]
     ```

3. **Crea un indicatore visuale**:
   - Usa DAX per creare una misura KPI:
     ```DAX
     KPI Status = 
     IF(
       SUM(Vendite[Fatturato]) >= SUM(Obiettivi[Obiettivo]),
       "Raggiunto",
       "Non Raggiunto"
     )
     ```

### Analisi con Tabelle Pivot:
1. Crea una tabella pivot con:
   - **Righe**: `Negozio`.
   - **Valori**: `KPI Status` (come un campo calcolato).
2. Aggiungi una visualizzazione KPI per evidenziare i risultati.

---

## Esempio 4: Dati Temporalmente Aggregati

### Scenario
Vuoi analizzare il fatturato aggregato per trimestri e confrontarlo con l’anno precedente.

### Step-by-step con Power Query:
1. **Aggiungi colonne temporali**:
   - Usa Power Query per creare colonne `Anno` e `Trimestre` dalla data:
     ```M
     Year = Date.Year([Data])
     Quarter = "Q" & Number.RoundUp(Date.Month([Data])/3)
     ```

2. **Calcola il totale per trimestre**:
   - Raggruppa i dati per `Anno` e `Trimestre` e calcola la somma del `Fatturato`.

3. **Crea una colonna di confronto**:
   - Aggiungi una colonna per calcolare lo scostamento percentuale con l'anno precedente:
     ```M
     [Fatturato Attuale] / [Fatturato Precedente] - 1
     ```

### Analisi con Tabelle Pivot:
1. Inserisci una tabella pivot con:
   - **Righe**: `Anno`, `Trimestre`.
   - **Valori**: `Fatturato` e lo scostamento percentuale.
2. Usa un grafico a linee per visualizzare il trend trimestrale.

---

Questi esempi sfruttano le funzionalità avanzate di **Power Query** per preparare i dati e di **tabelle pivot** per costruire analisi potenti. Prova ad applicarli ai tuoi progetti per ottimizzare i risultati!
