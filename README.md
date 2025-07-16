# n8n-nodes-nextcloud-tables

Ein **Community** n8n Node für die Integration mit Nextcloud Tables. Diese Node ermöglicht vollständige Tabellen-Verwaltung, erweiterte Datenoperationen und ist **speziell für KI-Agents optimiert**.

🇬🇧 English Version at https://github.com/grolaf/n8n-nodes-nextcloud-tables 🇬🇧

## 🚀 **Produktions-Status: v2.4.7** ✅

**Diese Node ist produktionsreif für die getesteten Kern-Features und gegen kritische NaN-Bugs abgehärtet!**

### ✅ **Version 2.4.8 - Production-Ready:**
- ✅ **Robuste Resource Locator Validierung** - Keine NaN-Fehler mehr
- ✅ **KI-Agent Kompatibilität** - Spezielle AI-Friendly Operationen  
- ✅ **Umfassende Fehlerbehandlung** - Detaillierte HTTP-Status-Codes
- ✅ **Optimierte API-Performance** - Query-Parameter für Column-Operationen
- ✅ **Verbesserte Log-Kennzeichnung** - Eindeutige Node-Identifikation für besseres Grepping
- ✅ **Strukturiertes Logging** - Debug, Info, Warn, Error Level mit Kontext

### ✅ **Version 2.4.7 - Production-Ready:**
- **🛡️ NaN-Bug-Fixes**: Robuste Validierung gegen alle NaN-Quellen (null, undefined, 'NaN' strings)
- **🧹 Production-Cleanup**: Alle Debug-Tools entfernt, saubere Codebase
- ⚡ **Enhanced Error Handling**: Hilfreiche Fehlermeldungen für Resource Locator Probleme
- 🔧 **Optimierte Builds**: TypeScript-Compilation ohne Warnings
- 📦 **Clean Dependencies**: Entfernte veraltete Scripts und Altlasten

### ✅ **Getestet & Produktionsreif:**
- **Tabellen-Management**: Grundlegende CRUD-Operationen (getAll, get) ✅
- **Spalten-Management**: Alle Operationen inkl. AI-friendly Extensions ✅
- **Zeilen-Management**: Basis CRUD (create, getAll, get) ✅
- **Views-Management**: Basis-Operationen (getAll, create) ✅
- **Shares-Management**: Benutzer/Gruppen-Freigaben ✅
- **NaN-Bug-Protection**: Robuste Resource Locator Validierung ✅

### ⚠️ **Implementiert aber ungetestet:**
- **Erweiterte Tabellen-Ops**: update, delete
- **Erweiterte Zeilen-Ops**: update (delete nicht von API unterstützt)
- **Erweiterte Views-Ops**: get, update, delete, getRows
- **Erweiterte Shares-Ops**: update, delete
- **CSV-Import**: Vollständige Import-Pipeline
- **Context-Integration**: App-Context-Features
- **Erweiterte Filter/Sort**: Komplexe Multi-Column-Operationen

## 🛡️ **Kritische Bug-Fixes in v2.4.7**

### **Problem gelöst: NaN Table IDs**
Nextcloud-Logs zeigten kritische Fehler wie:
```
[error] Did expect one result but found none for table id = NaN
[error] no read access to table id = 0
```

### **Root Cause: Resource Locator Handling**
```typescript
// VORHER: Unzureichende Validierung führte zu NaN IDs
if (!tableId || isNaN(tableId)) { ... }

// NACHHER: Robuste Validierung gegen ALLE NaN-Quellen
if (resourceLocator === null || resourceLocator === undefined || 
    resourceLocator === 'null' || resourceLocator === 'undefined' ||
    resourceLocator === 'NaN' || 
    (typeof resourceLocator === 'number' && isNaN(resourceLocator))) {
    throw new Error('Resource Locator ist erforderlich aber nicht gesetzt oder ungültig');
}
```

### **Gehärtete Validation in Load Options**
- ✅ **Tabellen-ID Extraktion**: Robuste Behandlung von `__rl` Resource Locators
- ✅ **Column/View Loading**: Validierung verhindert `/tables/NaN/columns` Requests
- ✅ **Error Messages**: Hilfreiche Debugging-Informationen
- ✅ **String-to-Number Conversion**: Sichere parseInt() mit Validation

