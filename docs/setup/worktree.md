# Worktree и параллельные сессии

## `git worktree list`

```text
/Users/kyifut/Documents/SmartHorizon/carmoney-lab                                 3240cbb [d1/1.2.1-1.2.3-kkkyifut]
/Users/kyifut/Documents/SmartHorizon/carmoney-lab/.kilo/worktrees/horse-sink      3240cbb (detached HEAD)
/Users/kyifut/Documents/SmartHorizon/carmoney-lab/.kilo/worktrees/unit-tests-map  3240cbb [unit-tests-map]
```

## Ответ второй сессии

- `LtvCalculatorTest.php` — расчёт LTV в процентах и исключения при нулевой стоимости или неположительной сумме.
- `AssessmentServiceTest.php` — сценарии сервиса: `approve` с лимитом, `review` и `reject` с нулевым лимитом.
- `DecisionEngineTest.php` — выбор `approve` / `review` / `reject` по порогам LTV, включая границы 85.0 и 85.01.
- `VinValidatorTest.php` — формат VIN: длина, запрещённые I/O/Q, регистр, спецсимволы и пустая строка.
- `ApplicationValidatorTest.php` — нормализация VIN, год из будущего, слишком маленькая сумма и сбор ошибок.

Вторая сессия работала в `/Users/kyifut/Documents/SmartHorizon/carmoney-lab/.kilo/worktrees/unit-tests-map` на ветке `unit-tests-map`.

## Почему нужны разные worktree

В одной папке на одной ветке агенты могут одновременно переписать один файл, и изменения одного испортят незакоммиченные изменения другого.
Разные worktree дают отдельные файлы и ветки: каждый агент проверяет свой diff, а изменения объединяются только осознанно.
