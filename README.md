# Анализ объявление на сайте Auto.ru

## Знакомство с проектом

## Описание данных:
| Параметр | Тип | Описание    |
| :-- | :-- | :-- |
| `km_age`           | `int`    | пробег |
| `mark`     | `str`    | марка |
| `model`         | `str`    | модель |
| `power`       | `int`   | количество лошадиных сил |
| `segment`         | `str`  | сегмент (`ECONOMY/MEDIUM/PREMIUM`) |
| `state`           | `str`  | состояние автомобиля |
| `transmission`   | `str`    | коробка передач |
| `year`     | `int`    | год выпуска |
| `engine-type`     | `str`    | тип двигателя |
| `type`         | `str`   | тип автомобиля (`suv`) |
| `region`  | `str`    | город продажи |
| `body_type`  | `str`    | тип кузова |
| `color`  | `str`    | цвет |
| `drive_type`  | `str`    | привод |
| `wheell_type`  | `str`    | тип руля (право-/леворульный) |
| `condition`  | `str`    | состояние автомобиля |
| `ownersCount`  | `str`    | количество владельцев |
| `is_customs`  | `str`    | растоможенность |
| `price`  | `int`    | цена автомобиля |


## Очистка и обработка данных

Полный код можно найти в `jupyter notebook` (вставить ссылку).

Первично просматриваем данные.

<img src="img/firstly_look.png" width="600" height="400" />

Просматривая колонки замечаем, что они написанные в разном формате, исправим это.

<img src='img/columns.png' width="600" height="100">

### Переименование колонок
1. engine-type -> engine_type, чтобы соотвестовала единному стилю
2. is_customs -> customs_cleared, чтобы улучшить понимание, что это за фича
3. ownersCount -> owners_count
   
```python
cars = cars.rename(columns={'engine-type': 'engine_type', 'is_customs': 'customs_cleared', "ownersCount": "owners_count"})

# Проверяем изменение 
cars.columns

# Выводит
Index(['item_link', 'km_age', 'mark', 'markName', 'model', 'modelName',
       'power', 'segment', 'state', 'transmission', 'year', 'engine_type',
       'type', 'region', 'body_type', 'color', 'drive_type', 'wheell_type',
       'condition', 'owners_count', 'customs_cleared', 'price'],
      dtype='object')
```

### Вывожу процент заполненных данных

<img src='img/percent_miss_values.png' width="600" height="300">

```python
cars = cars.drop('item_link', axis=1) # Дропаю 100% пропущенную фичу 
```