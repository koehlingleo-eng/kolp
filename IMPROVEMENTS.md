# Victorian Detective Game – konkrete Verbesserungen

## UI/UX (schöner)
- **Mikroanimationen vereinheitlichen**: ein zentrales Motion-Token-Set (`duration-150`, `ease-out`, `hover:scale-[1.02]`) statt gemischter Werte.
- **Bessere visuelle Hierarchie**: Überschriften/Sektionen per konsistentem Spacing-System (8px-Raster).
- **Kontrast-Boost** für Tooltips und Fließtext in dunklen Panels (AA-näher).
- **Progressive Disclosure**: Hinweise und „Noch unklar“-Texte mit `details/summary` klappbar.
- **Mobile Feinschliff**: größere Hit-Areas für Marker (mind. 44x44px) und sticky Aktionsleiste.

## Performance (effizienter)
- **Daten außerhalb des Komponenten-Bodys belassen** (bereits gut), plus:
  - `React.memo` für `EvidenceMarker`, `SceneryMarker`, `SuspectCard`.
  - `useCallback` für häufig weitergereichte Handler (`onChoose`, `onDiscover`, `onAskQuestion`).
- **Derived State minimieren**:
  - `score`, `askedCount`, `stars`, `suspectEvidenceMap` mit `useMemo` kapseln.
  - Wiederholte `find`-Aufrufe durch ID-Maps ersetzen (`Map<string, Evidence>`).
- **Render-Last reduzieren**:
  - Modal-Inhalte lazy laden (code-splitting).
  - Große Dekor-Komponenten optional als statische CSS-Hintergründe.

## Gameplay/Design (noch besser)
- **Adaptive Hint-Stufen**: nach 1–2 Fehldeutungen optional sanfter Hinweis.
- **Notebook aufwerten**:
  - Filter nach Quelle (Verhör/Umgebung/Beweis)
  - Priorisierte „kritische Notizen“ oben.
- **Balancing**:
  - Sternesystem um `timeSpent` ergänzen (optional), aber ohne Bestrafung bei Story-Spielstil.
- **Re-Playability**:
  - Rotierende Frage-Sets pro Verdächtigem (Pool > 4, je Run 4 gezogen).

## Architektur
- **useReducer statt viele useState**: klarere Event-Transitions (`DISCOVER_SCENERY`, `ASK_QUESTION`, `ACCUSE`).
- **Typisierung**: auf TypeScript migrieren (`Case`, `Evidence`, `Suspect`, `Question`).
- **Tests**:
  - `runGameLogicTests` in echte Unit-Tests (Vitest/Jest) überführen.

## Kurz-Roadmap
1. `useReducer` + Action-Typen einführen.
2. Marker-Komponenten `memo` + Handler `useCallback`.
3. Notebook-Filter + mobile sticky actions.
4. Unit-Tests + CI-Check.
