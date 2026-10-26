# Lab 04: Simple Python Database Connections

| | |
|---|---|
| **Student Name** | Eman Fatima |
| **Registration Number** | 2023-BCS-025 |
| **Section** | A |
| **GitHub Username** | Eman-Fatima-7125 |
| **Ubuntu Identity** | eman-fatima-7125@ubuntu |
| **Lab Number** | 04 |
| **Databases Fork** | https://github.com/Eman-Fatima-7125/Databases |
| **Submission Directory** | `DevOps/Labs/Lab04` |

---

## 1. Overview

This lab shows how a Python program connects to databases using a **username, password, endpoint (host:port) and database name**. A single file, `db_connect.py`, is edited through four stages. Python runs directly on an Ubuntu server, while Docker runs only the databases (MySQL 8.4 and three MongoDB 7.0 instances for dev, test and simulated prod).

Each stage connects, sends a real request and prints which database answered, so the target can be verified from the database itself.

| Stage | Task | Database | Source of connection settings |
|---|---|---|---|
| 1 | Task 4 | MySQL | Values written in the code |
| 2 | Task 5 | MongoDB | Values written in the code |
| 3 | Task 6 | MongoDB | Environment variables via `os.getenv()` |
| 4 | Task 7 | MongoDB | `credentials.ini` via `configparser` |

## 2. Learning Objectives

- Explain the username, password, endpoint and database name used for a connection.
- Connect to MySQL and MongoDB using a short Python program.
- Explain the settings embedded in a MongoDB URI.
- Use `os.getenv()` to run unchanged code against dev, test and simulated prod.
- Use `configparser` to read the same settings from an INI credentials file.
- Confirm the target by reading the environment value stored in the database.
- Capture readable evidence of each connection.

## 3. Repository Structure

```
DevOps/
└── Labs/
    └── Lab04/
        ├── README.md
        ├── Lab4_Solution.pdf
        └── screenshots/
            ├── databases_fork.png
            ├── databases_clone.png
            ├── docker_installation.png
            ├── database_services.png
            ├── database_ports.png
            ├── mysql_hardcoded_connection.png
            ├── mongo_hardcoded_connection.png
            ├── mongo_env_dev.png
            ├── mongo_env_test.png
            ├── mongo_env_prod.png
            ├── credential_files_created.png
            ├── credential_file_permissions.png
            ├── mongo_file_dev.png
            ├── mongo_file_test.png
            └── mongo_file_prod.png

Databases/                  # Separate fork (code lives here)
├── db_connect.py           # The only Python file edited
├── credentials.ini.example # Public dummy values
├── credentials.ini         # Local copy, ignored by Git
├── requirements.txt
├── compose.yaml
└── db-init/
```

## 4. Environment

| Component | Details |
|---|---|
| Operating system | Ubuntu 26.04.1 LTS (x86_64), accessed over SSH |
| Git | 2.53.0 |
| Docker Engine | 29.1.3 (`docker.io` package) plus Docker Compose plug-in |
| Python | 3.14.4 in a virtual environment (`.venv`) |
| Libraries | pymongo 4.19.0, mysql-connector-python 9.7.0, dnspython 2.9.0 |

## 5. Database Endpoints

| Database | Host endpoint | Database name | Username |
|---|---|---|---|
| MySQL | `127.0.0.1:3307` | `school_mysql` | `mysql_student` |
| MongoDB dev | `127.0.0.1:27017` | `school_dev` | `dev_user` |
| MongoDB test | `127.0.0.1:27018` | `school_test` | `test_user` |
| MongoDB simulated prod | `127.0.0.1:27019` | `school_prod` | `prod_user` |

> All credentials are public dummy values for disposable classroom databases. Passwords are intentionally not reproduced in this repository's documentation.

## 6. How to Reproduce

**1. Fork and clone**

```bash
git clone https://github.com/Eman-Fatima-7125/Databases.git
cd Databases
```

