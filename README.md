# LiveOS OS3

Eigenständiger LiveOS-Chat mit OS3, Training Engine, SkillNet und öffentlicher Web-Recherche.

## Online

GitHub-Pages-Adresse nach einmaliger Aktivierung unter **Settings → Pages → Deploy from a branch → main → / (root)**:

**https://urlaub-assistent.github.io/LiveOS/**

Die Trainingsseite liegt unter **/LiveOS/training/**. Chat und Trainingsseite nutzen dasselbe Gehirn-Schaltkreis-Logo aus `assets/liveos-icon.svg` und dasselbe PNG für das App-Symbol.

## Training und Modellstand

OS3 hat eine gemeinsame SkillNet-Trainingsbasis pro angemeldetem LiveOS-Konto. Jeder neue Trainingslauf setzt dessen zuletzt gespeicherten Checkpoint fort. Chat und Training lesen und schreiben denselben Checkpoint; Supabase Realtime verteilt bestätigte Updates an bereits geöffnete Chats desselben Kontos. Row Level Security hält die Checkpoints privat.

Die Trainingsmaschine läuft lokal im Browser auf der CPU und benötigt keine bezahlte API oder GPU. Sie nutzt ausgewogene Klassenauswahl, Momentum, Label-Smoothing, Gradient Clipping, Weight Decay, getrennte Validierung und Rücksprung zum besten geprüften Checkpoint. Bestehende OS2-Checkpoints werden migriert.

**Wichtig:** SkillNet ist ein 512-Feature → 64 Hidden-Neuronen → 19 Klassen Intent-/Routing-Klassifikator. Training verbessert die Zuordnung von Anfragen zu vorhandenen LiveOS-Fähigkeiten. Es trainiert kein generatives Sprachmodell, lernt nicht automatisch neue Fakten und macht freie Antworten nicht von selbst besser. Alle Geräte desselben Kontos nutzen denselben Stand; der Gastmodus bleibt lokal. Bitte nicht zwei Trainingsläufe desselben Kontos gleichzeitig starten, da beide den gesamten Checkpoint speichern.

## Verzeichnisstruktur

- `index.html`: LiveOS OS3 Chat
- `training/`: Training Engine, SkillNet-Core und Web Worker
- `assets/`: App-Icons
- `supabase/functions/liveos-web-research/`: öffentliche Web- und YouTube-Recherche
- `supabase/config.toml`: Supabase-Function-Konfiguration

## Supabase

LiveOS verwendet das bestehende Supabase-Projekt, damit Konten, Chatverläufe und Trainingsdaten erhalten bleiben. Die Recherchefunktion ist dort bereits bereitgestellt. Der Browser nutzt nur den öffentlichen Supabase-Schlüssel; private Schlüssel gehören ausschließlich auf den Server.

## Grenzen

Das Training läuft im Vordergrund des Browsers. Safari/iPadOS kann Hintergrund-Tabs pausieren; dann bleibt der letzte Checkpoint erhalten und kann nach erneutem Öffnen fortgesetzt werden. Die Web-Recherche liest ausschließlich öffentliche Seiten. Private Konten, Logins und Bezahlschranken werden nicht umgangen.
