# Wie erkennt man KI-generierte Texte? Eine quellenbasierte Bestandsaufnahme (Stand: August 2026)

**Methodik:** Diese Recherche startet beim Wikipedia-Kompendium *"Signs of AI writing"* und folgt von dort aus der zugrunde liegenden akademischen Literatur — Studien aus *Patterns*, *Nature*, NeurIPS, ICML und ACL sowie Preprints auf arXiv. Es wurde bewusst nicht nur nach Bestätigung gesucht, sondern gezielt auch nach Arbeiten, die zeigen, dass KI-Erkennung unzuverlässig oder grundsätzlich begrenzt ist — das ist tatsächlich der größere Teil der aktuellen Forschungslage.

---

## A. Zusammenfassung: Die wichtigsten Erkenntnisse

1. Es gibt **kein Verfahren, das die Autorschaft eines einzelnen, kurzen Textes zweifelsfrei beweist** — weder stilistische Analyse noch kommerzielle Detektoren noch Statistik.
2. Das Wikipedia-Kompendium ist kein Erkennungsalgorithmus, sondern eine von Freiwilligen über Jahre gesammelte Mustersammlung typischer Formulierungen — nützlich als Heuristik, nicht als Beweis (Wikipedia, *Signs of AI writing*).
3. Menschen, die selbst häufig mit LLMs schreiben, erkennen KI-Text erstaunlich zuverlässig — in einer Studie irrte sich die Mehrheitsentscheidung von fünf "Experten" nur bei 1 von 300 Artikeln, deutlich besser als die meisten kommerziellen Detektoren (Russell, Karpinska & Iyyer, 2025).
4. Automatische Detektoren (GPTZero, Turnitin, Originality.ai, Copyleaks u. a.) werben mit Genauigkeiten von 98–99,98 %, doch unabhängige Tests kommen regelmäßig auf deutlich niedrigere und stark schwankende Werte (Weber-Wulff et al., 2023; Dugan et al., 2024).
5. Ein zentrales, mehrfach repliziertes Problem: Detektoren stufen Texte von **Nicht-Muttersprachlern** systematisch häufiger fälschlich als KI-generiert ein — in einer Stanford-Studie über 61 % der TOEFL-Aufsätze, bei nahezu perfekter Erkennung für muttersprachliche Texte (Liang et al., 2023).
6. Einfaches **Paraphrasieren** hebelt fast alle getesteten Detektoren aus — ein Paraphrasier-Modell senkte die Trefferquote von DetectGPT von 70,3 % auf 4,6 % (Krishna et al., 2023).
7. Es gibt ein **theoretisches Unmöglichkeitsresultat**: Je besser ein Sprachmodell menschlichen Text imitiert, desto näher rückt die bestmögliche Erkennungsgenauigkeit an reines Raten heran (Sadasivan et al., 2023).
8. **Wasserzeichen** (z. B. Googles SynthID-Text) sind technisch elegant und funktionieren im Produktivbetrieb, wirken aber nur, wenn der Anbieter sie aktiv einbaut — bei Umschreiben, Paraphrasieren oder Rückübersetzung brechen sie häufig zusammen (Dathathri et al., 2024; Nachfolgeforschung zu SynthID-Robustheit).
9. **Content Credentials / C2PA** bieten kryptografisch überprüfbare Herkunftsnachweise, sind aber für reinen Text kaum verbreitet und lassen sich durch simples Kopieren des Textes ohne die Datei-Metadaten vollständig umgehen.
10. Ein eigener OpenAI-Detektor wurde bereits im Juli 2023 nach nur sechs Monaten wegen "geringer Genauigkeitsrate" wieder abgeschaltet — er erkannte nur 26 % der KI-Texte korrekt und stufte 9 % menschlicher Texte falsch ein (OpenAI, 2023).
11. Bestimmte Wortwahl-Signale (z. B. "delve", "underscore", "boast") sind statistisch nachweisbar häufiger in KI-Texten und lassen sich auf Korpusebene sogar quantifizieren — mindestens 10 % der 2024 veröffentlichten PubMed-Abstracts zeigen Spuren von LLM-Bearbeitung, in manchen Fachgebieten bis zu 30 % (Kobak et al., 2024). Das funktioniert aber nur statistisch über große Textmengen, nicht zuverlässig an einem Einzeltext.
12. Menschliche Sprache selbst verändert sich durch den Kontakt mit LLMs — bestimmte "KI-typische" Wörter tauchen inzwischen auch vermehrt in unvorbereiteter gesprochener Sprache auf, etwa in Podcasts (Yakura et al., 2024/2025; Juzek et al., 2025). Das schwächt langfristig die Aussagekraft rein lexikalischer Indizien.
13. Deutsche Texte werden von den meisten (meist englisch-zentrierten) Detektoren schlechter erkannt als englische; mehrsprachige Benchmarks zeigen Genauigkeitseinbrüche von teils über 40 Prozentpunkten bei weniger gut abgedeckten Sprachen.
14. Zahlreiche US-Universitäten (u. a. Vanderbilt, Johns Hopkins, Yale, University of Waterloo) haben die KI-Erkennungsfunktion von Turnitin wegen Zuverlässigkeitsproblemen zwischenzeitlich abgeschaltet.
15. Die einzig wirklich belastbare Aussage bleibt eine **statistische**, keine individuelle: Auf Korpusebene (Tausende Texte) lässt sich der Einfluss von LLMs nachweisen; bei einem einzelnen, möglicherweise überarbeiteten Text bleibt jede Einschätzung eine Wahrscheinlichkeitsaussage mit relevanter Fehlerquote in beide Richtungen.

---

## 1. Sprachliche und stilistische Merkmale

Das Wikipedia-Projekt *WikiProject AI Cleanup* pflegt seit 2023 eine sehr umfangreiche Sammlung wiederkehrender Formulierungsmuster aus tatsächlich identifizierten KI-Textbeiträgen (Wikipedia, *Signs of AI writing*). Die häufigsten, in mehreren unabhängigen Zusammenfassungen genannten Kategorien lassen sich so gruppieren:

