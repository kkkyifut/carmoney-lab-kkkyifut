@planner: планировщик. Он может читать код, AGENTS.md и docs/setup/code_map.md, пишет план в docs/plan/. Код не меняет. В плане всегда разделы: Файлы, Шаги, Тесты, Риски. Если данных не хватает — перечисляет, чего не хватает.
@scout: разведчик. Находит в коде то, что просят, и возвращает список: файл, строка, одна фраза — что там. Ничего не меняет и не предлагает исправлений.

Ответ @scout:

Все упоминания `mileage` в коде:

**Backend — чтение/валидация пробега:**
- `backend/src/Domain/ApplicationValidator.php:43` — читает `$payload['mileage']`, кастит в `int`
- `backend/src/Domain/ApplicationValidator.php:44` — сравнивает с `$this->rules['vehicle']['max_mileage_km']`
- `backend/src/Domain/ApplicationValidator.php:45` — формирует ошибку валидации по ключу `'mileage'`
- `backend/src/Domain/ApplicationValidator.php:78` — возвращает нормализованный `'mileage'` в результате

**Backend — пороговое значение (конфиг):**
- `backend/config/rules.php:23` — `'max_mileage_km' => 500000`

**Backend — запись/чтение в БД:**
- `backend/src/Repository/ApplicationRepository.php:19` — тип в PHPDoc параметра (содержит `mileage`)
- `backend/src/Repository/ApplicationRepository.php:38` — `INSERT INTO vehicles (... mileage_km ...)`
- `backend/src/Repository/ApplicationRepository.php:39` — `VALUES (... :mileage ...)`
- `backend/src/Repository/ApplicationRepository.php:45` — биндинг `':mileage' => $input['mileage']`
- `backend/src/Repository/ApplicationRepository.php:68` — `SELECT ... v.mileage_km ...` в выборке заявок

**Frontend:**
- `frontend/app.js:8` — `mileage` в списке `NUMERIC_FIELDS`

**SQL:**
- `db/schema.sql:22` — колонка `mileage_km INT UNSIGNED NOT NULL`
- `db/seed.sql:31` — `INSERT INTO vehicles (... mileage_km ...)`

**Тесты (фикстуры с пробегом, чтение в тестах через массив):**
- `tests/Unit/ApplicationValidatorTest.php:34` — `'mileage' => 84000`
- `tests/Unit/AssessmentServiceTest.php:38` — `'mileage' => 96000`