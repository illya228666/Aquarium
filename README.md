# Aquarium

Selbstständig lauffähige Lösung der Schulaufgabe **Aquarium / Zoogeschäft Bremer**.

- `Aquarium.Core` – gemeinsame Fachklasse: Maße, Volumen, Glasfläche und Preis.
- `Aquarium.Console` – eigenständige Konsolenanwendung mit Eingaben und Beispielwerten.
- `Aquarium.Wpf` – WPF-Anwendung mit animierter, maßstabsgetreuer Vorschau.
- `docs/03_Aquarium.docx` – ursprüngliches Arbeitsblatt.

Beide Programme verwenden **dieselbe** Berechnung aus `Aquarium.Core`, ohne Codekopien oder Abhängigkeiten von anderen Aufgaben.

## Starten

Im Projektverzeichnis:

```powershell
dotnet run --project Aquarium.Console
dotnet run --project Aquarium.Wpf
```

Für WPF wird Windows mit der passenden .NET Desktop Runtime benötigt. Die Lösung `Aquarium.sln` kann unabhängig von `all-tasks-and-launcher` geöffnet werden.

Alle drei Projekte definieren ihren eigenen festen Target Framework: `Aquarium.Core` und `Aquarium.Console` verwenden `net7.0`, `Aquarium.Wpf` verwendet `net7.0-windows`. Die Programme sind dadurch auch dann separat baubar, wenn nur die Projektordner kopiert werden. Für Console und WPF ist `RollForward=Major` aktiviert, damit bei Bedarf eine neuere installierte .NET-Runtime genutzt werden kann.

Bei alten Build-Artefakten nach dem Verschieben oder Umstellen der .NET-Version zunächst die `bin`- und `obj`-Ordner aller drei Projekte löschen und anschließend `dotnet restore Aquarium.sln` ausführen.

## Lange Windows-Pfade

Die Quelldateien können an ihrem ursprünglichen Ort bleiben, auch wenn der Checkout-Pfad lang ist. `Directory.Build.props` leitet auf Windows nur die von MSBuild und NuGet generierten Zwischenartefakte (`obj` und `project.assets.json`) nach `%TEMP%\AquariumBuild\<Projektname>\obj\` um. Ausgabedateien (`bin`) bleiben im Projekt. Nach einem Update das Projekt in Visual Studio neu laden und einmal `dotnet restore Aquarium.sln` ausführen. Falls mehrere Aquarium-Checkouts parallel auf demselben Rechner existieren, sollten sie nicht gleichzeitig mit demselben Temp-Zwischenverzeichnis gebaut werden.

## Berechnung

- Maße in Zentimetern; alle müssen größer als 0 sein.
- Volumen (Liter): Länge × Breite × Höhe / 1000
- Glasfläche (dm²): (2 × Länge × Höhe + 2 × Breite × Höhe + Länge × Breite) / 100
- Endpreis: 20 € Grundbetrag + Glasfläche × Glaspreis, auf 5 € aufgerundet.

Beispiel: 80 × 35 × 35 cm, 0,40 €/dm² → **98 Liter**, **108,50 dm²**, **65 €**.

Dieses Repository ist eigenständig und wird von `all-tasks-and-launcher` als Git-Submodule unter `07_Klassen_und_Objekte/Aquarium` eingebunden.
