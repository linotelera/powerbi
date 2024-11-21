# Tutorial Power BI: Workflow dai Dati al Report usando un Cubo OLAP e CSV

In questo tutorial creeremo un report Power BI che analizza il fatturato di una catena di supermercati. Il workflow partirà dall'importazione di dati CSV, passerà per l'integrazione con un cubo OLAP e terminerà con la creazione di un report interattivo.

## Prerequisiti
- **Power BI Desktop** installato.
- File CSV contenenti i dati delle vendite e dei prodotti.
- Accesso a un database SQL Server con un cubo OLAP.

---

## Step 1: Importazione e preparazione dei dati

### 1.1 Importa i dati da file CSV
1. Apri **Power BI Desktop**.
2. Clicca su **Ottieni dati** > **Testo/CSV**.
3. Seleziona i seguenti file CSV:
   - **Vendite.csv**:
     | Data       | Negozio       | Prodotto       | Quantità | Fatturato |
     |------------|---------------|----------------|----------|-----------|
     | 2024-01-01 | Supermercato A | Latte Intero   | 10       | 15.00     |
     | 2024-01-01 | Supermercato B | Pane Integrale | 20       | 30.00     |
     | 2024-01-02 | Supermercato A | Caffè Espresso | 5        | 25.00     |
   - **Prodotti.csv**:
     | Prodotto       | Categoria       | Prezzo Unitario |
     |----------------|-----------------|-----------------|
     | Latte Intero   | Latticini      | 1.50            |
     | Pane Integrale | Panificati     | 1.50            |
     | Caffè Espresso | Bevande        | 5.00            |

4. Clicca su **Trasforma dati** per aprire Power Query.

---

### 1.2 Trasforma i dati
1. Nella tabella `Vendite`:
   - Modifica il tipo di dati delle colonne `Data`, `Quantità` e `Fatturato`.
   - Aggiungi una colonna calcolata per il margine:
     ```
     Margine (%) = (Fatturato - (Quantità * [Prezzo Unitario])) / Fatturato * 100
     ```

2. Unisci la tabella `Vendite` con `Prodotti`:
   - Usa una **Join** sulla colonna `Prodotto`.
   - Aggiungi la colonna `Categoria` alla tabella `Vendite`.

---

## Step 2: Connessione al cubo OLAP
1. Torna alla schermata principale di Power BI.
2. Vai su **Ottieni dati** > **SQL Server Analysis Services**.
3. Seleziona il cubo OLAP con dimensioni e misure, ad esempio:
   - **Dimensioni**: `Tempo`, `Negozio`, `Categoria`.
   - **Misure**: `Fatturato`, `Quantità venduta`, `Margine`.

4. Integra i dati dal cubo con i file CSV utilizzando le relazioni:
   - Collega la dimensione `Prodotto` con il campo omonimo nella tabella `Vendite`.

---

## Step 3: Creazione del report

### 3.1 Visualizzazioni
1. Aggiungi una **tabella** che mostri:
   - Colonne: `Negozio`, `Mese`, `Fatturato`, `Quantità`, `Margine (%)`.
2. Inserisci un **grafico a barre** per confrontare il fatturato per categoria di prodotto.
3. Usa un **grafico a linee** per mostrare l'andamento temporale del fatturato.

### 3.2 Slicer e interattività
1. Aggiungi uno **slicer** per filtrare i dati per `Categoria` o `Anno`.
2. Configura il drill-through per analizzare i dettagli per negozio o prodotto.

---

### 3.3 Pubblicazione
1. Clicca su **File** > **Pubblica** per caricare il report su Power BI Service.
2. Condividi il report con i membri del team o crea una dashboard aziendale.

---

## Risultati Finali
Al termine, avrai un report che:
- Analizza il fatturato per negozio e categoria di prodotto.
- Mostra l'andamento temporale e la distribuzione dei margini.
- Permette di esplorare i dati in modo interattivo con slicer e drill-through.

---

## Esempio di Visualizzazioni
- **Tabella**: Fatturato e margine per negozio e mese.
- **Grafico a barre**: Fatturato per categoria di prodotto.
- **Grafico a linee**: Andamento temporale del fatturato.

---

## Prossimi Passi
- Automatizza l'aggiornamento dei file CSV con Power BI Service.
- Espandi il report per includere analisi di inventario o previsioni di vendita.
- Integra ulteriori fonti dati, come API o fogli Google.
