
## Pflichtenheft

> Basierend auf dem Lastenheft werden im Folgenden die Anforderungen und Umsetzungen an das Produkt genauer beschrieben.

#### Zielgruppe: <br> 
Vertriebsmitarbeiter, die in Kunden-Kontakt stehen, um stetige Verfügbarkeit der Kontaktdaten mittels einer App zu haben.

#### Ausgangssituation: <br>
In der Vergangheit pflegte der Vertrieb seine Kundenkontakte über eine Desktop-Applikation im Back-Office. Also bestand Handlungsbedarf seitens des Vertriebs, um online die Kontaktdaten via einer mobile Smartphone-App abzufragen und ändern zu können.

#### Zielsetzung: <br>
Entwicklung von zwei Software-Komponenten.

Server-seitig wird ein WebService implementiert, der alle Methoden für die Verwaltung von Firmen und Kontakten zur Verfügung stellt. Es wir davon ausgegangen, dass die infrastruktuellen Voraussetzungen (Hardware und Anbindung an das Internet, sowie ein Datenbank-Server) bereits zur Verfügung stehen.

Client-seitig wird eine App, die sowohl für die mobilen Betriebssystem Android und iOS zur Verfügung steht, implementiert.

#### Funktionale Anforderungen: <br>
Die Daten und Inhalte werden online auf einem Server gespeichert und verwaltet. Der Client kann mit Hilfe einer WebService-Architektur auf die Daten zugreifen.

Die Navigation in der Kontakt-App erfolgt durch Eingeben eines Passworts beim Login und durch klicken von entsprechenden Buttons, um einen gewünschten Effekt zu erzielen.

##### Datenbank-Schema

##### - Tabellen

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

Die referenzielle Integrität der Datenbank sorgt beim Löschen einer Firma für das abhängige Löschen der verknüpften Kontakte.

  Tabelle Benutzer:
  - Id, Typ: Guid
  - Name, Typ: char(50)
  - Passwort, Typ: char(50)

Das Feld Passwort muss verschlüsselt abgespeichert werden.


##### Server:

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


##### App(Client):

Login Form, mit Name, Passwort

[Abbildung Login-Form]
<br>

Firma Form mit einer Liste aller Firmen
- Button „Neu“, öffnet Firma Details-Form mit leeren Werten
- Button „Details“, öffnet Details-Form für die selektierte Firma
- Button „Löschen“, löscht die selektierte Firma

[Abbildung der Firma-Form]
<br>

Firma Details-Form enthält Kontrollen für die Eingabe der Felder wie Name, PLZ, …
- Button „Kontakte anzeigen“, öffnet Kontakt-Form mit der Liste aller Kontakte dieser Firma
- Button „Speichern“, Speicher die Änderungen

Abbildung der FirmaDetails-Form]
<br>

Kotakt-Form mit der Liste aller Kontakte einer Firma 
- Button „Neu“, öffnet Kontakt Details-Form mit leeren Werten
- Button „Details“, öffnet Details-Form für den selektierten Kontakt
- Button „Löschen“, löscht den selektierten Kontakt

[Abbildung der Kontakt-Form]
<br>

#### Nichtfunktionale Anforderungen: <br>
Die Bedienbarkeit der Kontakt-App sollte so einfach wie möglich erfolgen, die Mitarbeiter sich intuitiv zurecht finden. Daher befinden sich in der Client-App gut sichtbar Buttons. Die so schlichte Bedienbarkeit steigert nicht nur die Look & Feel-Anforderungen, sondern ermöglicht jedem Benutzer einen einfachen Zugang zum System. Es ist zu berücksichtigen, dass auch Mitarbeiter mit Sehbehinderungen die App bedienen können.

#### Sicherheitsanforderungen: <br>
Die Kontaktdaten müssen vor dem Zugriff vor Dritten geschützt werden, um die Korrektheit der eingepflegten Daten zu gewährleisten. Das System muss daher eine Benutzer-Verwaltung enthalten und die Client-App mit einem Login geschützt sein.
Die Server-Applikation wird in der Lage sein, Time-Outs zu erkennen. Die Client-App wird im Time-Out Fall den Benutzer auffordern, ein Re-Login durchzuführen.
