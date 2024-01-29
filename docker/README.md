# Ćwiczenie 5

Repozytorium ze wszystkim co związane z zadaniem 5: [link](https://github.com/alkatraz445/SIPO_5)


## `Dockerfile`

```dockerfile
# Używamy obrazu Pythona w wersji 3.10,
# który jest lekki (slim).
FROM python:3.10-slim

# Otwarcie i przypisanie portu 7777,
# aby można było korzystać z aplikacji na tym porcie.
EXPOSE 7777

# Ustawiamy zmienną środowiskową,
# aby zapobiec tworzeniu plików pycache.
ENV PYTHONDONTWRITEBYTECODE=1

# Ustawiamy zmienną środowiskową, aby uniknąć buforowania w Pythonie.
ENV PYTHONUNBUFFERED=1

# Kopiujemy plik requirements.txt do obecnego katalogu.
COPY requirements.txt .

# Instalujemy zależności wymienione w pliku requirements.txt.
RUN python -m pip install -r requirements.txt

# Ustawiamy katalog roboczy na /app.
WORKDIR /app

# Kopiujemy wszystkie pliki z obecnego katalogu do katalogu /app w kontenerze.
COPY . /app

# Dodajemy użytkownika o identyfikatorze 5678,
# bez hasła, bez interaktywnego prompta.
# Następnie zmieniamy właściciela katalogu /app na użytkownika appuser.
RUN adduser -u 5678 --disabled-password --gecos "" appuser && chown -R appuser /app

# Ustawiamy użytkownika appuser jako użytkownika,
# który będzie używany do uruchamiania kontenera.
USER appuser

# Komenda, która zostanie wykonana,
# gdy kontener zostanie uruchomiony.
# Uruchamiamy Gunicorn (web server dla Pythona),
# naszej aplikacji na porcie 7777.
CMD ["gunicorn", "--bind", "0.0.0.0:7777", "app:app"]
```

## Aplikacja Flask

Wersja pythona: `3.10`

### `app.py`

```python
from flask import Flask
from datetime import datetime

app = Flask(__name__)

@app.route('/')
def display_info():
    name = "Jakub Kraus"
    index_number = "344120"
    current_datetime = datetime.now().strftime("%Y-%m-%d %H:%M:%S")

    return f"{name}\n{index_number}\n{current_datetime}"

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0', port=7777)


```

### `requirements.txt`

```requirements.txt
flask==3.0.0
gunicorn==20.1.0
```