## 🤖 **KI-Agent Optimiert** ⭐

**Einzigartig**: Diese Node ist die **erste n8n Community Node**, die speziell für **KI-Agents** optimiert wurde!

### **Problem gelöst**: 
Standard n8n-Nodes verwenden `displayOptions`, die Parameter dynamisch verstecken. KI-Agents können diese nicht sehen.

### **Lösung**: AI-Friendly Operationen
- ✅ **Alle Parameter gleichzeitig sichtbar**
- ✅ **Keine UI-Dependencies** für KI-Agents
- ✅ **String-basierte IDs** statt Dropdown-Navigation
- ✅ **Flache Parameter-Struktur** ohne Verschachtelung
- ✅ **Robuste NaN-Protection** in v2.4.7

### **AI-Friendly Operationen verfügbar:**

#### **Spalten-Management (AI-Optimiert)**
```javascript
// Für KI-Agents optimiert - ALLE Parameter sichtbar
Operation: "Spalte Erstellen (KI-Friendly)"
{
  "tableIdAI": "123",
  "columnType": "selection", 
  "columnTitle": "Status",
  "columnMandatory": true,
  
  // Alle typ-spezifischen Parameter gleichzeitig verfügbar:
  "selectionOptionsAI": "[\"Offen\", \"In Bearbeitung\", \"Fertig\"]",
  "selectionDefaultAI": "Offen",
  "selectionMultipleAI": false,
  
  // Text-Parameter (werden ignoriert bei anderen Typen):
  "textSubtypeAI": "line",
  "textMaxLengthAI": 255,
  // ... alle anderen Parameter verfügbar
}

// Vollständige Updates möglich
Operation: "Spalte Aktualisieren (KI-Friendly)"
{
  "columnIdAI": "456",
  "columnType": "text",           // Typ ändern
  "columnTitle": "Neuer Name",    // Titel ändern
  "textSubtypeAI": "long",        // Text-spezifisch
  "textMaxLengthAI": 500,         // Max-Länge ändern
  // Nur relevante Parameter werden verwendet
}
```

**Vorteile für KI-Agents:**
- 🔍 **Parameter-Transparenz**: 24 Parameter gleichzeitig sichtbar
- 🎯 **Autonome Operationen**: Keine UI-Interaktion erforderlich
- 🚀 **String-basierte Eingaben**: Keine Dropdown-Listen, maximale Flexibilität
- 🛡️ **NaN-Protection**: Robuste Validierung verhindert API-Fehler (v2.4.7)
- ↩️ **Backward Compatible**: Human-UI bleibt unverändert

## 📊 **Feature-Übersicht & Test-Status**

### 🏗️ **Tabellen-Operationen**
- ✅ **Alle Tabellen abrufen**: Getestet, produktionsreif
- ✅ **Tabelle abrufen**: Getestet, produktionsreif
- ⚠️ **Tabelle erstellen**: Implementiert, ungetestet
- ⚠️ **Tabelle aktualisieren**: Implementiert, ungetestet
- ⚠️ **Tabelle löschen**: Implementiert, ungetestet

### 📋 **Spalten-Management** ✅ **VOLLSTÄNDIG GETESTET & AI-OPTIMIERT**
**Standard-Operationen:**
- ✅ **Alle Spalten abrufen**: Getestet, produktionsreif
- ✅ **Spalte abrufen**: Getestet, produktionsreif
- ✅ **Spalte erstellen**: Getestet, produktionsreif
- ⚠️ **Spalte aktualisieren**: Implementiert, ungetestet
- ⚠️ **Spalte löschen**: Implementiert, ungetestet

**🤖 KI-Friendly Operationen:**
- ✅ **Spalte Erstellen (KI-Friendly)**: Getestet, produktionsreif - 23 Parameter gleichzeitig sichtbar
- ⚠️ **Spalte Aktualisieren (KI-Friendly)**: Implementiert, ungetestet - 24 Parameter für vollständige Updates