- **Negative Parallelismen**: Konstruktionen der Form "Es ist nicht X, es ist Y", die eine Aussage künstlich zuspitzen, ohne inhaltlich viel zu sagen.
- **Dreiergruppen (Rule of Three)**: Aufzählungen von genau drei Adjektiven oder Vorteilen, oft ohne dass eine echte Dreiteiligkeit in der Sache liegt.
- **Falsche Spannweiten**: Formulierungen wie "von X bis Y", die einen Gegensatz oder ein Spektrum suggerieren, wo eigentlich nur zwei lose verwandte Dinge nebeneinandergestellt werden.
- **Übertriebene Bedeutungszuschreibung**: Aussagen darüber, warum ein Thema "wichtig" sei, "eine zentrale Rolle spielt" oder "bis heute nachwirkt" — oft ohne inhaltlichen Mehrwert.
- **Zwanghafte Zusammenfassungen**: Formulierungen wie "Zusammenfassend lässt sich sagen" oder "Insgesamt" am Ende von Absätzen, die in dieser Häufung bei menschlichen Fachtexten seltener vorkommen.
- **Auffällige, formelhafte Übergangswörter**: Häufung von "außerdem", "darüber hinaus", "nicht zuletzt", "zudem" in dichter Abfolge.
- **Ein spezifisches KI-Vokabular**: Wörter wie "delve" (dt. sinngemäß "sich vertiefen"), "intricate", "tapestry", "pivotal", "underscore", "landscape", "foster", "testament", "enhance", "crucial" im Englischen — im Deutschen entsprechend häufungsartig auftretende Wörter wie "maßgeblich", "vielschichtig" oder "unterstreichen".
- **Fehlende konkrete, persönliche Details**: generische Beispiele statt spezifischer, überprüfbarer Fakten oder persönlicher Erfahrungen.
- **Formatierungs-Reflexe**: Aufzählungspunkte und Fettungen auch dort, wo ein einzelner Satz gereicht hätte.

Warum entstehen diese Muster? Sie sind eine Folge des Trainingsprozesses: Modelle, die per Verstärkungslernen aus menschlichem Feedback (RLHF) auf "hilfreiche", ausgewogene und positiv klingende Antworten trainiert werden, tendieren zu einer statistischen Regression zum Mittelwert — konkrete Fakten werden zu generischen, überall passenden Aussagen geglättet (Wikipedia, *Signs of AI writing*).

**Wichtige Einschränkung schon hier:** Ein Hacker-News-Kommentator wies zu Recht darauf hin, dass Formulierungen wie "einerseits … andererseits" oder "nicht nur X, sondern auch Y" ganz regulär von Menschen verwendet werden — schließlich wurden die Modelle selbst auf menschlichem Text trainiert. Einzelne Signalwörter als Beweis zu nehmen, erzeugt daher zuverlässig falsche Anschuldigungen (Diskussion auf Hacker News zum Wikipedia-Artikel, 2025).

---

## 2. Stilometrische Analyse: Perplexity und Burstiness

Zwei Kernkonzepte tauchen in praktisch jedem älteren Detektionsverfahren auf:

- **Perplexity** misst, wie "vorhersagbar" ein Text für ein Referenzmodell ist. Technisch ist es (vereinfacht) der negative mittlere Log-Wahrscheinlichkeitswert der tatsächlich verwendeten Wörter unter einem Sprachmodell. Niedrige Perplexity bedeutet: Der Text folgt sehr vorhersagbaren, "glatten" Wortfolgen — ein Muster, das bei KI-generiertem Text häufiger auftritt.
- **Burstiness** misst die Schwankungsbreite der Perplexity zwischen einzelnen Sätzen eines Textes (üblicherweise die Standardabweichung). Menschliche Texte wechseln oft sprunghaft zwischen einfachen und komplexen, überraschenden Formulierungen; KI-Text ist tendenziell gleichmäßiger im Schwierigkeitsgrad (Beschreibung des GPTZero-Verfahrens in einer Analyse von Chen et al., 2023, arXiv:2310.01307).

Das Analyse-Tool **GLTR** (*Giant Language Model Test Room*, Gehrmann, Strobelt & Rush, 2019, ACL) visualisiert für jedes Wort, wie wahrscheinlich es unter einem Referenzmodell war (eingeteilt in vier Rangklassen: Top 10, Top 100, Top 1.000, Rest). In einer kontrollierten Studie mit menschlichen Testpersonen erhöhte GLTR die Trefferquote beim Erkennen generierter Texte von 54 % auf 72 % — ganz ohne vorheriges Training der Testpersonen (Gehrmann et al., 2019).

**Warum diese Methoden heute schwächer wirken:** Ältere Sprachmodelle mit einfachem, deterministischem Sampling erzeugten tatsächlich sehr niedrige, gleichmäßige Perplexity-Werte. Moderne Modelle nutzen variablere Sampling-Strategien (Temperature, Top-p/Top-k), wodurch die statistische Signatur weniger eindeutig wird. Zudem korreliert niedrige Perplexity nicht nur mit KI-Autorschaft, sondern schlicht mit **sprachlicher Einfachheit** — was zum zentralen Bias-Problem in Abschnitt 3 führt.

---

## 3. KI-Detektoren im Detail

### 3.1 Funktionsprinzipien

Man kann drei technische Grundtypen unterscheiden:

1. **Statistische Zero-Shot-Verfahren** ohne eigenes Training (Perplexity/Burstiness, GLTR): einfach, transparent, aber leicht durch moderne, fließend geschriebene Texte auszuhebeln.
2. **Modellbasierte Zero-Shot-Klassifikatoren**:
   - **DetectGPT** (Mitchell et al., 2023, ICML) nutzt die Beobachtung, dass von einem Modell erzeugter Text tendenziell in Regionen negativer Krümmung der Log-Wahrscheinlichkeitsfunktion dieses Modells liegt. Kleine, sinnerhaltende Störungen des Textes verändern die Wahrscheinlichkeit bei KI-Text stärker als bei Menschentext. In kontrollierten Tests verbesserte DetectGPT die Erkennungsgenauigkeit (AUROC) gegenüber dem stärksten einfachen Zero-Shot-Verfahren von 0,81 auf 0,95 bei generierten Falschmeldungstexten.
   - **Binoculars** (Hans et al., 2024, ICML) vergleicht die Perplexity eines Textes unter einem "Beobachter"-Modell mit der Kreuz-Perplexity unter einem eng verwandten "Performer"-Modell. Über verschiedene Textquellen hinweg erkannte Binoculars über 90 % generierter ChatGPT-Texte bei einer Falsch-Positiv-Rate von nur 0,01 % — ohne selbst auf ChatGPT-Daten trainiert worden zu sein. Die Autoren räumen jedoch selbst ein, dass die Methode für Englisch deutlich zuverlässiger funktioniert als für andere Sprachen (Hans et al., 2024, GitHub-Dokumentation).
3. **Trainierte, überwachte Klassifikatoren**: die meisten kommerziellen Tools (GPTZero, Turnitin, Originality.ai, Copyleaks, Pangram) fallen in diese Kategorie — neuronale Netze, die auf großen Mengen menschlicher und KI-generierter Beispieltexte trainiert wurden.

### 3.2 Wie zuverlässig sind kommerzielle Tools wirklich?

