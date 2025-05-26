# Projektarbeit

Dieses Repository enthält eine gemeinsame Jupyter-Notebook-Datei (`projektdatei.ipynb`), an der 3 Entwickler parallel arbeiten. Für eine reibungslose Zusammenarbeit gelten folgende verbindliche Regeln:

## Arbeitsweise mit Git und GitHub

### 1. Haupt-Branch (`main`)
- `main` enthält stets die **freigegebene und funktionierende Version** der Datei.
- Direkte Commits und Pushes in `main` sind **nicht erlaubt**.

### 2. Persönliche Feature-Branches
- Jeder Entwickler arbeitet ausschließlich in seinem eigenen Branch, z. B.:  
  - `projektarbeit/AhmedHossamMido`  
- Änderungen werden dort vorgenommen, committet und gepusht.

### 3. Bearbeitung der Datei
- Arbeite immer nur an einem klar abgegrenzten Abschnitt der Notebook-Datei.
- Vor der Bearbeitung: den aktuellen Stand von `main` in den eigenen Branch integrieren (`rebase` oder `merge`).
- Nach der Bearbeitung: Änderungen mit einer **aussagekräftigen Commit-Nachricht** speichern.

### 4. Pull Requests (PR)
- Änderungen aus Feature-Branches werden ausschließlich über **Pull Requests** in `main` integriert.
- Jeder PR muss:  
  - einen klaren Titel und eine Beschreibung enthalten,  
  - von mindestens einer weiteren Person überprüft werden,  
  - und nach erfolgreichem Review **ohne Konflikte gemerged** werden.

### 5. Konfliktvermeidung
- Vermeidet gleichzeitige Arbeit am selben Abschnitt des Notebooks.
- Vor jeder neuen Bearbeitung den eigenen Branch mit `main` synchronisieren.
- Merge-Konflikte sind im Team zu klären und sauber aufzulösen.

### 6. Kommunikation
- Änderungen und Absprachen werden über Issues, Pull-Request-Kommentare oder ein externes Kommunikationsmittel koordiniert.
- Wichtige Entscheidungen sind im Repository zu dokumentieren.

### 7. Regeln zum Schutz von `main`
- Direkte Änderungen am `main`-Branch sind ausnahmslos verboten.
- Alle Änderungen müssen per Pull Request erfolgen.
- Jeder Pull Request, der in `main` gemerged wird, benötigt die Genehmigung von **drei** Personen.

---

Diese Struktur gewährleistet, dass alle Änderungen nachvollziehbar, geprüft und sauber integriert werden, für ein stabiles und kooperatives Projekt.