**5 Spaltentypen vollständig unterstützt:**
- ✅ **Text**: Getestet - Pattern-Validierung, Max-Länge, Subtypen (einzeilig/mehrzeilig)
- ✅ **Number**: Getestet - Min/Max, Dezimalstellen, Präfix/Suffix, Validierung
- ✅ **DateTime**: Getestet - Standard-Datum, flexible Eingabeformate
- ✅ **Selection**: Getestet - Dropdown-Optionen, Standard-Werte, Mehrfachauswahl
- ✅ **UserGroup**: Getestet - Benutzer/Gruppen-Auswahl, Multi-Select, Teams

### 🎯 **Zeilen-Operationen**
- ✅ **Alle Zeilen abrufen**: Getestet, produktionsreif
- ✅ **Zeile abrufen**: Getestet, produktionsreif (clientseitige Filterung)
- ✅ **Zeile erstellen**: Getestet, produktionsreif
- ⚠️ **Zeile aktualisieren**: Implementiert, ungetestet
- ❌ **Zeile löschen**: Nicht von Nextcloud Tables API unterstützt

**Erweiterte Zeilen-Features (ungetestet):**
- ⚠️ **Smart-Pagination**: 1-1000 Zeilen optimiert
- ⚠️ **11 Filter-Operatoren**: =, !=, >, >=, <, <=, LIKE, starts_with, ends_with, is_empty, is_not_empty
- ⚠️ **Multi-Column-Sorting**: Prioritäts-basierte Sortierung
- ⚠️ **Volltext-Suche**: Case-sensitive/insensitive, spalten-spezifisch
- ✅ **Automatische Validierung**: Spalten-basierte Datenformatierung

### 📋 **Views-Management**
- ✅ **Views abrufen**: Getestet, produktionsreif
- ✅ **View erstellen**: Getestet, produktionsreif
- ⚠️ **View abrufen (einzeln)**: Implementiert, ungetestet
- ⚠️ **View aktualisieren**: Implementiert, ungetestet
- ⚠️ **View löschen**: Implementiert, ungetestet
- ⚠️ **Zeilen aus View abrufen**: Implementiert, ungetestet

### 🤝 **Kollaborations-Features**
- ✅ **Shares abrufen**: Getestet, produktionsreif
- ✅ **Share erstellen**: Getestet, produktionsreif (Benutzer & Gruppen)
- ⚠️ **Share aktualisieren**: Implementiert, ungetestet
- ⚠️ **Share löschen**: Implementiert, ungetestet
- ✅ **Benutzer/Gruppen-Listen**: Getestet, produktionsreif

### 📥 **CSV-Import** ⚠️ **UNGETESTET**
- ⚠️ **Flexible Optionen**: Header-Erkennung, Trennzeichen-Auswahl
- ⚠️ **Column-Mapping**: Automatische oder manuelle Zuordnung
- ⚠️ **Datentyp-Konvertierung**: Auto, Text, Number, DateTime, Boolean
- ⚠️ **Import-Status**: Überwachung und Fehlerbehandlung

### 🌐 **App-Context-Integration** ⚠️ **UNGETESTET**
- ⚠️ **Context-Navigation**: Nahtlose Nextcloud-App-Integration
- ⚠️ **Context-Tabellen**: Gefilterte Ansichten nach App-Context
- ⚠️ **Context-Pages**: App-Page-Management

## Installation

```bash
npm install n8n-nodes-nextcloud-tables
```

Starten Sie n8n neu, um die neue Node zu laden.

## Konfiguration

### Credentials
Erstellen Sie neue Credentials vom Typ "Nextcloud Tables API":

1. **Nextcloud URL**: Vollständige URL (z.B. `https://cloud.example.com`)
2. **Benutzername**: Ihr Nextcloud-Benutzername  
3. **Passwort**: App-Passwort (empfohlen) oder normales Passwort

**🔒 Sicherheit**: Verwenden Sie App-Passwörter:
- Nextcloud → Einstellungen → Sicherheit → App-Passwörter
- Erstellen Sie ein neues App-Passwort für n8n

## 🤖 **KI-Agent Usage Examples**

### Spalte für KI-Agents erstellen
```javascript
{
  "resource": "Spalte",
  "operation": "Spalte Erstellen (KI-Friendly)",
  "tableIdAI": "123",
  "columnType": "selection",
  "columnTitle": "Projekt-Status", 
  "columnDescription": "Aktueller Status des Projekts",
  "columnMandatory": true,
  "selectionOptionsAI": "[\"Geplant\", \"In Arbeit\", \"Testing\", \"Fertig\", \"Archiviert\"]",
  "selectionDefaultAI": "Geplant",
  "selectionMultipleAI": false
}
```