Hier klafft eine große Lücke zwischen Marketing und unabhängiger Prüfung:

- **Herstellerangaben**: Turnitin wirbt mit 98 % Genauigkeit und unter 1 % Falsch-Positiven auf Dokumentebene; Copyleaks mit 99,1 %; GPTZero mit 99 % bei 1 % Falsch-Positiv-Schwelle; Originality.ai mit 99 %.
- **Unabhängige, peer-reviewte Prüfung** (Weber-Wulff et al., 2023, *International Journal for Educational Integrity*): 14 gängige Tools wurden an unbearbeiteten, manuell editierten und maschinell paraphrasierten KI-Texten getestet. Nur **ein** Tool (Turnitin) klassifizierte alle unbearbeiteten Texte korrekt; **kein einziges** der 14 Tools erkannte zuverlässig alle Texte, die manuell überarbeitet oder maschinell paraphrasiert worden waren.
- **RAID-Benchmark** (Dugan et al., 2024, ACL, arXiv:2405.07940): der bislang umfangreichste unabhängige Test mit über 6 Millionen generierten Texten aus 11 Modellen, 8 Themenbereichen, 11 Angriffsarten und 4 Dekodier-Strategien. Ergebnis: Sowohl offene als auch kommerzielle Detektoren lassen sich durch adversariale Angriffe, veränderte Sampling-Strategien und unbekannte Generierungsmodelle leicht täuschen.
- **Pangram-Technical-Report** (arXiv:2402.14873, herstellernahe Quelle, daher mit Vorsicht zu lesen): berichtet für das eigene Modell 99 % Genauigkeit, während GPTZero in derselben Auswertung eine Falsch-Negativ-Rate von rund 10 % und Originality.ai eine Falsch-Positiv-Rate von über 9 % gehabt haben sollen.
- OpenAI stellte den eigenen "AI Text Classifier" bereits sechs Monate nach Veröffentlichung wieder ein — er erkannte nur 26 % der KI-Texte korrekt und markierte gleichzeitig 9 % ehrlicher menschlicher Texte fälschlich als KI (OpenAI, 2023).

**Fazit dieses Abschnitts**: Die tatsächliche Spannbreite unabhängig gemessener Genauigkeit reicht je nach Studie, Tool, Textlänge und Bearbeitungsgrad von deutlich unter 50 % bis über 90 % — es gibt keine verlässliche, universell gültige Kennzahl.

### 3.3 Das Bias-Problem gegenüber Nicht-Muttersprachlern

Die einflussreichste Einzelstudie zu diesem Thema stammt von Forschenden der Stanford University (Liang, Yuksekgonul, Mao, Wu & Zou, 2023, *Patterns*): Sieben verbreitete GPT-Detektoren stuften **über 61 %** von TOEFL-Aufsätzen nicht-muttersprachlicher Englisch-Schreiber fälschlich als KI-generiert ein, während Aufsätze US-amerikanischer Achtklässler nahezu fehlerfrei als menschlich erkannt wurden. Die Erklärung: Weniger variantenreiche Wortwahl und Syntax bei Nicht-Muttersprachlern führt zu niedrigerer Perplexity — genau das Signal, das Detektoren als "KI-typisch" werten. Ein einfacher Test bestätigte den Mechanismus: Ließ man ChatGPT die Wortwahl der TOEFL-Aufsätze "muttersprachlicher klingen" lassen, sank die Falscherkennung deutlich; vereinfachte man umgekehrt die Wortwahl nativer Aufsätze, stieg die Falscherkennung stark an.

Diese Befunde wurden seither mehrfach repliziert (u. a. Giray, 2024; weitere Studien 2025/2026) und gelten inzwischen als robuster, wiederkehrender Effekt und nicht als Eigenheit einzelner Tools. Mehrere Anbieter (u. a. GPTZero) haben nachträglich Anpassungen vorgenommen; unabhängige Nachtests fanden dennoch weiterhin messbare Restfehlerraten bei nicht-muttersprachlichen Texten.

**Relevanz für den deutschsprachigen Raum**: Da die meisten Trainings- und Testkorpora englisch-zentriert sind, gilt der Effekt tendenziell auch für nicht-englische Muttersprachler, die auf Englisch schreiben — und die verfügbaren Tools sind für deutsche Texte insgesamt schlechter kalibriert (siehe 3.4).

### 3.4 Mehrsprachigkeit und Deutsch

Mehrere Benchmarks zeigen einen deutlichen Leistungsabfall außerhalb des Englischen. Bei einer mehrsprachigen Shared-Task-Auswertung (2025) erreichten gut abgedeckte Sprachen wie Chinesisch, Russisch oder Spanisch 89–94 % Erkennungsgenauigkeit, während für im Training kaum vertretene Sprachen wie Hindi selbst das beste Team nur rund 52 % erreichte — nahe am Zufallsniveau. Auch die Binoculars-Autoren nennen die schwächere Leistung außerhalb des Englischen ausdrücklich als bekannte Grenze ihres Verfahrens.

Für deutschsprachige Texte berichten mehrere unabhängige (nicht-akademische) Tests aus 2026 durchgängig schlechtere Ergebnisse für die etablierten englischsprachigen Tools (GPTZero, ZeroGPT) im Vergleich zu Englisch. Als spezialisierte Alternative wird gelegentlich das an der FH Wedel entwickelte, kostenfreie Forschungsprojekt zur deutschen KI-Texterkennung genannt. Diese Angaben stammen aus praxisnahen, nicht peer-reviewten Quellen und sollten vor einer wichtigen Anwendung selbst nachgeprüft werden.

---

## 4. Technische Erkennungsmethoden: Watermarking, Provenance, Metadaten

### 4.1 Statistisches Text-Watermarking

Kirchenbauer et al. (2023, ICML) stellten das grundlegende Verfahren vor: Bei jedem generierten Wort wird eine pseudozufällige Menge "grüner" Token leicht bevorzugt. Ein einfacher statistischer Test kann später mit einem interpretierbaren p-Wert nachweisen, ob ein Text überproportional viele "grüne" Token enthält — ein Hinweis auf Generierung durch das wasserzeichentragende Modell, bei minimalem Qualitätsverlust.

**Google DeepMinds SynthID-Text** (Dathathri et al., 2024, veröffentlicht in *Nature*) ist die bislang einzige in großem Maßstab produktiv eingesetzte Umsetzung: über ein "Turnier-Sampling"-Verfahren wird das Wasserzeichen ressourcenschonend eingebettet. In einem Live-Test mit rund 20 Millionen Gemini-Nutzeranfragen bemerkten Nutzer keinen Qualitätsunterschied zwischen wasserzeichenversehenen und normalen Antworten (Dathathri et al., 2024; begleitender *Nature*-Kommentar 2024).

