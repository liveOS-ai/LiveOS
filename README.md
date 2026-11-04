# LiveOS

Eigenständiges LiveOS-Projekt (OS3) mit Chat, Trainingsoberfläche, SkillNet-Trainingskern und Web-Recherche.

Die App verwendet das bereits bestehende Supabase-Projekt, damit Benutzerkonten, Chats, Trainings-Checkpoints und die bisherige OS3-Websuche nicht verloren gehen.

## GitHub Pages

Repository-Website: https://urlaub-assistent.github.io/LiveOS/

GitHub Pages muss in den Repository Settings auf **Deploy from a branch → main → / (root)** gesetzt sein.

## Training

Die Trainingsseite liegt unter `/training/`. Sie optimiert einen kleinen Intent-/Routing-Klassifikator, nicht die Gewichte eines großen generativen Sprachmodells. Alle bestätigten Checkpoints werden pro LiveOS-Konto in Supabase gespeichert und sind nach Anmeldung auf den Geräten desselben Kontos verfügbar.
