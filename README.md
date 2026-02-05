

## Estructura recomendada del repo

```
sistemas-inteligentes/
├── README.md
├── LICENSE
├── .gitignore
├── CITATION.cff                         # opcional (si lo usáis como proyecto)
├── docs/
│   ├── enunciados/
│   │   ├── practica_01.pdf
│   │   └── practica_02.pdf
│   ├── guia_entorno.md
│   └── rubrica.md
├── scripts/
│   ├── setup_env.sh                     # crea entorno y dependencias
│   ├── run_all_tests.sh
│   └── download_data.sh                 # opcional
├── data/
│   ├── raw/                             # NO subir pesado (usar .gitignore)
│   ├── processed/
│   └── README.md                        # cómo conseguir los datos
├── notebooks/
│   ├── 01_exploracion.ipynb
│   ├── 02_modelado.ipynb
│   └── 03_evaluacion.ipynb
├── src/
│   ├── __init__.py
│   ├── config.py                        # rutas/semillas/params
│   ├── dataset.py
│   ├── features.py
│   ├── models/
│   │   ├── __init__.py
│   │   ├── baseline.py
│   │   └── mlp.py
│   ├── train.py
│   ├── evaluate.py
│   └── predict.py
├── tests/
│   ├── test_dataset.py
│   ├── test_features.py
│   └── test_models.py
├── reports/
│   ├── plantilla_informe.md
│   └── practica_01/
│       ├── informe.pdf
│       └── figuras/
├── requirements.txt                     # o pyproject.toml
└── pyproject.toml                       # recomendado (opcional)
```

---

## `.gitignore` (Python + ML típico)

```gitignore
# Python
__pycache__/
*.pyc
*.pyo
*.pyd
.venv/
venv/
.env

# Jupyter
.ipynb_checkpoints/

# Data (no subir datos pesados)
data/raw/
data/processed/*.csv
data/processed/*.parquet
*.h5
*.hdf5

# Modelos / outputs
runs/
checkpoints/
*.pth
*.pt
*.onnx

# OS / IDE
.DS_Store
.vscode/
.idea/
```

---

## `README.md` completo (plantilla autocontenida)

# Sistemas Inteligentes — Repositorio de Prácticas

Este repositorio agrupa las prácticas y entregables de la asignatura **Sistemas Inteligentes**.
Incluye código, notebooks, tests y documentación para ejecutar y reproducir resultados.

## 1. Contenido
- `src/`: código fuente (dataset, features, modelos, entrenamiento y evaluación)
- `notebooks/`: exploración y experimentos
- `tests/`: pruebas automáticas (pytest)
- `reports/`: informes y figuras
- `docs/`: enunciados, rúbrica y guías
- `data/`: datos (NO subir datasets pesados)

---

## 2. Requisitos
- Python 3.10+ (recomendado 3.11)
- Linux / macOS / Windows (WSL recomendado en Windows)

---

## 3. Instalación (entorno autocontenido)
### Opción A: venv + requirements.txt
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -U pip
pip install -r requirements.txt
````

### Opción B: (si usáis `pyproject.toml`)

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -U pip
pip install -e .
```

---

## 4. Datos

Los datos NO se suben al repositorio.

* Colocar datasets en `data/raw/`
* Si hay script de descarga:

```bash
bash scripts/download_data.sh
```

Más detalles: `data/README.md`

---

## 5. Ejecución

### 5.1 Entrenamiento

```bash
python -m src.train --config configs/baseline.yaml
```

### 5.2 Evaluación

```bash
python -m src.evaluate --checkpoint checkpoints/model.pt
```

### 5.3 Predicción

```bash
python -m src.predict --input data/raw/ejemplo.csv --output outputs/predicciones.csv
```

---

## 6. Tests (obligatorio antes de entregar)

```bash
pytest -q
```

---

## 7. Reproducibilidad

* Fijar semilla en `src/config.py`
* Registrar métricas y resultados en `runs/` (no versionado)
* Guardar modelos en `checkpoints/` (no versionado)

---

## 8. Entrega

La entrega se considera válida si:

1. El repositorio incluye este README actualizado.
2. Se puede instalar y ejecutar sin pasos ocultos.
3. Incluye informe en `reports/<practica>/informe.pdf`.
4. `pytest` pasa (si aplica) o se justifica lo que no aplique.

---

## 9. Autoría

* Alumno/a 1: Nombre Apellidos


---

## `requirements.txt` típico (Sistemas Inteligentes)
```txt
numpy
pandas
scikit-learn
matplotlib
opencv-python
tqdm
pyyaml
pytest
````

---

## Comandos para crear el repo (rápido)

```bash
mkdir -p sistemas-inteligentes/{docs/enunciados,docs,script,data/raw,data/processed,notebooks,src/models,tests,reports}
touch sistemas-inteligentes/{README.md,LICENSE,.gitignore,requirements.txt}
touch sistemas-inteligentes/src/{__init__.py,config.py,dataset.py,features.py,train.py,evaluate.py,predict.py}
touch sistemas-inteligentes/src/models/{__init__.py,baseline.py,mlp.py}
```
