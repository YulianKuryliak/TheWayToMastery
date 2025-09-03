# 📌 Лабораторна робота 0 — Налаштування середовища та перевірка інструментів

## 🎯 Мета
- Створити базову структуру проєкту.  
- Налаштувати пакет `twm` у форматі `src/`.  
- Встановити та перевірити інструменти якості коду (Black, Ruff, MyPy, pre-commit).  
- Виконати вправу на виправлення коду.  
- Закомітити та запушити зміни у Git.  

---

## ✅ Завдання

### Крок 1. Структура проєкту
TheWayToMastery/
│  pyproject.toml
│  .pre-commit-config.yaml
│  .gitignore
│  README.md
│
├─ .vscode/
│   ├─ settings.json
│   └─ launch.json
│
├─ src/
│   └─ twm/
│       ├─ __init__.py              # робить twm пакетом
│       │
│       ├─ python/
│       │   ├─ __init__.py          # підпакет python
│       │   └─ greetings.py         # перший модуль
│       │
│       └─ ml/
│           └─ __init__.py          # підпакет ml (поки порожній)
│
└─ labs/
    ├─ python/
    │   └─ lab_0/
    │       ├─ solution.py
    │       └─ hello_bad.py         # вправа на виправлення
    │
    └─ ml/
        └─ lab_1/                   


---

### Крок 2. Налаштування Git
1. Ініціалізувати репозиторій:
   ```bash
   git init
   ```
2. Додати `.gitignore` у корінь:
   ```gitignore
   .venv/
   **/__pycache__/
   *.pyc
   .pytest_cache/
   .vscode/
   ```
3. Зробити перший коміт:
   ```bash
   git add .
   git commit -m "Initial project structure"
   ```

---

### Крок 3. Встановлення інструментів
У віртуальному середовищі виконати:
```bash
pip install black ruff mypy pre-commit
```

---

### Крок 4. Мінімальний код
**`src/twm/python/greetings.py`**
```python
def hello(name: str) -> str:
    return f"Hello, {name}"
```

**`labs/python/lab_0/solution.py`**
```python
from twm.python.greetings import hello

print(hello("Python"))
```

---

### Крок 5. Вправа на виправлення коду
0. Зробити модуль twm видимим для всього проекту:
   pip install -e .

1. У `labs/python/lab_0/hello_bad.py` створити код із помилками:
   ```python
   import math

   def greet(name):
       return "Hello, " + name

   def add(a:int,b:int)->int: return a+b

   print(greet(123))
   ```
2. Виконати перевірки:
   ```bash
   black labs/
   ruff check labs/
   mypy labs/
   ```
3. Виправити так, щоб:
   - Black не змінював код,
   - Ruff не показував попереджень,
   - Mypy підтвердив типи.  

**Очікуваний результат:**
```python
def greet(name: str) -> str:
    return "Hello, " + name


def add(a: int, b: int) -> int:
    return a + b


print(greet("Python"))
```

---

### Крок 6. Налаштування pre-commit
1. Створити `.pre-commit-config.yaml`:
   ```yaml
   repos:
     - repo: https://github.com/psf/black
       rev: 24.8.0
       hooks:
         - id: black

     - repo: https://github.com/astral-sh/ruff-pre-commit
       rev: v0.5.7
       hooks:
         - id: ruff
           args: [--fix]

     - repo: https://github.com/pre-commit/mirrors-mypy
       rev: v1.10.0
       hooks:
         - id: mypy
   ```
2. Установити хуки:
   ```bash
   pre-commit install
   ```
3. Виконати коміт зі змінами:
   ```bash
   git add labs/python/lab_0/hello_bad.py labs/python/lab_0/solution.py
   git commit -m "Add hello exercise"
   ```

---

### Крок 7. Оновлення Git-репозиторію
1. Створити новий репозиторій на GitHub із назвою `TheWayToMastery`.  
2. Підключити remote:
   ```bash
   git remote add origin https://github.com/<твій_логін>/TheWayToMastery.git
   ```
3. Запушити зміни:
   ```bash
   git push -u origin main
   ```

---

## 📌 Контрольні питання
1. Що таке editable install (`pip install -e .`) і навіщо він потрібен?  
2. Для чого використовуються Black, Ruff, Mypy?  
3. Що робить pre-commit?  
4. Чим відрізняється «поганий код» на початку вправи від виправленого?  
5. Чому важливо робити перший коміт і пуш у Git?  