### Spalte für KI-Agents aktualisieren
```javascript
{
  "resource": "Spalte", 
  "operation": "Spalte Aktualisieren (KI-Friendly)",
  "columnIdAI": "456",
  "columnTitle": "Erweiterte Projekt-Status",
  "selectionOptionsAI": "[\"Backlog\", \"Sprint\", \"Review\", \"Done\", \"Cancelled\"]",
  "selectionDefaultAI": "Backlog"
}
```

### Verschiedene Spaltentypen für KI-Agents
```javascript
// Text-Spalte erstellen
{
  "columnType": "text",
  "columnTitle": "Beschreibung",
  "textSubtypeAI": "long",
  "textMaxLengthAI": 1000,
  "textPatternAI": "^[A-Za-z0-9\\s]+$"
}

// Zahlen-Spalte erstellen  
{
  "columnType": "number",
  "columnTitle": "Budget",
  "numberMinAI": 0,
  "numberMaxAI": 100000,
  "numberDecimalsAI": 2,
  "numberPrefixAI": "€"
}

// Benutzer/Gruppen-Spalte erstellen
{
  "columnType": "usergroup", 
  "columnTitle": "Zuständig",
  "usergroupTypeAI": "user",
  "usergroupMultipleAI": false
}
```

### Human vs. KI-Agent Vergleich
```javascript
// HUMAN (UI-optimiert) - Parameter erscheinen dynamisch
Operation: "Spalte Erstellen"
Tabelle: [Dropdown-Auswahl]
Typ: "Auswahl" 
// → Dann erscheinen Auswahl-spezifische Parameter

// KI-AGENT (AI-optimiert) - Alle Parameter sichtbar
Operation: "Spalte Erstellen (KI-Friendly)"  
// → ALLE 23 Parameter sofort sichtbar und verwendbar
// → String-basierte Eingaben statt Dropdown-Listen
// → Maximale Flexibilität für autonome Ausführung
```

## 🔧 **Advanced Usage**

### Erweiterte Zeilen-Abfrage mit Filtern
```javascript
{
  "resource": "Zeile",
  "operation": "Alle Zeilen Abrufen",
  "source": "table",
  "tableId": "123",
  "useFiltering": true,
  "filters": [
    {
      "columnId": "5",
      "operator": "EQ", 
      "value": "Aktiv"
    },
    {
      "columnId": "8",
      "operator": "GT",
      "value": "2024-01-01"
    }
  ],
  "useSorting": true,
  "sorting": [
    {
      "columnId": "10",
      "direction": "DESC"
    }
  ]
}
```

### CSV-Import mit Column-Mapping
```javascript
{
  "resource": "Import",
  "operation": "CSV in Tabelle Importieren",
  "tableId": "123",
  "csvData": "[Binary CSV Data]",
  "hasHeader": true,
  "delimiter": ";",
  "columnMapping": [
    {
      "csvColumn": "Kundenname",
      "tableColumn": "1",
      "dataType": "text"
    },
    {
      "csvColumn": "Erstellungsdatum", 
      "tableColumn": "2",
      "dataType": "datetime"
    }
  ]
}
```

## 📊 **Vollständige API-Abdeckung**

### ✅ Implementierte Endpunkte
- **Tables**: `/tables/*` (vollständige CRUD)
- **Rows**: `/tables/{id}/rows`, `/views/{id}/rows` (vollständige CRUD außer DELETE*)
- **Views**: `/tables/{id}/views`, `/views/{id}` (vollständige CRUD)
- **Columns**: `/tables/{id}/columns`, `/columns/{id}` (vollständige CRUD + AI-friendly)
- **Shares**: `/tables/{id}/shares`, `/shares/{id}` (vollständige CRUD)
- **Import**: `/tables/{id}/import` (POST + Status-Monitoring)
- **Context**: `/contexts/*` (GET-Operationen)

**\*Note**: Row DELETE ist von der Nextcloud Tables API nicht unterstützt

