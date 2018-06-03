
## Pflichtenheft

Basierend auf dem Lastenheft werden im Folgenden die Anforderungen und Umsetzungen genauer beschrieben.

#### Zielgruppe: <br> 
Vertrieb XY, der den Wunsch hat seine Kundenkontakte über eine mobile App zu pflegen.
Die App soll sowohl für die Betriebssysteme iOS und Android entwickelt werden.

#### Ausgangssituation: <br>
In der Vergangheit pflegte der Vertrieb seine Kundenkontakte über eine einfache Desktop-Applikation. Dabei war man jedoch einen Ort gebunden, was bei einer Mobile-App entfallen würde. Also bestand Handlungsbedarf und der Vertrieb hat sich entschieden, seine Kontakte über eine mobile Smartphone-App laufen zu lassen.

#### Zielsetzung: <br>
Für die Zukunft ist es dem Vertrieb daher von großer Bedeutung seine Kundenkontakte mobil auf dem Smartphone abrufen und ändern zu können. Die Mitarbeiter müssen in der Lage sein, die Kontakte schon unterwegs, wenn sie die Kunden besuchen, zu pflegen. Dies vereinfacht die vertriebsinterne Arbeit.

#### Funktionale Anforderungen: <br>
Die Kontakt-App sollte über acht Funktionen verfügen:
Anlegen eines Kontakts, Updaten eines Kontakts und Löschen eines Kontakts,
Anlegen einer Firma, Updaten einer Firma und Löschen einer Firma,
Außerdem sollte man die Beziehung von einem Kontakt zur dazugehörenden Firma Anlegen und Löschen können.

Jeder Kundenkontakt besitzt einen Namen und jede Firma besitzt einen Namen, eine Adresse und die dazugehörigen Mitarbeiter

Vor dem Benutzen der Kontakt-App muss sich der Benutzer einloggen.
Nach einem Login werden allen Benutzern die gleichen Inhalte dargestellt, nämlich eine Seite mit einem Suchfeld, in das man sowohl den Kontakt als auch die Firma eingeben kann. Der Benutzer hat nun die Möglichkeiten die Inhalte anzuschauen und diese aber auch zu Bearbeiten.

Das Navigieren durch die Kontakt-App erfolgt durch das Auswählen eines beliebigen Kontakt oder Firmenfeldes um an weitere Informationen zu gelangen.

Die Daten und Inhalte werden online auf einem Server gespeichert und verwaltet. Der Client kann mit Hilfe einer WebService-Architektur auf die Daten zugreifen.


#### Datenbank

Die referenzielle Integrität der Datenbank sorgt beim Löschen einer Firma für das abhängige Löschen der verknüpften Kontakte.

Des Weiteren sollte die Server-Applikation Time-Outs erkennen und  den Benutzer nach einer längeren Abwesenheit neu einloggen lassen.

#### - Existierende Datenbank mit den Tabellen Kunde und Kontakt.

  Tabelle Firma:
  - Id, Typ: Guid
  - Name, Typ: char(50)
  - PLZ, Typ: char(6)
  - Ort, Typ: char(50)
  - Strasse, Typ: char (50)
  
  Tabelle Kontakt:
  - Id, Typ: Guid
  - Name, Typ: char(50)
  - Vorname, Typ: char(30)

  Tabelle FirmaKontakt:
  - FirmaId, Typ: Guid
  - KontaktId, Typ: Guid

#### - Die Datenbank muss um die Tabelle Benutzer erweitert werden.

  Tabelle Benutzer:
  - Id, Typ: Guid
  - Name, Typ: char(50)
  - Passwort, Typ: char(50)

Das Feld Passwort muss verschlüsselt abgespeichert werden.


#### Server:

Es wird ein Web-Service implementiert, der folgende Methoden umfasst:

- Login(string Name, string Passwort)
<br> Rückgabewert: Session-Id, Typ: Guid

- Logout(Guid sessionId)

- GetAllFirma(Guid sessionId)
<br> Rückgabewert: List<FirmaObject>

- AddFirma(Guid sessionId, object firma)

- UpdateFirma(Guid sessionId, object firma)

- DeleteFirma(Guid sessionId, Guid firmaId)

- GetAllKontakt(Guid sessionId, Guid firmaId)
<br> Rückgabewert: List<KontaktObject>

- AddKontakt(Guid sessionId, Guid firmaId, object Kontakt)

- UpdateKontakt(Guid sessionId, Guid kontaktId)

- DeleteKontakt(Guid sessionId, Guid kontaktId)


#### App (Client):

Login Form, mit Name, Passwort [Abbildung Login-Form]

Firma Form mit einer Liste aller Firmen [Abbildung der Firma-Form]
- Button „Neu“, öffnet Firma Details-Form mit leeren Werten
- Button „Details“, öffnet Details-Form für die selektierte Firma
- Button „Löschen“, löscht die selektierte Firma

Firma Details-Form enthält Kontrollen für die Eingabe der Felder wie Name, PLZ, … [Abbildung der FirmaDetails-Form]
- Button „Kontakte anzeigen“, öffnet Kontakt-Form mit der Liste aller Kontakte dieser Firma
- Button „Speichern“, Speicher die Änderungen

Kotakt-Form mit der Liste aller Kontakte einer Firma [Abbildung der Kontakt-Form]
- Button „Neu“, öffnet Kontakt Details-Form mit leeren Werten
- Button „Details“, öffnet Details-Form für den selektierten Kontakt
- Button „Löschen“, löscht den selektierten Kontakt







#### Nichtfunktionale Anforderungen: <br>
Die Bedienbarkeit der Kontakt-App sollte so einfach wie möglich funktionieren.
Die ganzen Funktionen, die der Benutzer in der Kontakt-App anwenden kann, machen diese immer wieder erweiterbar.

#### Sicherheitsanforderungen: <br>
Die Kontaktdaten müssen vor dem Zugriff vor Dritten geschützt werden, um eine Korrektheit der eingepflegten Daten zu gewährleisten. Das System muss daher eine Benutzer-Verwaltung enthalten und die Client-App mit einem Login geschützt sein.
