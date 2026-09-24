1) Сервис: carmoney-lab — учебный сервис предварительной оценки заявки на заём под ПТС (README:1-7), данные синтетические.
2) Команды запуска и проверки: Makefile — `make up`, `make down`, `make ps`, `make logs`, `make install`, `make test`, `make lint`, `make seed`, `make help` (Makefile:11-52); docker-compose.yml поднимает `backend` (`php -S 0.0.0.0:8080 -t backend/public backend/public/router.php`) и `db` (`mysql:8.0`) на порту 8080 / 3307 (docker-compose.yml:1-45).
3) Решение approve / review / reject считается в `backend/src/Domain/` — там `DecisionEngine.php`, `LtvCalculator.php`, `AssessmentService.php` (а пороги — в `backend/config/rules.php`).

модель: training-2026-09-minimax-m3