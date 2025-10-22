# 📈 Analisi dell'Andamento degli Indici Azionari: S&P 500 vs EURO STOXX 50

> Progetto in Python (Pandas, NumPy, Matplotlib) per analizzare e confrontare l’andamento di **S&P 500** ed **EURO STOXX 50** su un orizzonte pluriennale: pulizia dati, rendimenti, volatilità e visualizzazioni.

---

## 🧭 Obiettivi

- Caricare e pulire serie storiche di S&P 500 ed EURO STOXX 50  
- Calcolare **rendimenti** (giornalieri, cumulati) e **statistiche** descrittive  
- Evidenziare periodi di **volatilità** e giornate a forte movimento  
- Confrontare l’evoluzione dei due indici con grafici chiari

---

## 🧰 Stack & Librerie

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

- **Pandas**: I/O, wrangling, time series  
- **NumPy**: calcoli numerici e trasformazioni  
- **Matplotlib (pyplot)**: grafici e visualizzazioni

---

## ▶️ Come eseguire

```bash
jupyter notebook "Progetto_2_(Pandas,_Numpy,_Matplotlib_pyplot).ipynb"
```

Esegui le celle in ordine dall’alto verso il basso.  
Assicurati che i file CSV siano nella cartella `data/` o aggiorna i percorsi nel notebook.

---

## 🧪 Dati attesi

- File CSV con almeno:
  - `Date` (formato data, es. `YYYY-MM-DD`)
  - `Close` (prezzo di chiusura)
- Frequenza: giornaliera (preferibile)
- Stesso range temporale o gestito via merge/allineamento date

---

## 🔍 Workflow dell’analisi

1. **Caricamento & Pulizia**
   - Parse delle date, ordinamento per data  
   - Gestione/riempimento dei valori mancanti  
   - Eventuale normalizzazione (es. rebase = 100)

2. **Feature Engineering**
   - Rendimenti giornalieri:  
     ```python
     df['return'] = df['Close'].pct_change()
     ```
   - Rendimenti cumulati (es. prodotto cumulativo di \(1+r\))  
   - Metriche riassuntive (media, std, var, min/max)

3. **Visualizzazioni**
   - Line chart dei prezzi/serie normalizzate  
   - Istogrammi della distribuzione dei rendimenti  
   - Confronti affiancati tra i due indici

4. **Lettura dei risultati**
   - Confronto di performance e volatilità  
   - Individuazione periodi “caldi” (crisi, rally, shock macro)

---

## 📊 Esempi di codice (estratti)

**Line chart storico (serie normalizzate):**
```python
base_sp = df_sp500['Close'] / df_sp500['Close'].iloc[0]
base_eu = df_stoxx['Close'] / df_stoxx['Close'].iloc[0]

plt.figure()
plt.plot(df_sp500['Date'], base_sp, label='S&P 500 (base=1)')
plt.plot(df_stoxx['Date'], base_eu, label='EURO STOXX 50 (base=1)')
plt.title('Confronto andamento normalizzato')
plt.xlabel('Data')
plt.ylabel('Indice normalizzato')
plt.legend()
plt.show()
```

**Rendimenti giornalieri e statistiche:**
```python
df_sp500['return'] = df_sp500['Close'].pct_change()
df_stoxx['return'] = df_stoxx['Close'].pct_change()

summary = pd.DataFrame({
    'mean_return': [df_sp500['return'].mean(), df_stoxx['return'].mean()],
    'std_return':  [df_sp500['return'].std(),  df_stoxx['return'].std()]
}, index=['S&P 500', 'EURO STOXX 50'])
print(summary)
```

**Istogramma rendimenti:**
```python
plt.figure()
df_sp500['return'].dropna().hist(bins=50, alpha=0.7)
plt.title('Distribuzione rendimenti giornalieri S&P 500')
plt.xlabel('Rendimento')
plt.ylabel('Frequenza')
plt.show()
```

---

## ✅ Risultati tipici (attesi)

- Andamenti di lungo periodo simili ma con **differenti intensità**  
- **Rendimenti medi** e **volatilità** non identici tra USA ed Europa  
- Giornate/periodi con movimenti estremi riconducibili a eventi macro

> I risultati effettivi dipendono dal periodo osservato e dalla qualità dei dati.

---

## 🔮 Estensioni possibili

- **Correlazione dinamica** (rolling correlation) tra indici  
- Indicatori tecnici (MA, RSI, volatilità storica annualizzata)  
- Aggregazioni mensili/trimestrali e analisi per regime di mercato  
- Dashboard interattiva (Streamlit/Plotly)  
- Integrazione API dati finanziari

---