**Grenzen**: Wasserzeichen funktionieren nur, wenn der Anbieter sie aktiv einbaut — es gibt aktuell keine Möglichkeit, ein Wasserzeichen nachträglich in bereits erzeugtem Text zu suchen, wenn das Modell keines gesetzt hat. Zudem zeigen mehrere Folgeuntersuchungen zu SynthID, dass die Methode zwar gegen einfache lexikalische Angriffe robust ist, bei sinnerhaltenden Umformulierungen (Paraphrasieren, Rückübersetzung) aber deutlich an Erkennungsgenauigkeit verliert. Ein von einem Menschen sorgfältig überarbeiteter Text lässt sich also weiterhin nur eingeschränkt zurückverfolgen.

### 4.2 Content Credentials / C2PA

Die *Coalition for Content Provenance and Authenticity* (C2PA) definiert einen offenen Standard für kryptografisch signierte, manipulationssichere Herkunftsnachweise ("Content Credentials"). Dabei wird bei der Erstellung eines Inhalts ein signiertes Manifest erzeugt, das Ersteller, verwendetes Werkzeug und Bearbeitungsschritte dokumentiert; jede nachträgliche Änderung am Inhalt macht die Signatur ungültig (C2PA-Spezifikation, 2025; Content Authenticity Initiative).

In der Praxis ist der Standard bislang vor allem bei Bildern und Videos verbreitet (z. B. Kamera-Integration bei aktuellen Samsung-Galaxy-Geräten, Microsoft Bing/Designer, professionelle Broadcast-Kameras). Für reinen **Text** ist die Verbreitung noch sehr gering, und das grundlegende Problem bleibt bestehen: Wird nur der reine Textinhalt kopiert (z. B. in ein neues Dokument eingefügt), geht die angehängte Signatur komplett verloren — anders als ein statistisches Wasserzeichen ist ein Content-Credential-Manifest keine im Text selbst verankerte Eigenschaft, sondern reine Begleit-Metadatei.

### 4.3 Weitere technische Ansätze

- **Retrieval-basierte Erkennung**: Krishna et al. (2023) schlagen vor, generierte Texte in einem durchsuchbaren Korpus früherer Modell-Ausgaben zu speichern und neue Anfragen per semantischer Ähnlichkeitssuche abzugleichen. Dieses Verfahren erkannte in Experimenten 80–97 % paraphrasierter KI-Texte — ist aber nur nutzbar, wenn der jeweilige Modellanbieter selbst einen solchen Korpus pflegt und öffnet, was aktuell nicht der Standardfall ist.
- **Embedding-/Stil-Repräsentationsverfahren**: neuere Forschungsarbeiten (z. B. Few-Shot-Stildetektion) nutzen gelernte Stil-Einbettungen statt einfacher Wortstatistik, sind aber überwiegend Forschungsprototypen ohne breite kommerzielle Verfügbarkeit.
- **Log-Probability-/Entropie-basierte Verfahren**: Weiterentwicklungen von GLTR und DetectGPT (z. B. Fast-DetectGPT) reduzieren den Rechenaufwand, benötigen aber weiterhin direkten oder indirekten Zugriff auf Wahrscheinlichkeitswerte eines Referenzmodells — bei rein schwarzen Blackbox-Modellen ohne API-Zugriff auf Logits ist das nicht immer möglich.

---

## 5. Vergleich Mensch vs. KI: Was ist wissenschaftlich belastbar?

### 5.1 Menschliche Erkennungsfähigkeit übertrifft oft die Software

Eine 2025 auf der ACL veröffentlichte Studie (Russell, Karpinska & Iyyer) ließ Testpersonen 300 englischsprachige Sachtextartikel als menschlich oder KI-generiert einstufen. Personen, die selbst regelmäßig mit ChatGPT und ähnlichen Modellen schreiben, erkannten KI-Text deutlich zuverlässiger als Gelegenheitsnutzer — bei einer Mehrheitsentscheidung von fünf solchen "Experten" irrten sich nur 1 von 300 Einschätzungen, und das selbst bei absichtlich paraphrasierten oder "humanisierten" Texten, wo automatische Tools deutlich schlechter abschnitten. Diese Personen stützten sich zwar stark auf bekannte "KI-Vokabeln", bezogen aber auch schwerer greifbare Kriterien wie Formalitätsgrad, Originalität und Klarheit mit ein.

Diese Studie deckt sich mit einer 2025 veröffentlichten, im Wikipedia-Kompendium zitierten Untersuchung: Vielnutzer von LLMs identifizierten KI-generierte Wikipedia-Artikel in rund 90 % der Fälle richtig, während Gelegenheitsnutzer kaum besser als der Zufall abschnitten.

### 5.2 Nachweisbare, aber nur statistisch belastbare Sprachverschiebungen

Kobak, González-Márquez, Horvát & Lause (2024) untersuchten 14 Millionen PubMed-Abstracts von 2010 bis 2024 und fanden einen abrupten Anstieg bestimmter Stilwörter ("delve", "underscore" u. a.) nach der Veröffentlichung von ChatGPT — ein Muster, das mit keinem anderen historischen Ereignis (auch nicht der Covid-Pandemie) vergleichbar war. Daraus lässt sich eine untere Schätzgrenze ableiten: mindestens 10 % der 2024er-Abstracts zeigen Spuren von LLM-Bearbeitung, in einzelnen Fachrichtungen bis zu 30 %. Bemerkenswert: Nachdem diese Wörter 2024 öffentlich als "KI-Marker" bekannt wurden, sank ihre Häufigkeit wieder spürbar — ein Hinweis darauf, dass Autorinnen und Autoren ihre Nutzung angepasst haben.

### 5.3 Die Sprachen selbst konvergieren

Zwei unabhängige Forschungsgruppen (Yakura et al., 2024/2025; Juzek et al., 2025) fanden anhand von Milliarden transkribierter Wörter aus Podcasts und wissenschaftlichen Vorträgen einen messbaren Anstieg "KI-typischer" Wörter auch in **unvorbereiteter, gesprochener** Sprache nach 2022 — über 34 Sprachen hinweg im Mittel ein Anstieg von gut 15 %. Das bedeutet: Menschliche Sprache selbst verändert sich durch den ständigen Kontakt mit KI-generiertem Text, was rein lexikalische Erkennungssignale mit der Zeit systematisch schwächer und unzuverlässiger macht.

---

## 6. Manipulation und Umgehung

