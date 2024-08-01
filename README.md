TEST ASTRO PROJECT AND MELTANO
===

### 1. Check Piton/UloKatok
```
python3 --version
```

### 2. Making Pirtual Enpironmen
```
python3 -m venv venvtest
source venvtest/bin/activate
```

### 3. Install AstroBoy
```
curl -sSL install.astronomer.io | sudo bash -s -- v1.28.0
```
- Upgrade to latest version :
```
curl -sSL install.astronomer.io | sudo bash -s
```
- Create Project
```
mkdir astroboy-project
cd astroboy-project
astro dev init
```

### 4. Install Metanol
```
pip install --upgrade pip
pip install "meltano"
```
- Create Metanol Project
```
cd ..
meltano init my-metanol-project
cd my-metanol-project
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
      user: myuser
      password: mypassword
      dbname: mydatabase
  loaders:
  - name: target-postgres
    config:
      host: localhost
      port: 5432
      user: myuser
      password: mypassword
      dbname: mydatabase
```

#### or

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
        # Lokasi file CSV yang akan diekstrak
        path: /path/to/your/data.csv
        # Opsi tambahan, misalnya delimiter
        delimiter: ","
```
b. Loaders `target-jsonl`
```
plugins:
  loaders:
    - name: target-jsonl
      config:
        # Direktori output untuk file JSONL
        output_dir: /path/to/output/directory
        # Apakah akan menimpa file yang ada
        overwrite: true
```
c. Transformer `dbt`
```
plugins:
  transformers:
    - name: dbt
      config:
        # Direktori yang berisi profil dbt
        profiles_dir: /path/to/dbt/profiles
        # Direktori proyek dbt
        project_dir: /path/to/dbt/project
```

### 5. Continue...