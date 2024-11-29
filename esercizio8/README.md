# Utilizzo di Append e Merge in Power Query

In questo esempio vedremo come combinare due tabelle utilizzando le funzioni **Aggiungi (Append)** e **Unisci (Merge)** in Power Query. L’obiettivo è:
1. Aggiungere i dati di due tabelle (`Vendite_T1` e `Vendite_T2`) per creare una tabella unica.
2. Unire questa tabella con un’altra tabella (`Prodotti`) per arricchire i dati con informazioni sui prodotti.

---

## 1. Dati di Esempio

### Tabella 1: Vendite_T1
| ID Vendita | ID Prodotto | Quantità | Data Vendita |
|------------|-------------|----------|--------------|
| 1          | 101         | 3        | 2024-01-15   |
| 2          | 102         | 5        | 2024-02-10   |

### Tabella 2: Vendite_T2
| ID Vendita | ID Prodotto | Quantità | Data Vendita |
|------------|-------------|----------|--------------|
| 3          | 103         | 2        | 2024-04-10   |
| 4          | 101         | 1        | 2024-05-01   |

### Tabella 3: Prodotti
| ID Prodotto | Nome Prodotto | Prezzo |
|-------------|---------------|--------|
| 101         | Prodotto A    | 20     |
| 102         | Prodotto B    | 30     |
| 103         | Prodotto C    | 25     |

---

## 2. Passaggi in Power Query

### **Passaggio 1: Aggiungi le Tabelle**
1. Carica le tabelle `Vendite_T1` e `Vendite_T2` in Power Query.
2. Vai nella scheda **Home** e seleziona **Aggiungi query** → **Aggiungi query come nuova**.
3. Nel dialogo:
   - Seleziona `Vendite_T1` come prima tabella.
   - Seleziona `Vendite_T2` come seconda tabella.
4. Clicca su **OK**. Si creerà una nuova tabella combinata chiamata `Vendite_Combinata` con i seguenti dati:

| ID Vendita | ID Prodotto | Quantità | Data Vendita |
|------------|-------------|----------|--------------|
| 1          | 101         | 3        | 2024-01-15   |
| 2          | 102         | 5        | 2024-02-10   |
| 3          | 103         | 2        | 2024-04-10   |
| 4          | 101         | 1        | 2024-05-01   |

---

### **Passaggio 2: Unisci le Tabelle**
1. Carica la tabella `Prodotti` in Power Query (se non è già caricata).
2. Seleziona la tabella `Vendite_Combinata`.
3. Vai nella scheda **Home** e seleziona **Unisci query**.
4. Nel dialogo:
   - Seleziona `Vendite_Combinata` come prima tabella.
   - Seleziona `Prodotti` come seconda tabella.
   - Crea la relazione sulla colonna `ID Prodotto` (chiave comune tra le tabelle).
5. Scegli il tipo di unione **Esterna Sinistra** (Left Outer Join) per includere tutte le righe di `Vendite_Combinata`.
6. Clicca su **OK**.
7. Espandi la nuova colonna aggiunta dalla tabella `Prodotti` e seleziona i campi `Nome Prodotto` e `Prezzo`. Il risultato sarà:

| ID Vendita | ID Prodotto | Quantità | Data Vendita | Nome Prodotto | Prezzo |
|------------|-------------|----------|--------------|---------------|--------|
| 1          | 101         | 3        | 2024-01-15   | Prodotto A    | 20     |
| 2          | 102         | 5        | 2024-02-10   | Prodotto B    | 30     |
| 3          | 103         | 2        | 2024-04-10   | Prodotto C    | 25     |
| 4          | 101         | 1        | 2024-05-01   | Prodotto A    | 20     |

---

## 3. Salvataggio dei Dati
1. Clicca su **Chiudi e carica** per applicare le modifiche e caricare i dati nel modello Power BI o in Excel.
2. Usa i dati combinati per creare visualizzazioni come tabelle, grafici o report personalizzati.

---

Questo esempio mostra come combinare e arricchire i dati in Power Query usando **Append** e **Merge**, rendendoli pronti per l’analisi e la visualizzazione.