| Manipulation | Beobachteter Effekt auf Detektoren | Quelle |
|---|---|---|
| Leichtes Paraphrasieren (z. B. mit spezialisiertem Paraphrasier-Modell) | Erkennungsrate von DetectGPT fiel von 70,3 % auf 4,6 %; Wasserzeichen, GPTZero und OpenAIs Klassifikator wurden ebenfalls ausgehebelt | Krishna et al., 2023 |
| Rekursives, mehrfaches Umformulieren | Selbst retrieval-basierte Abwehrmaßnahmen verlieren zunehmend an Wirksamkeit | Sadasivan et al., 2023 |
| Manuelle menschliche Überarbeitung | Keines von 14 getesteten Tools erkannte alle überarbeiteten KI-Texte korrekt | Weber-Wulff et al., 2023 |
| Einfacher "Selbstbearbeitungs"-Prompt ("Formuliere literarischer") | Erkennungsrate bei ChatGPT-3.5-Aufsätzen sank von 100 % auf 13 % | Liang et al., 2023 |
| Maschinelle Übersetzung / Rückübersetzung | Wasserzeichen (SynthID) und klassische Detektoren verlieren deutlich an Genauigkeit | Robustheitsstudien zu SynthID; Forschung zu sprachübergreifender Wasserzeichen-Konsistenz |
| Kommerzielle "Humanizer"-Tools | Zunehmend als eigenständiges Forschungsfeld ("adversariale Humanisierung") anerkannt; unabhängige, nicht-akademische Tests berichten deutlich reduzierte Erkennungsraten nach Humanisierung, aber keine vollständige Umgehung | aktuelle Forschung zu Verteilungsverschiebung bei der Texterkennung, 2026 |
| Umschreiben durch ein anderes KI-Modell | Reduziert modellspezifische statistische Signaturen (Perplexity, Wasserzeichen), die an das ursprüngliche Modell gebunden sind | ableitbar aus den Grundprinzipien von Perplexity- und Wasserzeichen-Verfahren |

**Wichtig**: Diese Tabelle beschreibt dokumentierte Forschungsergebnisse zur Funktionsweise und den Grenzen von Erkennungsverfahren — sie ist keine Anleitung und ersetzt nicht die Verantwortung, KI-Nutzung dort offenzulegen, wo dies verlangt wird (z. B. akademische Arbeiten, journalistische Inhalte).

---

## 7. Aktuelle Forschung im Überblick

Die Forschungslage 2023–2026 lässt sich in drei Wellen einteilen:

- **2023**: Grundlagenjahr — Kirchenbauer (Wasserzeichen), Mitchell/DetectGPT (Zero-Shot-Krümmung), Liang (Bias-Nachweis), Sadasivan (Unmöglichkeitsresultat), Krishna (Paraphrasier-Angriff), Weber-Wulff (erste große unabhängige Tool-Prüfung).
- **2024**: Konsolidierung und Skalierung — Hans/Binoculars (robusteres Zero-Shot-Verfahren), Dathathri/SynthID (produktionsreifes Wasserzeichen, *Nature*), Dugan/RAID (größter Benchmark), Kobak (Korpusweite Vokabelverschiebung), Yakura (Sprachkonvergenz gesprochener Sprache).
- **2025/2026**: Differenzierung — Russell et al. (menschliche Expertise schlägt viele Tools), Replikationsstudien zum Bias-Effekt in weiteren Sprachen, erste kommerzielle Anbieter (Pangram u. a.) mit eigenen technischen Reports, wachsende Forschung zu "adversarialer Humanisierung" als eigenem Wettrüsten zwischen Generierung und Erkennung, erste mehrsprachige Benchmarks mit expliziten Übersetzungs- und Niedrig-Ressourcen-Sprachen-Tests.

Ein wiederkehrendes Zitat aus dem RAID-Team (Callison-Burch, Pressemitteilung der University of Pennsylvania, 2024) bringt den Stand treffend auf den Punkt: Es handelt sich um ein fortlaufendes Wettrüsten zwischen Erkennungs- und Umgehungstechnologie, bei dem robuste Detektoren zwar ein anzustrebendes Ziel bleiben, aktuell verfügbare Werkzeuge aber weiterhin deutliche Schwächen und Angriffsflächen aufweisen.

---

## 8. Wichtige Einschränkung: Merkmal ≠ Beweis

Alle in dieser Recherche zusammengetragenen Verfahren — von der Wortwahl-Heuristik bis zum aufwendigsten Zero-Shot-Klassifikator — liefern **Wahrscheinlichkeitsaussagen auf Basis statistischer Muster**, keine Tatsachenfeststellung im Sinne eines Beweises. Der entscheidende Unterschied:

- *"Der Text weist Merkmale auf, die häufig bei KI-generiertem Text vorkommen"* ist eine Aussage über statistische Ähnlichkeit zu einem Trainingskorpus.
- *"Der Text wurde definitiv von einer KI geschrieben"* wäre eine Tatsachenbehauptung über die tatsächliche Entstehung des konkreten Textes — dafür reicht Stilanalyse allein grundsätzlich nicht aus, weil dieselben Muster auch bei Menschen auftreten (die ja die Trainingsdaten der Modelle geschrieben haben) und weil jede Form der Bearbeitung, Paraphrasierung oder Übersetzung die statistischen Spuren verändert oder verwischt.

Selbst die zuverlässigste heute verfügbare Methode — geschulte menschliche Einschätzung durch Vielnutzer von LLMs — erreichte im besten dokumentierten Fall eine Fehlerquote von rund einem Text unter 300, nicht null. Rechtlich ist diese Unschärfe bereits anerkannt: Nach Art. 22 DSGVO dürfen in der EU keine Sanktionen ausschließlich auf Basis eines automatisierten Detektor-Ergebnisses verhängt werden — eine menschliche Prüfung und Abwägung bleibt zwingend erforderlich.

---

## B. Methoden-Tabelle

