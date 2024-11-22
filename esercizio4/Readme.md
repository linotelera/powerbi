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
1. Unisci la tabella `Vendite` con `Prodotti`:
   - Usa una **Join** sulla colonna `Prodotto`.
   - Aggiungi le colonna `Categoria` e `Prezzo Unitario` alla tabella `Vendite`.
   - Rinomina le categorie generate in Categoria e Prezzo Unitario
   
2. Nella tabella `Vendite`:
   - Modifica il tipo di dati delle colonne `Data`, `Quantità` e `Fatturato`.
   - Aggiungi una colonna calcolata per il margine:
     ```
     Margine (%) = (Fatturato - (Quantità * [Prezzo Unitario])) / Fatturato * 100
     ```



## Step 2: Concetto di OLAP e Simulazione in Power BI

Un cubo OLAP (Online Analytical Processing) consente l’analisi multidimensionale dei dati. Un cubo contiene:
- **Dimensioni**: contesto dei dati (es. Tempo, Prodotto, Negozio).
- **Misure**: valori aggregati calcolati (es. Fatturato, Quantità, Margine).

Se non hai accesso a un cubo OLAP, puoi creare una **simulazione OLAP** direttamente in Power BI utilizzando i tuoi dati. In questa sezione, configureremo un modello dati che emula le funzionalità di un cubo OLAP.

---

### 2.1 Creazione di una Simulazione OLAP

1. **Importa i dati**
   - Segui i passaggi dello Step 1 per importare i file CSV `Vendite` e `Prodotti`.

2. **Crea relazioni tra le tabelle**
   - Vai alla scheda **Modello** nella barra laterale di Power BI.
   - Collega:
     - La colonna `Prodotto` di `Vendite` con la colonna `Prodotto` di `Prodotti`.
   - Assicurati che la relazione sia **1-Molti**.

3. **Crea gerarchie di dimensione**
   - Per la dimensione "Tempo", crea colonne derivate da `Data` nella tabella `Vendite`:
     - `Anno = YEAR(Vendite[Data])`
     - `Mese = FORMAT(Vendite[Data], "MMMM")`
     - `Giorno = DAY(Vendite[Data])`
   - Clicca con il tasto destro su `Data` > **Nuova gerarchia** > aggiungi `Anno`, `Mese` e `Giorno`.

4. **Definisci misure calcolate**
   - Vai su **Home** > **Nuova misura** e crea le seguenti misure:
     - Fatturato Totale:
       ```DAX
       Fatturato Totale = SUM(Vendite[Fatturato])
       ```
     - Margine Medio:
       ```DAX
       Margine Medio = AVERAGE(Vendite[Margine])
       ```
   - Le misure calcolate consentono di analizzare i dati su più dimensioni.

---

### 2.2 Utilizzo del Modello Dati in Power BI

Una volta configurato il modello dati:

1. **Analisi multidimensionale**
   - Usa le dimensioni per filtrare o esplorare i dati.
   - Esempi:
     - Analizza il Fatturato per `Negozio` e `Categoria di prodotto`.
     - Mostra le Quantità vendute per `Anno` e `Mese`.

2. **Visualizzazioni**
   - Crea un **grafico a barre** con:
     - Asse X: `Categoria`
     - Valore: `Fatturato Totale`.
   - Aggiungi un **grafico a linee** per l’andamento temporale:
     - Asse X: `Mese`
     - Valore: `Fatturato Totale`.

---

### 2.3 Simulazione di Drill-Down

1. **Drill-down sui grafici**
   - Aggiungi un grafico a barre con:
     - Asse X: Gerarchia `Data` con Anno, Mese e Giorno
     - Valore: `Fatturato Totale`.
   - Abilita il drill-down cliccando sull’icona della freccia nel grafico.
   - Clicca su una barra per scendere al livello successivo (es. da `Anno` a `Mese`).

2. **Filtro interattivo con slicer**
   - Aggiungi uno slicer (Filtro Dati) al report.
   - Usa `Negozio` o `Categoria` per filtrare i dati.

---

### Prossimi Passi

Questo approccio simula molte funzionalità OLAP senza SQL Server Analysis Services. Se hai accesso a un vero cubo OLAP:
- Segui i passaggi originali per collegarti al servizio SQL.
- Combina le dimensioni e le misure del cubo con i tuoi dati locali per un’analisi avanzata.