**2. Install Docker, Compose and Python**

```bash
sudo apt update -y
sudo apt install -y docker.io curl python3 python3-venv python3-pip
sudo mkdir -p /usr/local/lib/docker/cli-plugins
sudo curl -SL https://github.com/docker/compose/releases/latest/download/docker-compose-linux-x86_64 \
     -o /usr/local/lib/docker/cli-plugins/docker-compose
sudo chmod +x /usr/local/lib/docker/cli-plugins/docker-compose
sudo systemctl start docker
sudo usermod -aG docker $USER      # then sign out and reconnect
```

**3. Prepare Python**

```bash
cd ~/Databases
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

**4. Start the databases**

```bash
docker compose up -d --wait mysql mongo-dev mongo-test mongo-prod
docker compose ps
```

**5. Run the stage you want** (replace `db_connect.py` with that stage's version, then):

```bash
python db_connect.py
```

For the environment-variable stage, export `MONGO_USERNAME`, `MONGO_PASSWORD`, `MONGO_ENDPOINT` and `MONGO_DATABASE` for the chosen profile first. For the credentials-file stage, create and protect the file, then choose a section:

```bash
cp credentials.ini.example credentials.ini
chmod 600 credentials.ini
export APP_ENV=test        # dev | test | prod
python db_connect.py
```

**6. Stop the databases**

```bash
docker compose down
```

## 7. Task Summary

| Task | Description | Evidence |
|---|---|---|
| 1 | Fork and clone the `Databases` repository | `databases_fork.png`, `databases_clone.png` |
| 2 | Install Git, Docker, Docker Compose and Python | `docker_installation.png` |
| 3 | Start the four database containers and inspect ports | `database_services.png`, `database_ports.png` |
| 4 | MySQL connection with values in code | `mysql_hardcoded_connection.png` |
| 5 | MongoDB connection with values in code | `mongo_hardcoded_connection.png` |
| 6 | MongoDB connection using `os.getenv()` (dev, test, prod) | `mongo_env_dev.png`, `mongo_env_test.png`, `mongo_env_prod.png` |
| 7 | MongoDB connection using `credentials.ini` (dev, test, prod) | `credential_files_created.png`, `credential_file_permissions.png`, `mongo_file_dev.png`, `mongo_file_test.png`, `mongo_file_prod.png` |

## 8. Expected Results

| Profile | Database | Port | Environment |
|---|---|---|---|
| MySQL | `school_mysql` | 3307 | dev |
| dev | `school_dev` | 27017 | dev |
| test | `school_test` | 27018 | test |
| prod | `school_prod` | 27019 | prod |

## 9. Key Concepts

- **MongoDB URI:** `mongodb://username:password@endpoint/database`. The database in the URI is also the authentication database in this lab.
- **`ping` command:** creating a client does not contact the server, so `database.command("ping")` sends a real request to prove connectivity.
- **`os.getenv()`:** Python inherits exported shell variables, so the same code can target different environments without edits.
- **`configparser`:** reads named sections from `credentials.ini`. `APP_ENV` selects the section and defaults to `dev` when unset.
- **`chmod 600`:** an INI file stores secrets in plain text, so only the owner may read or write it.

## 10. Exam Evaluation Questions

Predictions, results and explanations for the three exam questions are written in `Lab4_Solution.pdf`:

1. A missing environment variable (`unset MONGO_DATABASE`)
2. Which source the file version reads (`unset APP_ENV`)
3. A wrong password in the file (`[test]` section)

## 11. Security Notes

- `credentials.ini` is ignored by Git and must **never** be committed.
- No passwords, credential-bearing URIs, private keys or tokens are included in the documentation.
- The `prod` environment is a disposable local simulation.

## 12. Deliverables

- `Lab4_Solution.pdf`: full report with identity, fork URL, connection results, captioned screenshots and exam answers.
- `screenshots/`: the 15 required screenshots with exact filenames.
- `README.md`: this file.
