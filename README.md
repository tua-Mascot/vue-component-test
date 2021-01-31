### Vue practice. Test task.
<p align="center" width="100%">
    <img width="40%" src="https://i.imgur.com/7SnWTJm.png"> 
</p>

<details>
  <summary>Specification</summary>

Тестовое задание для Front-end

На базе JSON-структуры:
```json
{
  displaySettings: {
    subType:"condition",
    type:"followers",
  },
  elements: [
    {
      type:"rule",
      condition: {
	  entity:"contact",
        field:"followers",
        operand:"lt",
        value:5000,
      },
      onFail: {
        action:"fallthrough"
      },
      onMatch:  {
        action:"goto",
        target:"5e26e98027b2c58a70085d4f"
      }
    },
    {
      type:"rule",
      condition: {
	  entity:"contact",
        field:"followers",
        operand:"lt",
        value:15000,
      },
      onFail: {
        action:"goto",
        target:"5e26e98027b2c58a70085d4e"
      },
      onMatch:  null
    }
  ]
}
```

Сделать компонент в Vue, как на картинке: <br>
![](https://i.imgur.com/UOyHK3M.png)

По кнопке “+ Add value” добавляется такая же структура как у последнего элемента в массиве elements, но: <br>
    • c onMatch равным null <br>
    • значение свойства onFail для него нужно взять у предыдущего последнего элемента <br>
    • а у того элемента, с к-го берётся значение onFail, нужно заменить его на { action: “fallthrough”} <br>

У каждого элемента кроме “Followers count is” должно быть можно задать значение для поля  condition.value через input-элемент в этой области: <br>
![](https://i.imgur.com/Cx0MKEg.png) <br>
Также элемент можно удалить: <br>
![](https://i.imgur.com/OCIWGO5.png)

Нельзя удалить элемент в случае, если он один в списке и onFail также должен оставаться на последнем элементе.

Верстку делать не обязательно, но будет плюсом.

Пример <br>
Исходная структура - на 2 элемента, “less than 5000”, и “5000 or greater”
```json
{
  displaySettings: {
    subType:"condition",
    type:"followers",
  },
  elements: [
    {
      type:"rule",
      condition: {
	  entity:"contact",
        field:"followers",
        operand:"lt",
        value:5000,
      },
      onFail: {
        action:"goto",
        target:"5e26e98027b2c58a70085d4e"
      },
      onMatch:  {
        action:"goto",
        target:"5e26e98027b2c58a70085d4f"
      }
    },
  ]
}
```

После добавления элемента - “less than 5000”, “less than 15000” и “15000 or greater”:
```json
{
  displaySettings: {
    subType:"condition",
    type:"followers",
  },
  elements: [
    {
      type:"rule",
      condition: {
	  entity:"contact",
        field:"followers",
        operand:"lt",
        value:5000,
      },
      onFail: {
        action:"fallthrough"
      },
      onMatch:  {
        action:"goto",
        target:"5e26e98027b2c58a70085d4f"
      }
    },
    {
      type:"rule",
      condition: {
	  entity:"contact",
        field:"followers",
        operand:"lt",
        value:15000,
      },
      onFail: {
        action:"goto",
        target:"5e26e98027b2c58a70085d4e"
      },
      onMatch:  null
    }
  ]
}
```
</details>