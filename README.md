# Metric-based Analysis to Identify Anomalous Releases in the npm Ecosystem Software Supply Chain

LaTeX sources of my Master's Thesis in **Computer Science – Security and Software Engineering**, University of Genoa (DIBRIS), defended in July 2026.

- **Author:** Michele Frattini
- **Advisors:** Luca Caviglione, Giovanni Lagorio
- **Examiner:** Matteo Dell'Amico

📄 The compiled thesis is available at [`main.pdf`](main.pdf).

---

## 🇬🇧 Abstract

The Open-Source Software ecosystem relies heavily on package managers such as **npm**, which hosts over two million libraries. However, its open nature makes it vulnerable to Software Supply Chain Attacks (SSCAs), where malicious code is injected into legitimate components. Existing detection tools share two limitations: they analyze only the most recent release, lacking a longitudinal perspective, and incur high operational costs through sandbox execution or commercial LLM inference.

This thesis proposes a metric-based approach to identify anomalous npm releases by tracking their evolution across versions. It first studies four SSCAs that affected the npm ecosystem in 2025 — a malicious Windows DLL injection, a cryptocurrency-stealing attack, and two self-propagating *Shai-Hulud* worm variants — and derives five metrics:

1. **File Types**
2. **Package Size**
3. **Longest Line Length**
4. **Unique Hexadecimal Values**
5. **Unique Ethereum Addresses**

The metrics are evaluated against a goodware baseline of 629 popular packages (their 20 most recent versions) and a malware collection of 20 compromised releases. Results show that each attack is detectable by at least one metric, but no single one identifies all four simultaneously, highlighting the value of combining lightweight measures as a practical complement to semantically rich approaches.

## 🇮🇹 Abstract

L'ecosistema Open Source si affida in larga parte a package manager come **npm**, che ospita oltre due milioni di librerie. La sua natura aperta lo rende però vulnerabile ai *Software Supply Chain Attack* (SSCA), in cui codice malevolo viene iniettato in pacchetti legittimi. Gli strumenti di rilevamento esistenti condividono due limiti: analizzano solo la release più recente, senza una prospettiva longitudinale, e comportano costi operativi elevati (sandbox execution o inferenza con LLM commerciali).

Questa tesi propone un approccio basato su metriche per identificare release npm anomale, seguendone l'evoluzione tra versioni successive. Vengono analizzati quattro SSCA che hanno colpito l'ecosistema npm nel 2025 (un'iniezione di DLL malevola per Windows, un attacco crypto-stealer e due varianti del worm *Shai-Hulud*), da cui vengono derivate cinque metriche (elencate sopra). Le metriche sono valutate su una baseline "goodware" di 629 pacchetti popolari (20 versioni più recenti) e su un dataset "malware" di 20 release compromesse. I risultati mostrano che ogni attacco è rilevabile da almeno una metrica, ma nessuna metrica singola li rileva tutti e quattro, evidenziando il valore della combinazione di misure leggere come complemento pratico ad approcci semanticamente più ricchi.

---

## Repository structure

```
.
├── main.tex                     # Main document, includes all chapters
├── preamble.tex                 # Package configuration and document style
├── acronyms.tex                 # List of acronyms used in the thesis
├── abstract.tex
├── introduction.tex             # Ch. 1 - Introduction
├── background.tex               # Ch. 2 - Background
├── related.tex                  # Ch. 3 - Related Work
├── Attacks/                      # Ch. 4 - Analysis of Recent Attacks (Attack A-D)
├── ExperimentalSetup/           # Ch. 5 - Experimental Setup (datasets and tool)
├── metrics/                      # Ch. 6 - Metrics Analysis (one subfolder per metric)
├── conclusion.tex               # Ch. 7 - Conclusion
├── Acknowledgements.tex
├── bib.bib                       # Bibliography (biblatex)
├── masterthesis.cls              # DIBRIS official LaTeX template (Computer Science)
├── masterthesis_ceng.cls         # Template variant for Computer Engineering
└── main.pdf                      # Compiled thesis
```

## Companion tools & datasets

The experimental pipeline behind Chapters 5 and 6 is split across three companion repositories:

- 🔎 **[npm-packages-analyzer](https://github.com/Frazzerz/npm-packages-analyzer)** — the core Python tool that computes the five metrics. It fetches npm package releases, extracts their tarballs, and analyzes each file — using, among others, [Magika](https://github.com/google/magika) for file-type classification and [tree-sitter](https://tree-sitter.github.io/tree-sitter/) for stripping code comments — to build the goodware and malware datasets.
- 📥 **[Download-malicious-npm-packages](https://github.com/Frazzerz/Download-malicious-npm-packages)** — a script that retrieves the tarballs of compromised, already-unpublished npm releases by querying mirror registries (e.g. Huaweicloud, Taobao, Tencent), which often keep a copy for a while after the upstream removal. Its output feeds `npm-packages-analyzer` via the `--local` flag to build the malware dataset.
- 📊 **[Datasets-npm-Analysis](https://github.com/Frazzerz/Datasets-npm-Analysis)** — the goodware (629 popular packages, 20 versions each) and malware (20 compromised releases) datasets produced with the two tools above, used for all the analyses in Chapter 6.
