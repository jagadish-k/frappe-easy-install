# Frappe/ERPNext Easy Install Script

A Python script to simplify the installation, deployment, and management of Frappe/ERPNext using Docker containers.

## Features

- 🐳 One-command production setup with Docker
- 🔄 Easy upgrades for existing installations
- 🛠️ Development environment setup
- � Generate configuration files without starting containers
- 🔧 Custom image building capabilities
- 🔐 Automatic password generation and management
- ⚡ Multiple site creation with app installation
- 🔄 Database migrations
- 📦 Backup scheduling support

## Prerequisites

- Python 3.6+
- Docker and Docker Compose (will be installed automatically if missing on Linux)
- Git (for development setup)

## Installation

1. Download the script:
   ```bash
   curl -O https://gist.githubusercontent.com/your-username/gist-id/raw/easy-install.py
   ```

2. Make it executable:
   ```bash
   chmod +x easy-install.py
   ```

## Usage

### Basic Commands

```bash
./easy-install.py [command] [options]
```

### Available Commands

| Command    | Description                                      |
|------------|--------------------------------------------------|
| `deploy`   | Set up a production instance                    |
| `develop`  | Set up a development environment                |
| `upgrade`  | Upgrade an existing installation                |
| `exec`     | Access the backend container shell              |
| `generate` | Generate config files without starting containers|
| `build`    | Build custom Docker images                      |

### Common Options

These options are available for most commands:

| Option              | Description                                      |
|---------------------|--------------------------------------------------|
| `-n, --project`     | Project name (default: "frappe")                |
| `-v, --version`     | ERPNext version to install                      |
| `-i, --image`       | Custom image name                               |
| `-g, --backup-schedule` | Backup cron schedule (default: "@every 6h")   |
| `-m, --http-port`   | HTTP port for no-SSL setup (default: 8080)      |
| `-q, --no-ssl`      | Disable HTTPS                                   |
| `--no-proxy`        | Disable proxy/reverse proxy                     |

### Production Deployment

```bash
./easy-install.py deploy \
  -n my-erpnext \
  -s erp.example.com \
  -e admin@example.com \
  -v version-14 \
  -a erpnext
```

Options specific to `deploy`:
- `-s, --sitename`: Site domain(s) (can specify multiple)
- `-e, --email`: Email for SSL certificates
- `-a, --app`: App(s) to install (can specify multiple)

### Development Setup

```bash
./easy-install.py develop -n my-dev-env
```

### Upgrade Existing Installation

```bash
./easy-install.py upgrade -n my-erpnext -v version-14
```

### Generate Configuration Files

```bash
./easy-install.py generate \
  -n my-config \
  -s site1.example.com \
  -e admin@example.com \
  -o /path/to/output
```

Options specific to `generate`:
- `-o, --output-dir`: Output directory for generated files

### Build Custom Images

```bash
./easy-install.py build \
  -n my-build \
  -r https://github.com/your/frappe \
  -b custom-branch \
  -t myorg/custom-apps:latest \
  -x
```

Options specific to `build`:
- `-p, --push`: Push image after build
- `-r, --frappe-path`: Frappe repository URL
- `-b, --frappe-branch`: Frappe branch to use
- `-j, --apps-json`: Path to apps.json
- `-t, --tag`: Image tag(s) (can specify multiple)
- `-c, --containerfile`: Path to Containerfile
- `-y, --python-version`: Python version
- `-d, --node-version`: Node.js version
- `-x, --deploy`: Deploy after build
- `-u, --upgrade`: Upgrade after build

## Generated Files

When using the `generate` command or during deployment, the script creates:

1. `[project].env` - Environment variables configuration
2. `[project]-compose.yml` - Docker Compose file
3. `[project]-passwords.txt` - Contains generated passwords

## Examples

### Basic Production Setup

```bash
./easy-install.py deploy \
  -n my-erpnext \
  -s erp.example.com \
  -e admin@example.com \
  -a erpnext
```

### Development Environment

```bash
./easy-install.py develop -n my-dev
```

### Generate Config Files Only

```bash
./easy-install.py generate \
  -n staging \
  -s staging.example.com \
  -e admin@example.com \
  -o ~/erpnext-configs
```

### Build and Deploy Custom Image

```bash
./easy-install.py build \
  -n custom \
  -r https://github.com/your/frappe \
  -b version-14 \
  -t myorg/custom-erpnext:latest \
  -x \
  -s custom.example.com \
  -e admin@example.com
```

## Notes

1. On first run, the script will clone the `frappe_docker` repository.
2. For production setups, avoid using "example.com" in email addresses.
3. Passwords are automatically generated and saved in `[project]-passwords.txt`.
4. For development setups, additional configuration may be needed as per Frappe documentation.

## Troubleshooting

Check the `easy-install.log` file for detailed error information if something goes wrong.
