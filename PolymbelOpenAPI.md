# Основные требования

1. 1С должен иметь кнопки для ручной выгрузки данных через Open API.
2. 1С в случае каких-либо изменений (категорий, цветов, характеристик, номенклатуры и прочего) - должен автоматически ходить к Open API сайта.
3. 1С должен иметь кнопки для ручной выгрузки изображений (категорий, номенклатуры) по FTP.
4. 1С должен автоматически выгружать изображения в случае их изменений по FTP.

# File system. FTP

Все изображения отправляем по FTP на сервер с сайтом.<br>
Адрес FTP и данные аутентификации пришлю позже.

<b>Изорбажения выгружаем с перезаписью каталога/всех изображений в каталоге</b>.<br>
Чтобы очистить каталоги от ненужных изображений.

<h2>Категории</h2>

`/public/imgs/categories/[id]/img-name.ext`<br>

`id` - уникальный идентификатор категории.

<h2>Номенклатура</h2>

`/public/imgs/nomenclatures/[nomenclatureId]/[colorId]/img-name.ext`<br>

`nomenclatureId` - уникальный идентификатор номенклатуры.<br>
`colorId` - уникальный идентификатор цвета.

# Open API

Для доступа к API передаём в каждом запросе query параметр `?login=polymebel&password=123`.

<details><summary>Пояснения</summary>

`uniqueId` - уникальный идентификатор записи<br>

`String` - строка<br>
`Number` - число<br>
`Array` - массив<br>
`Boolean` - логическое значение true/false<br>
`null` - нуль<br>
`undefined` - значение не определено<br>

`|` - ИЛИ<br>
`String | Number` - строка или число<br>
`Array<String>` - массив строк<br>
`Array<Array<String>>` - двумерный массив типа String<br>

</details>

<h2>Категории</h2>

<details><summary>POST /openAPI/categories</summary>
Добавляем новую категорию или категории на сайт.

```json
[
  {
    "id": "uniqueId", // String | Number
    "name": "Мебель для персонала", // String
    "parentId": "uniqueId", // String | Number | null | undefined
    "isNode": "true" // Boolean
  }
]
```

</details>

<details><summary>PUT /openAPI/categories</summary>

Обновляем категорию или категории.

```json
[
  {
    "id": "uniqueId", // String | Number
    "name": "Мебель для персонала", // String
    "parentId": "uniqueId", // String | Number | null
    "isNode": "true" // Boolean
  }
]
```

</details>

<details><summary>PUT /openAPI/categories/[id]</summary>

Обновляем категорию.

```json
{
  "id": "uniqueId", // String | Number
  "name": "Мебель для персонала", // String
  "parentId": "uniqueId", // String | Number | null
  "isNode": "true" // Boolean
}
```

</details>

<details><summary>DELETE /openAPI/categories</summary>

Удаляем категории.

```json
["uniqueId", "uniqueId"],
```

Удаляем все категории.

```json
[]
```

</details>

<details><summary>DELETE /openAPI/categories/[id]</summary>

Удаляем категорию точечно.

</details>

<h2>Цвета номенлатуры</h2>

<details><summary>POST /openAPI/nomenclature-colors</summary>

Добавляем список цветов для номенклатуры.

```json
[
  {
    "id": "uniqueId", // Number | String
    "label": "Белый премиум", // String
    "value": "FDFDFD" // String. HEX
  },
  {
    "id": "uniqueId", // Number | String
    "label": "Дуб шамони", // String
    "value": "866C5D" // String. HEX
  }
]
```

</details>

<details><summary>PUT /openAPI/nomenclature-colors/[id]</summary>

Обновляем цвет номенклатуры.

```json
{
  "id": "uniqueId", // Number | String
  "label": "Белый премиум", // String
  "value": "FDFDFD" // String. HEX
}
```

</details>

<details><summary>DELETE /openAPI/nomenclature-colors/[id]</summary>

Удаляем цвет номенклатуры точечно.

</details>

<h2>Номенклатура</h2>

<details><summary>POST /openAPI/nomenclatures</summary>

Добавляем номенклатуру.

```json
[
  {
    "id": "uniqueId", // String | Number
    "article": "К.102", // String | Number
    "description": "Какое-то описание", // String
    "manufacturer": "Юнитекс", // String
    "color": "uniqueId", // Number | String
    "price": "15500", // Number | String
    "quantity": "150", // Number | String Наличие товара доступное для продажи
    "category": ["uniqueId", "uniqueId", "uniqueId"], // Array<String|Number> Перечисление уникальных идентификаторов категорий как местоположение номенклатуры в иерархии
    "characteristics": [
      ["Тип стола", "Прямой"],
      ["Высота", "75"]
    ] // Array<Array<{String, String}>> Двумерный массив с названием и значением характеристики
  }
]
```

</details>

<details><summary>PUT /openAPI/nomenclatures</summary>

Обновляем номенклатуру.

```json
[
  {
    "id": "uniqueId", // String | Number
    "article": "К.102", // String | Number
    "description": "Какое-то описание", // String
    "manufacturer": "Юнитекс", // String
    "color": "uniqueId", // Number | String
    "price": "15500", // Number | String
    "quantity": "150", // Number | String Наличие товара доступное для продажи
    "category": ["uniqueId", "uniqueId", "uniqueId"], // Array<String|Number> Перечисление уникальных идентификаторов категорий как местоположение номенклатуры в иерархии
    "characteristics": [
      ["Тип стола", "Прямой"],
      ["Высота", "75"]
    ] // Array<Array<{String, String}>> Двумерный массив с названием и значением характеристики
  }
]
```

</details>

<details><summary>PUT /openAPI/nomenclatures/[id]</summary>

Обновляем номенклатуру точечно.

```json
{
  "id": "uniqueId", // String | Number
  "article": "К.102", // String | Number
  "description": "Какое-то описание", // String
  "manufacturer": "Юнитекс", // String
  "color": "uniqueId", // Number | String
  "price": "15500", // Number | String
  "quantity": "150", // Number | String Наличие товара доступное для продажи
  "category": ["uniqueId", "uniqueId", "uniqueId"], // Array<String|Number>Перечисление уникальных идентификаторов категорий как местоположениеноменклатуры в иерархии
  "characteristics": [
    ["Тип стола", "Прямой"],
    ["Высота", "75"]
  ] // Array<Array<{String, String}>> Двумерный массив с названием изначением характеристики
}
```

</details>

<details><summary>DELETE /openAPI/nomenclatures</summary>

Удаляем номенклатуру.

```json
["uniqueId", "uniqueId", "uniqueId"]
```

Удаляем всю номенклатуру.

```json
[]
```

</details>

<details><summary>DELETE /openAPI/nomenclatures/[id]</summary>

Удаляем номенклатуру точечно.

</details>
