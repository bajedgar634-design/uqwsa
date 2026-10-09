# Проверка CI

## Событие, ветка и SHA
- Workflow: Python quality
- События: push (main), pull_request, workflow_dispatch
- Ветка: main → ci/boundary
- SHA исходного: <SHA>
- SHA красного: <SHA>
- SHA зелёного: <SHA>

## Красный запуск
- URL: <URL красного run>
- Job: tests (3.11) и tests (3.12)
- Упавший step: Run tests
- Тест: test_at_limit (AssertionError)
- Ожидаемый результат: False на границе 120
- Фактический результат: True (из-за замены > на >=)

## Исправление
- Коммит: "Restore strict SLA boundary"
- Возвращён оператор > в sla.py

## Зелёный запуск на Python 3.11 и 3.12
- URL: <URL зелёного run>
- Оба job зелёные, 6 методов OK

## Два новых сценария
- test_negative_elapsed: is_overdue(-1) → ValueError
- test_unknown_priority: is_overdue(10, "urgent") → ValueError
- Итог: 8 методов, обе версии Python зелёные

## Что автоматическая проверка пока не покрывает
- Не проверяются иные входные типы (строки, None, float)
- Не проверяются версии Python вне матрицы (3.10, 3.13)
- Не проверяется поведение при очень больших числах
- Не проверяется формат вывода / логирование