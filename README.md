# tts

Cookiecutter based tts process

---

## Spis treści
1. [Wymagania wstępne](#wymagania-wstępne)
2. [Instalacja pipx](#instalacja-pipx)
3. [Instalacja Poetry](#instalacja-poetry)
4. [Alternatywa: virtualenv i pip](#alternatywa-virtualenv-i-pip)
5. [Uruchamianie projektu](#uruchamianie-projektu)
6. [Tworzenie pluginów](#tworzenie-pluginów)
7. [Materiały dodatkowe](#materiały-dodatkowe)

---

## Wymagania wstępne
- Python 3.8+
- pipx (zalecane)
- Poetry (zalecane)

## Instalacja pipx

### macOS
```bash
brew install pipx
pipx ensurepath
```

**Dodatkowe (opcjonalne) komendy:**
```bash
sudo pipx ensurepath --global
sudo pipx ensurepath --prepend
```

Więcej: [Customising your installation](https://pipx.pypa.io/stable/installation/)

### Linux
#### Ubuntu 23.04 lub nowszy
```bash
sudo apt update
sudo apt install pipx
pipx ensurepath
```
#### Fedora
```bash
sudo dnf install pipx
pipx ensurepath
```
#### Inne dystrybucje
```bash
python3 -m pip install --user pipx
python3 -m pipx ensurepath
```

**Dodatkowe (opcjonalne) komendy:**
```bash
sudo pipx ensurepath --global
sudo pipx ensurepath --prepend
```

### Windows
#### Scoop
```powershell
scoop install pipx
pipx ensurepath
```
#### pip
```powershell
py -m pip install --user pipx
```
Jeśli pojawi się ostrzeżenie o PATH, uruchom:
```powershell
.\pipx.exe ensurepath
```

---

## Instalacja Poetry

### Linux/macOS
```bash
curl -sSL https://install.python-poetry.org | python3 -
pip install poetry
sudo apt install python3-poetry
```
### Windows (PowerShell)
```powershell
(Invoke-WebRequest -Uri https://install.python-poetry.org -UseBasicParsing).Content | python -
pip install poetry
```
Po instalacji sprawdź:
```bash
poetry --version
```

---

## Alternatywa: virtualenv i pip
Jeśli nie chcesz używać Poetry:
```bash
python -m venv venv
# Linux/macOS:
source venv/bin/activate
# Windows:
venv\Scripts\activate
```

---

## Uruchamianie projektu

1. Zainstaluj zależności:
```bash
poetry install
```
2. Aktywuj środowisko:
```bash
poetry shell
```
3. Uruchom projekt zgodnie z instrukcją w sekcji Usage lub Development.

---

## Tworzenie pluginów
1. Utwórz nowy moduł w `process/plugins/`
2. Zaimplementuj klasę dziedziczącą po `ProcessBase`
3. Zarejestruj plugin w `PluginRegistry`

Szczegóły: [Developer Guide](docs/developer_guide.md)

---

## Materiały dodatkowe
- [Oficjalna dokumentacja pipx](https://pipx.pypa.io/)
- [Oficjalna dokumentacja Poetry](https://python-poetry.org/docs/)

### Installing pipx
On macOS:

brew install pipx
pipx ensurepath

Additional (optional) commands

To allow pipx actions in global scope.

sudo pipx ensurepath --global

To prepend the pipx bin directory to PATH instead of appending it.

sudo pipx ensurepath --prepend

For more details, refer to Customising your installation.
On Linux:

    Ubuntu 23.04 or above

sudo apt update
sudo apt install pipx
pipx ensurepath

    Fedora:

sudo dnf install pipx
pipx ensurepath

    Using pip on other distributions:

python3 -m pip install --user pipx
python3 -m pipx ensurepath

Additional (optional) commands

To allow pipx actions in global scope.

sudo pipx ensurepath --global

To prepend the pipx bin directory to PATH instead of appending it.

sudo pipx ensurepath --prepend

For more details, refer to Customising your installation.
On Windows:

    Install via Scoop:

scoop install pipx
pipx ensurepath

    Install via pip (requires pip 19.0 or later)

# If you installed python using Microsoft Store, replace `py` with `python3` in the next line.
py -m pip install --user pipx

It is possible (even most likely) the above finishes with a WARNING looking similar to this:

WARNING: The script pipx.exe is installed in `<USER folder>\AppData\Roaming\Python\Python3x\Scripts` which is not on PATH

If so, go to the mentioned folder, allowing you to run the pipx executable directly. Enter the following line (even if you did not get the warning):

.\pipx.exe ensurepath

This will add both the above mentioned path and the %USERPROFILE%\.local\bin folder to your search path. Restart your terminal session and verify pipx does run.





Install Poetry

pipx install poetry

Install Poetry (advanced)
You can skip this step, if you simply want the latest version and already installed Poetry as described in the previous step. This step details advanced usages of this installation method. For example, installing Poetry from source, having multiple versions installed at the same time etc.

pipx can install different versions of Poetry, using the same syntax as pip:

pipx install poetry==1.8.4

pipx can also install versions of Poetry in parallel, which allows for easy testing of alternate or prerelease versions. Each version is given a unique, user-specified suffix, which will be used to create a unique binary name:

pipx install --suffix=@1.8.4 poetry==1.8.4
poetry@1.8.4 --version

pipx install --suffix=@preview --pip-args=--pre poetry
poetry@preview --version

Finally, pipx can install any valid pip requirement spec, which allows for installations of the development version from git, or even for local testing of pull requests:

pipx install --suffix @main git+https://github.com/python-poetry/poetry.git@main
pipx install --suffix @pr1234 git+https://github.com/python-poetry/poetry.git@refs/pull/1234/head

Update Poetry

pipx upgrade poetry

Uninstall Poetry

pipx uninstall poetry




### Installing Poetry

This project uses Poetry for dependency management. To install Poetry:

#### On Linux/macOS:

```bash
# Method 1: Using the official installer
curl -sSL https://install.python-poetry.org | python3 -

# Method 2: Using pip
pip install poetry

# Method 3: On Ubuntu/Debian
sudo apt install python3-poetry
```

#### On Windows (PowerShell):

```powershell
# Method 1: Using the official installer
(Invoke-WebRequest -Uri https://install.python-poetry.org -UseBasicParsing).Content | python -

# Method 2: Using pip
pip install poetry
```

After installation, verify Poetry is installed correctly:

```bash
poetry --version
```

#### Alternative: Using virtualenv and pip

If you prefer not to install Poetry, you can use traditional virtualenv and pip:

```bash
# Create a virtual environment
python -m venv venv

# Activate the virtual environment
# On Linux/macOS:
source venv/bin/activate
# On Windows:
# venv\Scripts\activate

# Install dependencies from requirements.txt
pip install -r requirements.txt
```

### Creating New Modules

The Process system is designed to be modular. Here's how to create and set up new modules:

#### 1. Create a new protocol module (e.g., for a new protocol like GraphQL):

```bash
# Create the directory structure
mkdir -p graphql
cd graphql

# Initialize Poetry for the module
poetry init

# Add dependencies
poetry add fastapi uvicorn graphql-core

# Add development dependencies
poetry add --group dev pytest black isort mypy

# Create basic files
touch server.py client.py .env.example
```

#### 2. Create a new plugin for the Process engine:

```bash
# Navigate to the process directory
cd process

# Create a plugin directory if it doesn't exist
mkdir -p plugins

# Create a new plugin file
touch plugins/my_plugin.py
```

Example plugin implementation in `plugins/my_plugin.py`:

```python
from process.process_base import ProcessBase
from process.plugin_system import register_plugin

class MyPlugin(ProcessBase):
    """Custom processing plugin."""
    
    def process_text(self, text, **options):
        """Process text with custom logic."""
        # Implement your processing logic here
        processed_text = text.upper()  # Example: convert to uppercase
        
        # Create and return a result
        return self.create_result(
            data=processed_text,
            format="text",
            metadata={"plugin": "my_plugin"}
        )

# Register the plugin
register_plugin("my_plugin", MyPlugin)
```

#### 3. Create a new service module with monitoring:

```bash
# Create the directory structure
mkdir -p my_service
cd my_service

# Initialize Poetry for the module
poetry init

# Add dependencies
poetry add prometheus-client healthcheck

# Create basic files
touch server.py client.py .env.example
```

Example `.env.example` for the new service:

```
# My Service Environment Variables
MY_SERVICE_HOST=0.0.0.0
MY_SERVICE_PORT=8080
MY_SERVICE_LOG_LEVEL=INFO
MY_SERVICE_PROCESS_HOST=process
MY_SERVICE_PROCESS_PORT=8000

# Monitoring settings
MY_SERVICE_ENABLE_METRICS=true
MY_SERVICE_METRICS_PORT=9101
MY_SERVICE_HEALTH_CHECK_INTERVAL=30

# Core settings
CORE_LOG_LEVEL=INFO
```

### Adding New Plugins

The Process system can be extended with plugins. To create a new plugin:

1. Create a new module in the `process/plugins/` directory
2. Implement a class that inherits from `ProcessBase`
3. Register the plugin with the `PluginRegistry`

See the [Developer Guide](docs/developer_guide.md) for detailed instructions.

### Creating New Service Interfaces

You can add new service interfaces (e.g., WebSocket) by following the pattern of existing services:

1. Create a new directory for your service
2. Implement a server that connects to the Process engine
3. Implement a client for easy integration

See the [Modular Architecture](docs/modular_architecture.md) documentation for details.

## Testing Modules

Each module in the Process system can be tested independently. Here's how to test different components:

### Testing the Process Engine

```bash
# Navigate to the process directory
cd process

# Run tests with Poetry
poetry run pytest

# Or with traditional pytest if not using Poetry
python -m pytest
```

### Testing Protocol Implementations

```bash
# Example: Testing the gRPC service
cd grpc
poetry run pytest

# Example: Testing the REST API
cd rest
poetry run pytest
```

### Testing Health Checks and Monitoring

Each service exposes health check and metrics endpoints that can be tested:

```bash
# Start the service
cd imap
poetry run python server.py

# In another terminal, test the health endpoint
curl http://localhost:8080/health

# Test the metrics endpoint
curl http://localhost:9101/metrics
```

### End-to-End Testing

Test the entire system with all services running:

```bash
# Start all services with Docker Compose
docker-compose up -d

# Run end-to-end tests
cd tests/e2e_tests
python -m pytest
```

## Documentation

Detailed documentation is available in the `docs/` directory:

- [Developer Guide](docs/developer_guide.md) - Comprehensive guide for developers
- [Modular Architecture](docs/modular_architecture.md) - Details on the system architecture
- [Environment Variables](docs/environment_variables.md) - List of all configuration options
- [API Reference](docs/api_reference.md) - API documentation for all components

## Contributing

Contributions are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Plik pyproject.toml

Projekt korzysta z Poetry do zarządzania zależnościami. Jeśli plik `pyproject.toml` nie istnieje, utwórz go poleceniem:

```bash
poetry init
```

Przykładowa zawartość pliku `pyproject.toml` dla tego projektu:

```toml
[tool.poetry]
name = "tts"
version = "0.1.0"
description = "Cookiecutter based tts process"
authors = ["Twoje Imię <twoj@email.com>"]
license = "MIT"

[tool.poetry.dependencies]
python = ">=3.8,<4.0"
# Dodaj tu zależności projektu, np.:
# numpy = "^1.26.0"
# requests = "^2.31.0"

[tool.poetry.dev-dependencies]
# pytest = "^7.0"

[build-system]
requires = ["poetry-core>=1.0.0"]
build-backend = "poetry.core.masonry.api"
```

Po utworzeniu pliku możesz instalować zależności i zarządzać środowiskiem za pomocą poleceń Poetry opisanych wyżej.

---

## Instalacja

```bash
# Instalacja zależności (jeśli nie została wykonana automatycznie)
poetry install
```




## Uruchamianie











2. Użycie cookiecutter jako alternatywy
Cookiecutter to popularne narzędzie do generowania projektów z szablonów. Możemy stworzyć dedykowany szablon cookiecutter dla projektów TTS.
2.1. Instalacja cookiecutter

```bash
pip install cookiecutter
```

Użycie szablonu z repozytorium GitHub
```bash
cookiecutter gh:pyfunc/cookiecutter
```

lub Użycie lokalnego szablonu
```bash
cookiecutter path/to/cookiecutter-tts-project/
```





```bash
# Ustaw uprawnienia wykonywania dla skryptów
chmod +x hooks/pre_gen_project.py
chmod +x hooks/post_gen_project.py
```
```bash
# Uruchomienie serwisów w kontenerach
make up
```

{% if cookiecutter.components.mcp %}
Aby uruchomić serwer MCP:
```bash
cd mcp
poetry run python mcp_server.py
```
{% endif %}

## Funkcjonalności

- Modularny system z wieloma komponentami
- Wsparcie dla różnych protokołów komunikacyjnych (gRPC, REST, WebRTC, MCP, MQTT, WebSocket)
- Integracja z Model Context Protocol (MCP)
- Narzędzia zapewnienia jakości kodu (Black, isort, Flake8, mypy)
- Automatyczna konfiguracja pre-commit hooks
- Comprehensive Makefile for common tasks
- Konfiguracja Docker i docker-compose (opcjonalnie)

## Konfiguracja

### Konfiguracja szablonu

- Konfiguracja projektu znajduje się w pliku `cookiecutter.json`.

### Konfiguracja środowiska

Wygenerowany projekt używa spójnego systemu zmiennych środowiskowych z prefiksami dla każdego komponentu:

- `CORE_*` - Ustawienia rdzenia frameworka
- `PROCESS_*` - Ustawienia silnika Process
- `GRPC_*` - Ustawienia usługi gRPC
- `REST_*` - Ustawienia usługi REST API
- `MCP_*` - Ustawienia usługi MCP
- `MQTT_*` - Ustawienia usługi MQTT
- `WEBSOCKET_*` - Ustawienia usługi WebSocket
- `LANGCHAIN_*` - Ustawienia integracji LangChain

Można używać jednego pliku `.env` dla całego projektu lub oddzielnych plików dla każdego komponentu:

```bash
# Kopiowanie przykładowych plików środowiskowych
cp .env.example .env

# Lub dla poszczególnych komponentów
cp process/.env.example process/.env
cp grpc/.env.example grpc/.env
cp rest/.env.example rest/.env
cp mcp/.env.example mcp/.env
cp mqtt/.env.example mqtt/.env
cp websocket/.env.example websocket/.env
```

Szczegółowa dokumentacja zmiennych środowiskowych znajduje się w pliku `docs/environment_variables.md`.

## Testy

```bash
make test
```