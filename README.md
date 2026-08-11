# ai-text-detection

Ein Claude Skill mit evidenzbasiertem Referenzwissen zur Erkennung von KI-generierten Texten (ChatGPT, Claude, Gemini u. a.) — basierend auf ~20 wissenschaftlichen Quellen (Stanford *Patterns*, *Nature*, ICML, NeurIPS, ACL, arXiv).

## Was der Skill enthält

- `SKILL.md` — steuert, wann Claude den Skill nutzt und wie er antwortet (Checkliste statt Ja/Nein-Urteil, Warnung vor Bias gegenüber Nicht-Muttersprachlern, keine Herstellerangaben ungeprüft übernehmen).
- `references/ai-text-detection-research.md` — die vollständige Recherche: Methoden-Tabelle mit Zuverlässigkeitsbewertung, 20-Punkte-Checkliste, Detektoren-Vergleich (GPTZero, Turnitin, Originality.ai u. a.), vollständiges Quellenverzeichnis.

## Installation

**Claude.ai / Claude Cowork:** SKILL.md-Datei (oder die gepackte `.skill`-Datei) über die Skill-Verwaltung hochladen.

**Claude Code:** Diesen Ordner nach `~/.claude/skills/ai-text-detection/` kopieren (oder als Submodule/Klon einbinden).

## Stand

August 2026. Detektor-Genauigkeiten ändern sich schnell — bei wichtigen Entscheidungen aktuelle Zahlen zusätzlich prüfen.

## Lizenz

Füge hier deine bevorzugte Lizenz hinzu (z. B. MIT), falls du das Repo öffentlich teilst.
