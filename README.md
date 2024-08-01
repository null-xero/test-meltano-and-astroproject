TEST ASTRO PROJECT AND MELTANO
===

## 1. Check Piton/UloKatok
```
python3 --version
```

## 2. Making Pirtual Enpironmen
```
python3 -m venv venvtest
source venvtest/bin/activate
```

## 3. Install AstroBoy
```
curl -sSL install.astronomer.io | sudo bash -s -- v1.28.0
```
- Upgrade to latest version :
```
curl -sSL install.astronomer.io | sudo bash -s
```
- Create Project
```
cd astroboy_project
astro dev init
```

## 4. Install Metanol `THERE ARE TWO OPTIONS`
```
pip install --upgrade pip
pip install "meltano"
```
- Create Metanol Project
```
cd ..
cd my_metanol_project
meltano init
```
- Add Plugin Metanol
1.  Plugin Extractor & Loader `postgres`
```
meltano add extractor tap-postgres
meltano add loader target-postgres
```
2. Edit file `meltano.yml` in directory `my-metanol-project` for config plugin
```
plugins:
  extractors:
  - name: tap-postgres
    config:
      host: localhost
      port: 5432
      user: meltano
      password:
      dbname: mydatabase
  loaders:
  - name: target-postgres
    config:
      host: localhost
      port: 5432
      user: meltano
      password:
      dbname: mydatabase
```

# or

1. Plugin Extractor `csv`, Loader `jsonl`, & Transformer `dbt`
```
meltano add extractor tap-csv
meltano add loader target-jsonl
meltano add transformer dbt
```
2. Edit file `meltano.yml` in directory `my-metanol-project` for config plugin
```
version: 1
plugins:
  extractors:
    - name: tap-csv
      config: {}
  loaders:
    - name: target-jsonl
      config: {}
  transformers:
    - name: dbt
      config: {}
```
* Note: The `{}` sign can be filled in as in the section below

a. Extractors `tap-csv`
```
plugins:
  extractors:
    - name: tap-csv
      config:
        # Location of the CSV file to extract
        path: /path/to/your/data.csv
        # Additional options, for example delimiter
        delimiter: ","
```
b. Loaders `target-jsonl`
```
plugins:
  loaders:
    - name: target-jsonl
      config:
        # Output directory for JSONL files
        output_dir: /path/to/output/directory
        # Whether to overwrite existing files
        overwrite: true
```
c. Transformer `dbt`
```
plugins:
  transformers:
    - name: dbt
      config:
        # Directory containing dbt profiles
        profiles_dir: /path/to/dbt/profiles
        # Dbt project directory
        project_dir: /path/to/dbt/project
```

## 5. Open Airplaw
Open url: http://localhost:8080/ for Airflow UI
- USERNAME: `admin`
- PASSWORD: `admin`