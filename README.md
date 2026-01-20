# Dokumentacja Projektu ELK (PBD)

Ten projekt zawiera konfigurację środowiska Elasticsearch, Logstash i Kibana (ELK Stack) przygotowaną do uruchomienia za pomocą Docker Compose. Służy on do przetwarzania, analizy i wizualizacji danych.

## Struktura plików i katalogów

Poniżej znajduje się opis zawartości poszczególnych folderów i plików w projekcie.

### Główny katalog

- **`docker-compose.yml`**: Główny plik orkiestracji usług Docker. Definiuje i uruchamia trzy kontenery:
  - `elasticsearch`: Baza danych i silnik wyszukiwania.
  - `kibana`: Interfejs graficzny do wizualizacji danych i zarządzania Elasticsearch.
  - `logstash`: Narzędzie do pobierania, przetwarzania i wysyłania danych do Elasticsearch.

### `logstash/`

Katalog montowany do kontenera Logstash, zawierający konfiguracje pipeline'ów oraz pliki danych.

- **`logstash.conf`**: Główny plik konfiguracyjny (pipeline), który definiuje wejścia (inputs), filtry (filters) i wyjścia (outputs) dla Logstasha.
- **`logstash-*.conf`** (np. `logstash-apache.conf`, `logstash-warehouse.conf`): Pliki konfiguracyjne dla zadań.
- **`vgsales.csv`**: Plik CSV z danymi o sprzedaży gier wideo, używany jako źródło danych.
- **`web_access.log`**: Plik z logami dostępu serwera WWW, używany jako źródło danych.
- **`blacklist.yml`**: Plik YAML zawierający listę (słownik) wykluczonych lub specjalnych wartości, wykorzystywany przez filtry Logstasha.

### `extras/`

Folder z materiałami dodatkowymi i dokumentacją.

- **`Endpointy CAT API.pdf`**: Dokumentacja techniczna opisująca endpointy `_cat` API w Elasticsearch, które służą do szybkiego podglądu stanu klastra, indeksów itp.

### `helpers/`

Folder z plikami pomocniczymi.

- **`games.json`**: Przykładowe dane w formacie JSON do bezpośredniego importu do Elasticsearch, w przypadku błędu importu z CSV.
- **`export.ndjson`**: Plik eksportu z Kibany. Zawiera zapisane obiekty, takie jak wizualizacje, dashboardy czy wzorce indeksów, który można zaimportować w Kibanę w przypadku błędnej konfiguracji przez studenta.

### `solutions/`

Katalog zawierający wzorcowe lub przykładowe rozwiązania konfiguracji.

- **`logstash/`**: Zawiera gotowe, działające pliki konfiguracyjne (`.conf`) dla różnych zadań (np. `security.conf`, `warehouse.conf`, `custom.conf`), które mogą służyć jako referencja lub gotowe rozwiązania do laboratoriów.
- **`kibana/`**, **`elasticsearch/`**: Zawierają odpowiednio konfiguracje i materiały dla zadań z tych technologii.

## Uruchomienie środowiska

Aby uruchomić cały stos ELK, należy wykonać poniższe polecenie w głównym katalogu projektu:

```bash
docker-compose up -d
```

Po uruchomieniu usługi będą dostępne pod adresami:

- **Kibana**: [http://localhost:5601](http://localhost:5601)
- **Elasticsearch**: [http://localhost:9200](http://localhost:9200)
