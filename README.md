# Pfadiralala-IV
[![Build Status](https://travis-ci.org/vcp-kurhessen/Pfadiralala-IV.svg?branch=master)](https://travis-ci.org/vcp-kurhessen/Pfadiralala-IV)

Das ''Pfadiralala IV'' und ''Pfadiralala IVplus'' sind Liederbücher der Region Kurhessen im Verband Christlicher Pfadfinderinnen und Pfadfinder. Es ist ausschließlich zum internen Gebrauch von den Mitgliedern der Region bestimmt und wird nur an diese ausgegeben. Das Liederbuch stellt daher keine Veröffentlichung im Sinne des Pressegesetzes dar. Alle Rechte an den Melodien, Texten und Zeichnungen liegen bei den Autoren. 

## Datei-Struktur

- **basic-design.tex**: Konfiguration der verwendeten Pakete.
- **Grifftabelle\*.tex**: Grifftabellen für verschiedene Saiteninstrumente.
- **PfadiralalaIV.tex**: Definition des Liederbuchs (Lieder und Reihenfolgen).
- **PfadiralalaIVplus.tex**: Definition des Ergänzungsbuchs *Pfadiralala IVplus*.
- **Tutorial.tex**: Beispiel-Song mit den am häufigsten verwendeten Kommandos. 

## Anforderungen

Folgende Software wird zum bauen der Bücher verwendet bzw. benötigt:

- `make`: [https://www.gnu.org/software/make/]()
- `abcm2ps`: [http://moinejf.free.fr]()
- `pdflatex` + verschiedene Pakete, z.B. TexLive: [https://www.tug.org/texlive/]()
- `ps2pdf`: [https://ghostscript.com/doc/current/Ps2pdf.htm]()
- `pdfcrop`: [https://ctan.org/pkg/pdfcrop]()
- `songidx`: [http://songs.sourceforge.net]() (Versionen für macOS (64-bit) und Linux (32- und 64-bit) liegen im Repo)
- `sed`: [https://www.gnu.org/software/sed/]() (Wichtig: es werden Features aus gnu-sed verwendet, auf *BSD muss gsed explizit installiert werden.) 

## LaTeX kompilieren / Makefile

Im Makefile sind verschiedene build targets für die Bücher definiert, die verschiedene Versionen des gleichen Buches erzeugen.

Um die einfachen (bilderlosen) Versionen zu erzeugen, genügt ein simpler Aufruf:

```
make
``` 

- **PfadiralalaIV{plus}.pdf**: Draft version des Liederbuchs
- **PfadiralalaIV{plus}-pics.pdf**: Version des Liederbuchs mit Bildern
- **PfadiralalaIV{plus}.pdf**: Version des Liederbuchs mit Bildern und Schnittrand
- **clean**: Löscht alle temporären Dateien und Liederbuch PDFs
- **PDFs**: Sucht in den Lieder* Ordnern nach dem Dateinamen und erzeugt ein PDF im Ordner PDFs

### Kompilieren mit Docker

##### Vorbereitung
Um die Tools zum kompilieren nicht selbst auf dem System installieren zu müssen, kann auch Docker zum kompilieren verwendet werden. Zunächst muss das Image entweder heruntergeladen oder gebaut werden: 

```bash
# Image herunterladen
docker pull hoechst/pfadiralala
```
oder

```bash
# Image selbst bauen
docker build -t hoechst/pfadiralala Tools/.
```

##### Mit Docker kompilieren
Um das Buch mit Hilfe des Docker images zu bauen, kann entweder docker oder docker-compose verwendet werden:

```bash
# Build mit Docker und manuellem mount
docker run --rm -it -v "$PWD:/PfadiralalaIV" hoechst/pfadiralala make
```

```bash
# Build mit docker und expliziter Angabe der Quelldaten
docker run --rm -it -v "$PWD:/PfadiralalaIV" hoechst/pfadiralala make
```

```bash
# Build mit docker-compose und ohne weitere notwendige Parameter
docker-compose run latex make
```