| Methode | Wie funktioniert sie? | Was wird analysiert? | Zuverlässigkeit (1–10) | Schwächen | Quelle |
|---|---|---|---|---|---|
| Manuelle Stil-Heuristik (Wikipedia-Liste) | Abgleich mit bekannten Formulierungsmustern | Wortwahl, Satzbau, Rhetorik | 4 | Hohe Falsch-Positiv-Rate bei stilistisch ähnlich schreibenden Menschen; erfordert Erfahrung | Wikipedia, *Signs of AI writing* |
| Perplexity/Burstiness (klassisch, z. B. alte GPTZero-Methode) | Misst Vorhersagbarkeit und deren Schwankung im Text | Statistische Sprachmuster | 3 | Verwechselt "einfache Sprache" mit "KI-Sprache"; wirkungslos bei modernen, variabel samplenden Modellen | Chen et al., 2023 (GPTZero-Beschreibung); GLTR-Grundlagenarbeit (Gehrmann et al., 2019) |
| GLTR-gestützte menschliche Einschätzung | Visualisiert Token-Wahrscheinlichkeitsränge zur Unterstützung menschlicher Urteile | Wortrang-Verteilung | 5 | Nur Hilfsmittel, kein automatisches Urteil; hebt Trefferquote nur moderat an (54 %→72 %) | Gehrmann et al., 2019 |
| DetectGPT / Fast-DetectGPT (Zero-Shot-Krümmung) | Misst Krümmung der Log-Wahrscheinlichkeitsfunktion bei kleinen Textstörungen | Wahrscheinlichkeitslandschaft des Quellmodells | 5 | Braucht Zugriff auf Logits eines nahen Referenzmodells; bricht bei Paraphrasierung stark ein (70,3 %→4,6 %) | Mitchell et al., 2023; Krishna et al., 2023 |
| Binoculars (Beobachter/Performer-Perplexity-Verhältnis) | Vergleicht Perplexity zweier eng verwandter Modelle | Kreuz-Perplexity-Verhältnis | 6 | Deutlich schwächer außerhalb des Englischen; anfällig für starke Textbearbeitung | Hans et al., 2024 |
| Trainierte kommerzielle Klassifikatoren (GPTZero, Copyleaks u. a.) | Neuronales Netz, trainiert auf großen Mengen Beispieltexten | Gelernte, oft intransparente Merkmalskombination | 4 | Große Schwankungsbreite zwischen Studien (teils unter 50 %, teils über 90 %); ESL-Bias; anfällig für Paraphrasierung | Weber-Wulff et al., 2023; Dugan et al., 2024 |
| Turnitin (schulisch/akademisch optimiert) | Ähnlich trainierter Klassifikator, bewusst konservativ kalibriert | Wie oben, mit Fokus auf niedrige Falsch-Positiv-Rate | 5 | Lässt laut eigener Kalibrierung bewusst mehr KI-Text unentdeckt durch, um Falschbezichtigungen zu vermeiden | Weber-Wulff et al., 2023 |
| Statistisches Wasserzeichen (Kirchenbauer-Verfahren) | Bevorzugt bei der Generierung eine geheime "grüne" Token-Teilmenge | Statistischer Test auf Token-Verteilung | 8 (wenn vorhanden und intakt) | Funktioniert nur, wenn der Anbieter es aktiv einbaut; bricht bei Paraphrasierung/Übersetzung deutlich ein | Kirchenbauer et al., 2023; Sadasivan et al., 2023 |
| SynthID-Text (produktionsreifes Wasserzeichen) | "Turnier-Sampling" zur Token-Auswahl, geringe Qualitätseinbußen | Wie oben, skaliert für Produktivbetrieb | 8 (wenn vorhanden und intakt) | Gleiche Grundschwäche wie alle Wasserzeichen; anfällig für semantikerhaltende Umformulierung | Dathathri et al., 2024 (*Nature*) |
| Retrieval-basierte Erkennung | Sucht semantisch ähnliche Texte in einem Korpus früherer Modell-Ausgaben | Semantische Ähnlichkeit zu bekannten Generierungen | 7 (nur bei Zugriff auf den Korpus) | Nur nutzbar, wenn der Modellanbieter selbst einen offenen Korpus pflegt — aktuell kaum verfügbar | Krishna et al., 2023 |
| Content Credentials / C2PA | Kryptografisch signiertes Herkunfts-Manifest bei der Dateierstellung | Erstellungs- und Bearbeitungsverlauf einer Datei | 3 (für reinen Text) | Geht komplett verloren, sobald nur der Textinhalt kopiert wird; für Text kaum verbreitet | C2PA-Spezifikation, 2025 |
| Korpusweite Vokabelanalyse ("Excess Vocabulary") | Vergleicht Wortfrequenzen großer Textmengen mit Vor-LLM-Basiswerten | Statistische Häufigkeitsverschiebung auf Korpusebene | 8 (nur für Aggregatanalysen, nicht für Einzeltexte) | Sagt nichts über einen einzelnen Text aus; nur auf großen Textmengen aussagekräftig | Kobak et al., 2024 |
| Menschliche Einschätzung, ungeübt | Intuitive Bewertung ohne besondere Vorkenntnisse | Gesamteindruck | 2–3 | Kaum besser als Zufall laut mehreren Studien | Wikipedia, *Signs of AI writing*; verwandte Detektionsstudien |
| Menschliche Einschätzung, geübte LLM-Vielnutzer | Kombination aus Vokabel-, Stil- und Plausibilitätsprüfung, oft mehrköpfig als Mehrheitsentscheid | Ganzheitlicher Texteindruck plus spezifische Indizien | 7–8 (individuell), höher im Gruppenkonsens | Aufwendig, nicht skalierbar, nur an einer Studie mit begrenztem Textkorpus (300 Sachtexte) belegt | Russell, Karpinska & Iyyer, 2025 |

---

## C. Praktische Checkliste: 20 Prüfpunkte für einen verdächtigen Text

**Sehr aussagekräftig** *(deutet stark auf maschinelle Erzeugung hin, aber immer noch kein Beweis)*
1. Ein von der Plattform selbst durchgeführter, positiver Wasserzeichen-Test (z. B. SynthID-Prüfung bei Google-Inhalten) — sofern der Text seit der Erstellung nicht wesentlich umformuliert wurde.
2. Ein gültiges, kryptografisch signiertes C2PA-Manifest, das den Text als KI-generiert ausweist.
3. Übereinstimmung mit einem bekannten, dokumentierten Fall aus einem Retrieval-Korpus eines Modellanbieters.
4. Mehrheitliches, unabhängiges Urteil mehrerer erfahrener LLM-Vielnutzer, die den Text unabhängig voneinander bewerten.

**Möglicherweise aussagekräftig** *(sinnvolle Hinweise, aber mit spürbarer Fehlerquote)*
5. Auffällige Häufung mehrerer typischer KI-Formulierungen gleichzeitig (nicht nur eine einzelne).
6. Durchgängig gleichmäßiger Schwierigkeitsgrad und Satzrhythmus über den gesamten Text (geringe "Burstiness").
7. Fehlen jeglicher konkreter, überprüfbarer persönlicher Details oder spezifischer Fakten.
8. Ergebnis eines seriösen, forschungsbasierten Zero-Shot-Detektors (z. B. Binoculars) bei nachweislich unbearbeitetem Text.
9. Wiederkehrende, identische rhetorische Strukturen in mehreren Absätzen desselben Textes.
10. Auffällige Widersprüche zwischen behauptetem Fachwissen und tatsächlicher inhaltlicher Tiefe.

