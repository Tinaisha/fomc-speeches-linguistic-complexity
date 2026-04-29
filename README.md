# General Notebook Pipelines
## 00_DataConstructions
- Start with fed_speeches_dataframe.csv (web‑scraped Board of Governors speeches).
- Clean text (remove “Return to text”, fix stuck words)
- Merge with imported Bpres dataset (2023–2025) 
- Merge with Campiglio et al. (2025) dataset. This needs manual download, links are included in the "Campiglioetal_2025" text note.
- Apply more cleaning: remove suspicious/long/noise tokens; remove URL‑like patterns, file extensions, PDF artifacts; remove high‑symbol‑density strings and alphanumeric junk.
- Compute textual characteristics 
- Handle missing William Poole speeches: identify missing items; compute textual features; and merge into main dataset

## 01_PreliminaryObservation
- Clean name formatting and duplicates
- Construct role variables (Board member, President, etc.)
- Create strain upper bounds
- Save as FedSpeechesCleaned.csv
- Produce descriptive statistics and preliminary plots

## 02_AddTimestampPC
- Merge FedSpeechesCleaned.csv with otherData/fomcspeak_archive.csv (data with timestamps)
- Compute principal components (PCs)
- Drop unused variables (including raw text)
- Save as FedSpeechesPC.csv

## 03_TopicModellingLDA & 04_WordCloud
- Add topic proportions using FedSpeecheswithMoreControl.csv (other files work, as long as the content and the key merge are unique)
- Generate word clouds for visualization

## 05_AddControlAndRegMain
- Merge macroeconomic data (FRED, ALFRED, Greenbook/Tealbook) to save as FedSpeecheswithMoreControl.csv
- Merge speaker background data
- Merge daily and intraday financial data
- Save intermediate file as FedSpeechesRegression.csv
- Apply additional transformations: condensed categorical variables; additional engineered features; topic proportions
- Final regression dataset → FedSpeechesRobust.csv
- All the main regression results are made here.

## 06_SampleRobustPowerBIData
- Load FedSpeechesRobust.csv
- Re‑run main regression specifications on subsamples
- Export Power BI‑ready datasets

## More Data Details:
A lot of the data sources are fully referenced in the report pdf: **FedSpeechesProject.pdf**. This is also the full report for this project. Here I listed the core:
- FOMC Speeches 1986–2025: Core dataset from Campiglio et al. (2025); Web‑scraped speeches from Federal Reserve Board and 12 Federal Reserve Banks websites; Archival speeches (e.g., William Poole 1998–2008) from FRASER
- Speaker Background Information: Compiled from: Federal Reserve Board biographies; Regional bank biographies; Conti‑Brown & Nygaard FRB Directors Database; Riboni & Ruge‑Murcia (2025) dataset. Variables include gender, race, degree major, terminal degree, pre‑Fed career, institutional role, saltwater/freshwater classification, age, and tenure.
- Daily Financial Market Data: Yahoo Finance API
- Intraday Financial Market Data (2010–2023): Bloomberg Terminal (15‑minute frequency). Restricted to 09:00–16:30 ET
- Speech timestamps from FRASER FOMC Speak Archive
- Macroeconomic Data: ALFRED; Greenbook/Tealbook (publicly accessible portions)

## Other notes and References:
Campiglio, E., Deyris, J., Romelli, D., & Scalisi, G. (2025). Warning words in a warming world: Central bank communication and climate change. European Economic Review, 178, 105101.

Riboni, A., & Ruge‑Murcia, F. (2025). Membership Turnover and Policy Disagreement at the FOMC. HAL Working Paper hal‑05229751.

Conti‑Brown, P., & Nygaard, K. (n.d.). Federal Reserve Bank Boards of Directors Biographical Database. Available at: https://www.contibrown.com/frb-directors-database

Federal Reserve Bank of St. Louis. (2024). FOMC Speak Archive. FRASER: Federal Reserve Archival System for Economic Research. https://fraser.stlouisfed.org/timeline/fomc-speak-archive

Yahoo Finance. (n.d.). Historical Market Data API. Retrieved from https://finance.yahoo.com/  

Bloomberg L.P. (n.d.). Bloomberg Terminal – Intraday Price and Volume Data. Accessed via institutional subscription

Federal Reserve Bank of St. Louis. (n.d.). ALFRED: Archival Federal Reserve Economic Data. https://alfred.stlouisfed.org/. Accessed using API key

Federal Reserve Bank of Philadelphia. (n.d.). Greenbook and Tealbook Real‑Time Data (Real‑Time Data Research Center). Retrieved from: https://www.philadelphiafed.org/surveys-and-data/real-time-data-research/greenbook  

Board of Governors of the Federal Reserve System. (n.d.). Speeches and Testimony. https://www.federalreserve.gov/newsevents/speeches.htm

Federal Reserve Banks (12 Districts). (n.d.). Public Speeches and Remarks by Bank Presidents.  
