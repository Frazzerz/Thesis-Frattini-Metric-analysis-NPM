# Metric-based Analysis to Identify Anomalous Releases in the npm Ecosystem Software Supply Chain

Sorgenti LaTeX della mia tesi di laurea magistrale in **Computer Science – Security and Software Engineering**, Università di Genova (DIBRIS), discussa a maggio 2026.

- **Autore:** Michele Frattini
- **Relatori:** Luca Caviglione, Giovanni Lagorio
- **Correlatore:** Matteo Dell'Amico

📄 Il PDF compilato è disponibile in [`main.pdf`](main.pdf).

## Abstract

L'ecosistema Open Source si affida in larga parte a package manager come **npm**, che ospita oltre due milioni di librerie. La sua natura aperta lo rende però vulnerabile ai *Software Supply Chain Attack* (SSCA), in cui codice malevolo viene iniettato in pacchetti legittimi. Gli strumenti di rilevamento esistenti condividono due limiti: analizzano solo la release più recente, senza una prospettiva longitudinale, e comportano costi operativi elevati (sandbox execution o inferenza con LLM commerciali).

Questa tesi propone un approccio basato su metriche per identificare release npm anomale, seguendone l'evoluzione tra versioni successive. Vengono analizzati quattro SSCA che hanno colpito l'ecosistema npm nel 2025 (un'iniezione di DLL malevola per Windows, un attacco crypto-stealer e due varianti del worm *Shai-Hulud*), da cui vengono derivate cinque metriche:

1. **File Types**
2. **Package Size**
3. **Longest Line Length**
4. **Unique Hexadecimal Values**
5. **Unique Ethereum Addresses**

Le metriche sono valutate su una baseline "goodware" di 629 pacchetti popolari (sulle 20 versioni più recenti) e su un dataset "malware" di 20 release compromesse. I risultati mostrano che ogni attacco è rilevabile da almeno una metrica, ma nessuna metrica singola li rileva tutti e quattro, evidenziando il valore della combinazione di misure leggere come complemento pratico ad approcci semanticamente più ricchi.

## Struttura del repository

```
.
├── main.tex                     # Documento principale, include tutti i capitoli
├── preamble.tex                 # Configurazione pacchetti e stile del documento
├── acronyms.tex                 # Elenco degli acronimi usati nella tesi
├── abstract.tex
├── introduction.tex             # Cap. 1 - Introduction
├── background.tex               # Cap. 2 - Background
├── related.tex                  # Cap. 3 - Related Work
├── Attacks/                      # Cap. 4 - Analysis of Recent Attacks (Attack A-D)
├── ExperimentalSetup/           # Cap. 5 - Experimental Setup (dataset e tool)
├── metrics/                      # Cap. 6 - Metrics Analysis (una sottocartella per metrica)
├── conclusion.tex               # Cap. 7 - Conclusion
├── Acknowledgements.tex
├── bib.bib                       # Bibliografia (biblatex)
├── masterthesis.cls              # Classe LaTeX del template DIBRIS (Computer Science)
├── masterthesis_ceng.cls         # Variante del template per Computer Engineering
└── main.pdf                      # Tesi compilata
```

## Compilazione

Il documento usa la classe `masterthesis` (template ufficiale DIBRIS) e gestisce la bibliografia con **biblatex/biber**. Per compilare da sorgente:

```bash
latexmk -pdf main.tex
```

oppure manualmente:

```bash
pdflatex main.tex
biber main
pdflatex main.tex
pdflatex main.tex
```

> Per compilazioni rapide durante la stesura, è possibile passare l'opzione `[nocoverpage]` alla classe in `main.tex` per saltare il frontespizio.

Per la variante Computer Engineering del template, sostituire `\documentclass{masterthesis}` con `\documentclass{masterthesis_ceng}`.

## Strumento sviluppato

Le metriche descritte nel Capitolo 6 sono calcolate tramite un tool Python dedicato, **npm Packages Analyzer**, sviluppato per questa tesi e mantenuto in un repository separato:

👉 [github.com/Frazzerz/npm-packages-analyzer](https://github.com/Frazzerz/npm-packages-analyzer)

Il tool recupera le release di un pacchetto npm, ne estrae i tarball e calcola le cinque metriche (usando, tra gli altri, [Magika](https://github.com/google/magika) per la classificazione dei file e [tree-sitter](https://tree-sitter.github.io/tree-sitter/) per la rimozione dei commenti dal codice), producendo così i dataset "goodware" e "malware" usati nell'analisi.

## Licenza

Questo repository contiene materiale accademico (tesi di laurea magistrale). Se non diversamente specificato, i contenuti sono da intendersi a scopo di consultazione; per riutilizzo o citazione fare riferimento all'autore.
