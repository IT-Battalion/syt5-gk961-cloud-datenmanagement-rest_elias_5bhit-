# Deployment
Zum einfachen testen der Umgebung kann `sail` verwendet werden. Folgende Schritte sind erforderlich:

1. Docker starten.
2. `cp .env.example .env`
3. `composer install`
4. `npm install`
5. `php artisan key:generate`
6. `./vendor/bin/sail up -d`
7. `./vendir/bin/sail migrate`

Danach kann die Authentifizierungs GUI unter `http://localhost` aufgerufen werden.

# Testing
Da alles mit `curl` testbar sein muss, musste ich den XSRF Token für Requests deaktivieren. Dafür habe ich in `config/sanctum.php` und in `app/Http/Kernel.php` die Middleware `VerifyCsrfToken` auskommentiert.

```bash
curl -X POST -d "name=pelias&email=pelias@student.tgm.ac.at&password=YourPasswordHere10&password_confirmation=YourPasswordHere10" http://localhost/register
curl -X POST -d "email=pelias@student.tgm.ac.at&password=YourPasswordHere10!" http://localhost/login
```