**Schwache Indizien** *(für sich allein nicht ausreichend)*
11. Einzelne "typische" KI-Vokabeln (z. B. "maßgeblich", "vielschichtig", "unterstreichen").
12. Ergebnis eines einzelnen kommerziellen Online-Detektors ohne Zweitmeinung.
13. Betont ausgewogener, neutraler Tonfall ("einerseits … andererseits").
14. Formelhafte Einleitungen oder Schlussfolgerungen.
15. Auffällige Nutzung von Aufzählungspunkten oder Fettungen in an sich fließtext-üblichen Kontexten.
16. Rein subjektiver Bauchgefühl-Eindruck ("klingt irgendwie nach KI").

**Keine verlässlichen Beweise**
17. Kurze Textlänge unter etwa 200–300 Wörtern — hier versagen fast alle statistischen Verfahren nachweislich.
18. Texte von erkennbaren Nicht-Muttersprachlern oder in einfacher, klarer Sprache — hohes Risiko einer Fehleinstufung durch Bias-Effekte.
19. Ein einzelner, nicht bestätigter Score eines kostenlosen Online-Tools ohne Angabe der Falsch-Positiv-Rate.
20. Die bloße Tatsache, dass ein Text "zu gut" oder "zu druckreif" wirkt — das ist ebenso häufig bei sorgfältig arbeitenden Menschen der Fall.

---

## D. AI-Detektoren im Vergleich

| Tool | Funktionsweise | Bekannte Stärken | Bekannte Schwächen | Einordnung unabhängiger Tests |
|---|---|---|---|---|
| GPTZero | Perplexity/Burstiness plus trainierter Klassifikator | Kostenlose Basisnutzung, breite Bekanntheit, für Englisch gut kalibriert | Deutlich schwächer bei deutschen Texten; ESL-Bias dokumentiert (mit Nachbesserungen seit 2023) | In unabhängigen Studien stark schwankende Werte je nach Textart und Bearbeitungsgrad |
| Turnitin | Trainierter Klassifikator, in Plagiatssoftware integriert | Breite Verankerung im akademischen Betrieb | Bewusst konservativ (mehr unentdeckte KI-Texte statt Falschbezichtigungen); von mehreren Universitäten wegen Zuverlässigkeitsbedenken abgeschaltet | Einziges Tool, das in der Weber-Wulff-Studie alle unbearbeiteten Texte korrekt erkannte, versagte aber ebenfalls bei bearbeiteten Texten |
| Originality.ai | Trainierter Klassifikator, Fokus Content-Marketing/SEO-Branche | In mehreren Vergleichstests mit guter Gesamtleistung | In anderen Studien mit auffällig hoher Falsch-Positiv-Rate; Ergebnisse zwischen Studien widersprüchlich | Uneinheitliches Bild je nach Testquelle |
| Copyleaks | Trainierter Klassifikator, Teil einer Plagiats-Suite | Als eher "konservativ" (weniger Falsch-Positive) beschrieben | Übersieht dafür tendenziell mehr tatsächlich generierte Texte | Gemischte, meist nicht-akademische Testberichte |
| Pangram | Neuerer trainierter Klassifikator mit eigenem technischem Report | Herstellerseitig sehr niedrige gemeldete Fehlerraten, auch bei ESL-Texten | Bislang wenig unabhängige, nicht-herstellernahe Verifikation verfügbar | Nur begrenzt extern geprüft |
| DetectGPT / Fast-DetectGPT | Forschungs-Tool, Zero-Shot-Krümmungsanalyse | Kein Trainingskorpus nötig, wissenschaftlich gut dokumentiert | Kein fertiges Endnutzer-Produkt; braucht Modellzugriff; bricht bei Paraphrasierung stark ein | Gut in akademischer Literatur dokumentiert |
| Binoculars | Forschungs-Tool, Zwei-Modell-Perplexity-Vergleich | Hohe Genauigkeit bei niedriger Falsch-Positiv-Rate im Original-Setup | Schwächer außerhalb des Englischen (von den Autoren selbst benannt) | Peer-reviewt (ICML 2024), aber primär Forschungscode |
| OpenAI AI Text Classifier | (eingestellt) trainierter Klassifikator | — | Erkannte nur 26 % der KI-Texte, 9 % Falsch-Positive; 2023 abgeschaltet | Offiziell vom Hersteller selbst als unzureichend bewertet |
| FH Wedel KI-Texterkennung | Deutsches, kostenfreies Forschungsprojekt | Speziell für deutsche Fließtexte kalibriert | Reichweite und externe Validierung begrenzt; keine peer-reviewte Publikation gefunden | Nur aus nicht-akademischen Quellen bekannt — vor wichtiger Nutzung selbst prüfen |

---

## E. Wissenschaftliche Einschätzung: Wie gut lässt sich 2026 tatsächlich feststellen, ob ein Text von einer KI stammt?

Die ehrliche Antwort lautet: **zuverlässig auf Korpusebene, nicht zuverlässig am Einzeltext.**

Auf Ebene großer Textmengen — Tausende oder Millionen Dokumente — lässt sich der Einfluss von LLMs heute robust und mit wissenschaftlicher Methodik nachweisen, wie die Vokabelverschiebungs-Studien zu PubMed-Abstracts eindrücklich zeigen (Kobak et al., 2024). Auch produktionsreife Wasserzeichenverfahren wie SynthID-Text funktionieren im großen Maßstab zuverlässig, solange der Text unverändert vom generierenden System stammt.

Bei einem **einzelnen, isolierten Text** — genau der Situation, in der Menschen typischerweise eine Entscheidung treffen wollen ("Hat mein Kollege/meine Kollegin diesen Text mit KI geschrieben?") — sieht das Bild deutlich schlechter aus:

- Es existiert ein **theoretisches Argument** (Sadasivan et al., 2023), warum perfekte Erkennung bei ausreichend guten Sprachmodellen grundsätzlich unmöglich wird, weil sich die statistischen Verteilungen von Mensch- und KI-Text zunehmend überlappen.
- **Praktisch** bestätigt sich das: Der umfangreichste verfügbare Benchmark (RAID, über 6 Millionen Texte) zeigt, dass selbst die besten aktuell verfügbaren Detektoren durch einfache, realistische Textveränderungen ausgehebelt werden.
- Die **Fehlerquoten sind nicht symmetrisch verteilt** — sie treffen systematisch bestimmte Gruppen härter, insbesondere Nicht-Muttersprachler und Personen mit einfachem, klarem Schreibstil. Das macht automatisierte Einzelfallentscheidungen (z. B. Studienausschluss, Bewerbungsablehnung) besonders riskant und ethisch fragwürdig.
- **Menschliche Expertise** — insbesondere von Personen, die selbst regelmäßig mit LLMs arbeiten — schlägt in aktuellen Studien viele automatisierte Tools deutlich, bleibt aber aufwendig, nicht skalierbar und in ihrer Generalisierbarkeit über verschiedene Textarten hinweg bislang nur begrenzt untersucht.
- Ein zusätzlicher, struktureller Trend verschärft das Problem mit der Zeit: Da menschliche Sprache selbst zunehmend von LLM-typischen Formulierungen beeinflusst wird (Yakura et al., 2024/2025; Juzek et al., 2025), werden rein stilistische Signale langfristig **weniger**, nicht mehr aussagekräftig.

