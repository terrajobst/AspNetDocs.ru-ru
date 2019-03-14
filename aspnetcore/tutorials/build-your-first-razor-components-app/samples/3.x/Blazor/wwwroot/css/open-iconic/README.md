---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57054221"
---
<a name="open-iconic-v111httpuseiconiccomopen"></a>[Open Iconic версии 1.1.1](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconichttpuseiconiccom-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collectionhttpuseiconiccomopenicons"></a>Open Iconic — решение с открытым кодом одного уровня с [Iconic](http://useiconic.com). Это небольшая коллекция, которая содержит 223 отчетливых значка и которая готова к использованию с Bootstrap и Foundation. [Просмотреть коллекцию](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a>Что такое Open Iconic?

* Коллекция из 223 значков, которые отчетливо видны даже с размером 8 пикселей.
* SVG-файлы малого размера (61,8 для всего набора). 
* SVG-спрайты &mdash; это современная замена иконочных шрифтов.
* Форматы Webfont (EOT, OTF, SVG, TTF, WOFF), PNG и WebP.
* Таблицы стилей Webfont (включая версии для Bootstrap и Foundation) в формате CSS, LESS, SCSS и Stylus.
* Растровые изображения в формате PNG и WebP с размером 8, 16, 24, 32, 48 и 64 пикселя.


## <a name="getting-started"></a>Начало работы

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-iconshttpuseiconiccomopenicons-and-referencehttpuseiconiccomopenreference-sections"></a>Пример кода и все необходимое для начала работы с Open Iconic см. в руководстве по использованию [значков](http://useiconic.com/open#icons) и в [справочных материалах](http://useiconic.com/open#reference).

### <a name="general-usage"></a>Общие сведения об использовании

#### <a name="using-open-iconics-svgs"></a>Использование SVG-изображений Open Iconic

Мы предпочитаем использовать формат SVG и считаем, что это лучший способ представления значков в веб-решениях. Так как значки Open Iconic представляют собой обычные SVG-изображения, мы советуем использовать их так же, как и другие изображения (обязательно укажите атрибут `alt`).

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a>Использование SVG-спрайтов Open Iconic

Значки Open Iconic также предоставляются в виде SVG-спрайтов, что позволяет отобразить все значки в наборе с помощью одного запроса. Это похоже на использование иконочного шрифта, но без дополнительной нагрузки.

Значки из SVG-спрайта добавляются немного иначе, чем вы привыкли, но это сделать так же легко. *Совет. Чтобы легко адаптировать значки под стиль, мы советуем добавить общий класс в тег*  `<svg>` *, а уникальное имя класса для каждого отдельного значка в тег* `<use>` *.*  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

Для изменения размера значков используются только основные таблицы стилей CSS. Все значки представлены в виде квадрата, поэтому просто укажите тег `<svg>` с одинаковыми значениями ширины и высоты.

```
.icon {
  width: 16px;
  height: 16px;
}
```

Изменить цвет значков еще проще. Вам нужно просто указать правило `fill` в теге `<use>`.

```
.icon-account-login {
  fill: #f00;
}
```

Дополнительные сведения о SVG-спрайтах см. в [руководстве Крис Койера (Chris Coyier)](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).

#### <a name="using-open-iconics-icon-font"></a>Использование иконочных значков Open Iconic:


##### <a name="with-bootstrap"></a>С Bootstrap

Наши таблицы стилей для Bootstrap можно найти здесь: `font/css/open-iconic-bootstrap.{css, less, scss, styl}`


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a>С Foundation

Наши таблицы стилей для Foundation можно найти здесь: `font/css/open-iconic-foundation.{css, less, scss, styl}`

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a>В исходном формате

Наши стандартные таблицы стилей можно найти здесь: `font/css/open-iconic.{css, less, scss, styl}`

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a>Лицензия

### <a name="icons"></a>Значки

Весь код (включая разметку SVG) предоставляется по [лицензии MIT](http://opensource.org/licenses/MIT).

### <a name="fonts"></a>Шрифты

Все шрифты предоставляются по [лицензии SIL](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).