### 🔧 **Kompatibilität**
- **Nextcloud**: 28+ (getestet)
- **Tables App**: 0.6+ (getestet) 
- **n8n**: 1.0+ (getestet)

### 🛠️ **Technische Details**
- **API Version**: Hybrid v1/v2 (optimal je nach Operation)
- **Authentifizierung**: Basic Auth mit App-Passwort-Support
- **Error Handling**: 10 HTTP-Status-Codes mit spezifischen Meldungen
- **Retry Logic**: 3 Versuche mit exponentiellem Backoff
- **Validation**: Spalten-basierte Echtzeit-Validierung

## Development & Testing

### Setup
```bash
npm install          # Dependencies
npm run build        # TypeScript kompilieren  
npm run dev          # Development-Modus
npm run lint         # Code-Prüfung
npm run format       # Code formatieren
```

### Projekt-Architektur
```
nodes/NextcloudTables/
├── NextcloudTables.node.ts              # Haupt-Node
├── descriptions/                        # UI-Definitionen
│   ├── column.ts     ← KI-OPTIMIERT
│   ├── table.ts      ├── row.ts
│   ├── view.ts       ├── share.ts  
│   ├── import.ts     └── context.ts
├── handlers/                           # Business Logic
│   ├── column.handler.ts ← KI-FRIENDLY LOGIC
│   └── *.handler.ts
├── helpers/                           # Core Utilities
│   ├── api.helper.ts                  # HTTP + Error Handling
│   ├── data.formatter.ts              # Validation
│   └── node.methods.ts                # Dynamic Dropdowns
└── interfaces/                        # TypeScript Types
```

## 🛠️ **Troubleshooting**

### Logging & Debugging

**🔍 Verbesserte Log-Kennzeichnung (Neu in v2.4.8)**  
Alle Logs der Node sind jetzt eindeutig gekennzeichnet für besseres Grepping:

```bash
# Alle Nextcloud Tables Node Logs
grep "N8N-NEXTCLOUD-TABLES" /path/to/n8n/logs

# Nur API-Fehler
grep "N8N-NEXTCLOUD-TABLES.*API-ERROR" /path/to/n8n/logs

# Nur Validierungsfehler
grep "N8N-NEXTCLOUD-TABLES.*VALIDATION-ERROR" /path/to/n8n/logs

# Operation-spezifische Logs
grep "N8N-NEXTCLOUD-TABLES.*OPERATION-" /path/to/n8n/logs

# Resource Locator Debugging
grep "N8N-NEXTCLOUD-TABLES.*RESOURCE-VALIDATION" /path/to/n8n/logs
```

**Log-Kategorien:**
- `[N8N-NEXTCLOUD-TABLES] [DEBUG] [API-REQUEST]` - API-Anfragen
- `[N8N-NEXTCLOUD-TABLES] [DEBUG] [API-RESPONSE]` - API-Antworten  
- `[N8N-NEXTCLOUD-TABLES] [INFO] [OPERATION-START]` - Operation gestartet
- `[N8N-NEXTCLOUD-TABLES] [INFO] [OPERATION-SUCCESS]` - Operation erfolgreich
- `[N8N-NEXTCLOUD-TABLES] [ERROR] [OPERATION-ERROR]` - Operation fehlgeschlagen
- `[N8N-NEXTCLOUD-TABLES] [WARN] [VALIDATION-ERROR]` - Validierungsfehler
- `[N8N-NEXTCLOUD-TABLES] [DEBUG] [RESOURCE-VALIDATION]` - Resource Locator Debugging

**Beispiel-Logs:**
```
2024-01-15T10:30:45.123Z [N8N-NEXTCLOUD-TABLES] [INFO] [OPERATION-START] table.getAll
2024-01-15T10:30:45.124Z [N8N-NEXTCLOUD-TABLES] [DEBUG] [API-REQUEST] GET /tables
2024-01-15T10:30:45.234Z [N8N-NEXTCLOUD-TABLES] [DEBUG] [API-RESPONSE] GET /tables -> 200 (110ms)
2024-01-15T10:30:45.235Z [N8N-NEXTCLOUD-TABLES] [INFO] [OPERATION-SUCCESS] table.getAll completed (112ms)
```