Die derzeit robusteste, wenn auch aufwendigste Kombination ist ein mehrstufiges Vorgehen: technische Herkunftsnachweise dort nutzen, wo verfügbar (Wasserzeichen, Content Credentials), automatisierte Detektoren nur als groben, nie alleinstehenden Erstindikator einsetzen, und bei wichtigen Entscheidungen zusätzlich geschulte menschliche Einschätzung sowie — wo immer möglich — ein direktes Gespräch mit der betreffenden Person einholen. Eine automatisierte Software-Ausgabe allein reicht wissenschaftlich betrachtet nicht als Beweis, und in der EU ist eine ausschließlich darauf gestützte Sanktionsentscheidung nach Art. 22 DSGVO ohnehin nicht zulässig.

---

## F. Quellenverzeichnis

1. Wikipedia — *Signs of AI writing* (WikiProject AI Cleanup): https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing
2. Liang, W., Yuksekgonul, M., Mao, Y., Wu, E. & Zou, J. (2023). *GPT detectors are biased against non-native English writers*. Patterns, 4(7). https://www.cell.com/patterns/fulltext/S2666-3899(23)00130-7 (Preprint: https://arxiv.org/abs/2304.02819)
3. Weber-Wulff, D., Anohina-Naumeca, A., Bjelobaba, S., Foltýnek, T., Guerrero-Dib, J., Popoola, O., Šigut, P. & Waddington, L. (2023). *Testing of detection tools for AI-generated text*. International Journal for Educational Integrity, 19(26). https://link.springer.com/article/10.1007/s40979-023-00146-z
4. Krishna, K., Song, Y., Karpinska, M., Wieting, J. & Iyyer, M. (2023). *Paraphrasing evades detectors of AI-generated text, but retrieval is an effective defense*. NeurIPS 2023. https://arxiv.org/abs/2303.13408
5. Sadasivan, V. S., Kumar, A., Balasubramanian, S., Wang, W. & Feizi, S. (2023). *Can AI-Generated Text be Reliably Detected?* arXiv:2303.11156. https://arxiv.org/abs/2303.11156
6. Mitchell, E., Lee, Y., Khazatsky, A., Manning, C. D. & Finn, C. (2023). *DetectGPT: Zero-Shot Machine-Generated Text Detection using Probability Curvature*. ICML 2023. https://arxiv.org/abs/2301.11305
7. Kirchenbauer, J., Geiping, J., Wen, Y., Katz, J., Miers, I. & Goldstein, T. (2023). *A Watermark for Large Language Models*. ICML 2023. https://proceedings.mlr.press/v202/kirchenbauer23a.html
8. Hans, A., Schwarzschild, A., Cherepanova, V., Kazemi, H., Saha, A., Goldblum, M., Geiping, J. & Goldstein, T. (2024). *Spotting LLMs With Binoculars: Zero-Shot Detection of Machine-Generated Text*. ICML 2024. https://arxiv.org/abs/2401.12070 (Code: https://github.com/ahans30/Binoculars)
9. Dathathri, S. et al. (2024). *Scalable watermarking for identifying large language model outputs*. Nature, 634, 818–823. https://www.nature.com/articles/s41586-024-08025-4
10. Dugan, L., Hwang, A., Trhlík, F., Zhu, A., Ludan, J. M., Xu, H., Ippolito, D. & Callison-Burch, C. (2024). *RAID: A Shared Benchmark for Robust Evaluation of Machine-Generated Text Detectors*. ACL 2024. https://aclanthology.org/2024.acl-long.674/
11. Russell, J., Karpinska, M. & Iyyer, M. (2025). *People who frequently use ChatGPT for writing tasks are accurate and robust detectors of AI-generated text*. ACL 2025. https://arxiv.org/abs/2501.15654
12. Kobak, D., González-Márquez, R., Horvát, E.-Á. & Lause, J. (2024). *Delving into ChatGPT usage in academic writing through excess vocabulary*. arXiv:2406.07016. https://arxiv.org/html/2406.07016v1
13. Gehrmann, S., Strobelt, H. & Rush, A. (2019). *GLTR: Statistical Detection and Visualization of Generated Text*. ACL 2019 (System Demonstrations). https://aclanthology.org/P19-3019/
14. Coalition for Content Provenance and Authenticity (C2PA). *C2PA and Content Credentials Explainer*, Version 2.2/2.4. https://spec.c2pa.org/specifications/specifications/2.4/explainer/Explainer.html ; FAQ: https://c2pa.org/faqs/
15. OpenAI (2023). *New AI classifier for indicating AI-written text* (mit Update zur Einstellung vom 20. Juli 2023). https://openai.com/index/new-ai-classifier-for-indicating-ai-written-text/
16. Yakura, H. et al. (2024/2025). *Empirical evidence of Large Language Model's influence on human spoken communication*. arXiv:2409.01754.
17. Juzek, T. S. et al. (2025). *Model Misalignment and Language Change: Traces of AI-Associated Language in Unscripted Spoken English*. arXiv:2508.00238. https://arxiv.org/abs/2508.00238
18. Pangram (2024). *Technical Report on the Pangram AI-Generated Text Classifier*. arXiv:2402.14873. (Herstellernahe Quelle — mit Vorsicht zu lesen.)
19. Chen, W. et al. (2023). Analyse der GPTZero-Perplexity/Burstiness-Methodik. arXiv:2310.01307.
20. Nature (2024). *AI watermarking must be watertight to be effective* (redaktioneller Kommentar zu SynthID-Text). https://www.nature.com/articles/d41586-024-03418-x

---

*Hinweis: Diese Zusammenstellung wurde im August 2026 erstellt und spiegelt den zu diesem Zeitpunkt verfügbaren Forschungsstand wider. Da sich sowohl Sprachmodelle als auch Erkennungsverfahren sehr schnell weiterentwickeln, sollten insbesondere die berichteten Genauigkeitszahlen einzelner kommerzieller Tools vor einer wichtigen Anwendung erneut geprüft werden.*
