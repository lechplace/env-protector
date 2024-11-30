# Env Protector

`env-protector` to Pythonowa paczka, która ułatwia zarządzanie plikami `.env` w projektach Git. Automatyzuje szyfrowanie i odszyfrowywanie plików `.env` przy użyciu hooków Git, zapewniając bezpieczeństwo poufnych danych.

---
## Motywacja

W wielu projektach programistycznych pliki `.env` są używane do przechowywania poufnych informacji, takich jak klucze API, dane logowania do baz danych czy konfiguracje serwisów. Jednak przypadkowe dodanie tych plików do repozytorium Git może prowadzić do poważnych konsekwencji, takich jak wycieki danych czy narażenie infrastruktury na ataki.

**Env Protector** został stworzony, aby:
- Zapewnić automatyczne zabezpieczanie plików `.env` w procesie pracy z Git.
- Zminimalizować ryzyko przypadkowego udostępnienia poufnych informacji.
- Uprościć zarządzanie szyfrowaniem i odszyfrowywaniem plików `.env`, eliminując konieczność ręcznej obsługi.
- Ułatwić współpracę w zespołach, gdzie każdy członek ma dostęp do tych samych, bezpiecznych konfiguracji.

---

## Funkcje

- **Automatyczne szyfrowanie plików `.env`** przy każdym `git commit`.
- **Automatyczne odszyfrowywanie plików `.env`** po `git pull` lub `git merge`.
- Obsługa plików `.env.gpg` przy użyciu GPG (`GNU Privacy Guard`).
- Odczyt hasła GPG z pliku `.env_protector`.
- Dodawanie plików `.env` i `.env_protector` do `.gitignore`.
- **Komenda systemowa `env-protector`** do łatwego konfigurowania hooków.

---

## Instalacja

1. Zainstaluj paczkę za pomocą pip:
   ```bash
   pip install env-protector
   ```

2. Upewnij się, że masz zainstalowane GPG:
   - **Linux/macOS**: GPG jest zazwyczaj preinstalowany. Jeśli nie, zainstaluj go:
     ```bash
     sudo apt install gnupg  # Ubuntu
     brew install gnupg     # macOS
     ```
   - **Windows**: Pobierz [GPG for Windows](https://gnupg.org/download/).

---

## Użycie

1. **Utwórz plik `.env_protector` z hasłem GPG:**
   ```bash
   echo "GPG_PASSWORD=YOURPASS" > .env_protector
   ```

2. **Skonfiguruj hooki Git za pomocą komendy `env-protector`:**
   W terminalu, w katalogu swojego projektu, wykonaj:
   ```bash
   env-protector
   ```

   Komenda ta automatycznie:
   - Dodaje `.env` i `.env_protector` do `.gitignore`.
   - Tworzy hooki `pre-commit` i `post-merge`.

3. **Dodaj plik `.env` do repozytorium:**
   - Utwórz plik `.env` z konfiguracjami:
     ```text
     API_KEY=123456
     SECRET_KEY=my_secret_key
     ```
   - Dodaj plik `.env` do repozytorium:
     ```bash
     git add .env
     git commit -m "Dodano plik .env"
     ```

   Plik `.env` zostanie automatycznie zaszyfrowany jako `.env.gpg`.

4. **Odszyfrowanie pliku `.env`:**
   Po wykonaniu `git pull` lub `git merge` plik `.env.gpg` zostanie automatycznie odszyfrowany.

---

## Przykład działania

1. **Konfiguracja hooków Git:**
   ```bash
   env-protector
   ```

   Wyjście w terminalu:
   ```text
   Konfigurowanie hooków Git...
   Dodano .env do .gitignore.
   Dodano .env_protector do .gitignore.
   Utworzono hook Git: .git/hooks/pre-commit
   Utworzono hook Git: .git/hooks/post-merge
   Konfiguracja zakończona!
   ```

2. **Dodawanie i szyfrowanie pliku `.env`:**
   ```bash
   echo "API_KEY=example_key" > .env
   git add .env
   git commit -m "Szyfrowanie pliku .env"
   ```

3. **Odszyfrowanie pliku `.env`:**
   Po wykonaniu `git pull`:
   ```text
   Rozszyfrowywanie pliku .env.gpg...
   Plik .env został rozszyfrowany.
   ```

---

## Wymagania

- Python >= 3.6
- Zainstalowany GPG

---

## Problemy i pytania

Jeśli napotkasz jakiekolwiek problemy lub masz pytania, utwórz zgłoszenie w repozytorium GitHub.

---

## Licencja

Projekt jest dostępny na licencji [MIT](LICENSE).