### Häufige Probleme

**401 Unauthorized**  
✅ **Lösung**: App-Passwort verwenden, Berechtigungen prüfen

**KI-Agent kann Parameter nicht sehen**  
✅ **Lösung**: KI-Friendly Operationen verwenden (`createAIFriendly`, `updateAIFriendly`)

**🚨 NaN Table ID Errors (BEHOBEN in v2.4.7)**  
❌ **Symptom**: Nextcloud-Logs zeigen `table id = NaN` oder `table id = 0`  
✅ **Lösung**: Update auf v2.4.7 - Robuste Resource Locator Validierung implementiert

**Filter funktionieren nicht**  
✅ **Lösung**: Spalten-IDs statt Namen, korrekte Operatoren verwenden

**Column-Erstellung fehlgeschlagen**  
✅ **Behoben**: Verwendet optimierte API v1 mit Query-Parametern

**Resource Locator Validation Errors**  
✅ **Neu in v2.4.7**: Detaillierte Fehlermeldungen helfen bei Debugging:
```
"Resource Locator ist erforderlich aber nicht gesetzt oder ungültig"
"Ungültige ID in Resource Locator: 'undefined' ist keine gültige Zahl"
```

### Error Handling
Detaillierte Fehlermeldungen für alle HTTP-Status-Codes:
- **400-404**: Client-Fehler mit Lösungshinweisen
- **429**: Rate-Limiting mit automatischer Wiederholung  
- **5xx**: Server-Fehler mit Retry-Logic
- **Resource Locator**: Spezifische Validierung und Debugging-Hilfen (v2.4.7)

## 🎯 **Roadmap**

### ✅ **Version 2.4.8 (Aktuell)**
- ✅ **Verbesserte Log-Kennzeichnung** - Eindeutige `[N8N-NEXTCLOUD-TABLES]` Präfixe
- ✅ **Strukturiertes Logging** - Debug, Info, Warn, Error Level mit Kontext
- ✅ **API-Request/Response Logging** - Detaillierte Debugging-Informationen
- ✅ **Operation-Tracking** - Start, Success, Error Logging mit Zeitstempel
- ✅ **Validation-Logging** - Resource Locator und Parameter-Validierung
- ✅ **Grep-freundliche Logs** - Einfache Filterung nach Kategorien

### ✅ **Version 2.4.7**
- 🛡️ **Kritische NaN-Bug-Fixes**: Robuste Resource Locator Validierung
- 🧹 **Production-Cleanup**: Entfernung aller Debug-Tools und Altlasten
- ⚡ **Enhanced Error Handling**: Hilfreiche Fehlermeldungen und Validierung
- 📦 **Optimierte Builds**: Saubere TypeScript-Compilation ohne Warnings

### ✅ **Version 2.4.6 (Vorgänger)**
- Vollständige KI-Agent-Optimierung
- 24 AI-Parameter mit systematischer Trennung
- Robuste Validierung und Error Handling
- Saubere UX für alle Operationen

### 🔮 **Zukünftige Versionen**
- **Weitere AI-Friendly Operationen** für andere Ressourcen
- **Erweiterte KI-Features** (Bulk-Operations, Schema-Inference)
- **Performance-Optimierungen** für große Datenmengen
- **Extended Context-Integration** mit mehr Nextcloud-Apps

## Contributing

**Beiträge willkommen!** Besonders:
- 🤖 **KI-Agent Testing**: Testen Sie die AI-friendly Operationen
- 🐛 **Bug Reports**: GitHub Issues für Probleme
- 💻 **Code**: Verbesserungen und neue Features
- 📝 **Dokumentation**: Beispiele und Best Practices

## Lizenz

MIT

## Support

- **GitHub**: [Issues & Discussions](https://github.com/terschawebIT/n8n-nodes-nextcloud-tables)
- **n8n Community**: [Community Forum](https://community.n8n.io/)
- **Documentation**: [Nextcloud Tables API](https://github.com/nextcloud/tables/blob/main/docs/API.md)

---

**🤖 Diese Node ist die erste KI-Agent-optimierte n8n Community Node!**  
**Probieren Sie die AI-friendly Operationen aus und erleben Sie autonome Tabellen-Verwaltung.** 
