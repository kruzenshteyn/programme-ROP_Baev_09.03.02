# Пример Python для лабораторной работы № 11

```python
from decimal import Decimal, InvalidOperation

def calculate_total(price, quantity, discount=0):
    try:
        p = Decimal(str(price))
        d = Decimal(str(discount))
    except InvalidOperation as exc:
        raise ValueError("price and discount must be numbers") from exc
    if not isinstance(quantity, int) or isinstance(quantity, bool):
        raise TypeError("quantity must be an integer")
    if p < 0 or quantity <= 0 or not (Decimal(0) <= d <= Decimal(1)):
        raise ValueError("values outside accepted range")
    return (p * quantity * (Decimal(1) - d)).quantize(Decimal('0.01'))

assert calculate_total(100, 2, 0.1) == Decimal('180.00')
assert calculate_total(0, 1, 0) == Decimal('0.00')
for data in [(-1, 1, 0), (100, 0, 0), (100, 2, 1.5)]:
    try:
        calculate_total(*data)
    except ValueError:
        pass
    else:
        raise AssertionError(f"Expected error: {data}")
```

Контрольные тесты показаны как образец; для полного отчёта нужны собственные значения на границах исходного условия и описание ожидаемого поведения.
