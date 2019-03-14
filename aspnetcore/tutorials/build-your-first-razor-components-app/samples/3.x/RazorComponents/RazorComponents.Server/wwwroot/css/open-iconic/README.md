---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064851"
---
<a name="open-iconic-v111httpuseiconiccomopen"></a>[<span data-ttu-id="8ef0b-101">Open Iconic версии 1.1.1</span><span class="sxs-lookup"><span data-stu-id="8ef0b-101">Open Iconic v1.1.1</span></span>](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconichttpuseiconiccom-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collectionhttpuseiconiccomopenicons"></a><span data-ttu-id="8ef0b-102">Open Iconic — решение с открытым кодом одного уровня с [Iconic](http://useiconic.com).</span><span class="sxs-lookup"><span data-stu-id="8ef0b-102">Open Iconic is the open source sibling of [Iconic](http://useiconic.com).</span></span> <span data-ttu-id="8ef0b-103">Это небольшая коллекция, которая содержит 223 отчетливых значка и которая готова к использованию с Bootstrap и Foundation.</span><span class="sxs-lookup"><span data-stu-id="8ef0b-103">It is a hyper-legible collection of 223 icons with a tiny footprint&mdash;ready to use with Bootstrap and Foundation.</span></span> [<span data-ttu-id="8ef0b-104">Просмотреть коллекцию</span><span class="sxs-lookup"><span data-stu-id="8ef0b-104">View the collection</span></span>](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a><span data-ttu-id="8ef0b-105">Что такое Open Iconic?</span><span class="sxs-lookup"><span data-stu-id="8ef0b-105">What's in Open Iconic?</span></span>

* <span data-ttu-id="8ef0b-106">Коллекция из 223 значков, которые отчетливо видны даже с размером 8 пикселей.</span><span class="sxs-lookup"><span data-stu-id="8ef0b-106">223 icons designed to be legible down to 8 pixels</span></span>
* <span data-ttu-id="8ef0b-107">SVG-файлы малого размера (61,8 для всего набора).</span><span class="sxs-lookup"><span data-stu-id="8ef0b-107">Super-light SVG files - 61.8 for the entire set</span></span> 
* <span data-ttu-id="8ef0b-108">SVG-спрайты &mdash; это современная замена иконочных шрифтов.</span><span class="sxs-lookup"><span data-stu-id="8ef0b-108">SVG sprite&mdash;the modern replacement for icon fonts</span></span>
* <span data-ttu-id="8ef0b-109">Форматы Webfont (EOT, OTF, SVG, TTF, WOFF), PNG и WebP.</span><span class="sxs-lookup"><span data-stu-id="8ef0b-109">Webfont (EOT, OTF, SVG, TTF, WOFF), PNG and WebP formats</span></span>
* <span data-ttu-id="8ef0b-110">Таблицы стилей Webfont (включая версии для Bootstrap и Foundation) в формате CSS, LESS, SCSS и Stylus.</span><span class="sxs-lookup"><span data-stu-id="8ef0b-110">Webfont stylesheets (including versions for Bootstrap and Foundation) in CSS, LESS, SCSS and Stylus formats</span></span>
* <span data-ttu-id="8ef0b-111">Растровые изображения в формате PNG и WebP с размером 8, 16, 24, 32, 48 и 64 пикселя.</span><span class="sxs-lookup"><span data-stu-id="8ef0b-111">PNG and WebP raster images in 8px, 16px, 24px, 32px, 48px and 64px.</span></span>


## <a name="getting-started"></a><span data-ttu-id="8ef0b-112">Начало работы</span><span class="sxs-lookup"><span data-stu-id="8ef0b-112">Getting Started</span></span>

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-iconshttpuseiconiccomopenicons-and-referencehttpuseiconiccomopenreference-sections"></a><span data-ttu-id="8ef0b-113">Пример кода и все необходимое для начала работы с Open Iconic см. в руководстве по использованию [значков](http://useiconic.com/open#icons) и в [справочных материалах](http://useiconic.com/open#reference).</span><span class="sxs-lookup"><span data-stu-id="8ef0b-113">For code samples and everything else you need to get started with Open Iconic, check out our [Icons](http://useiconic.com/open#icons) and [Reference](http://useiconic.com/open#reference) sections.</span></span>

### <a name="general-usage"></a><span data-ttu-id="8ef0b-114">Общие сведения об использовании</span><span class="sxs-lookup"><span data-stu-id="8ef0b-114">General Usage</span></span>

#### <a name="using-open-iconics-svgs"></a><span data-ttu-id="8ef0b-115">Использование SVG-изображений Open Iconic</span><span class="sxs-lookup"><span data-stu-id="8ef0b-115">Using Open Iconic's SVGs</span></span>

<span data-ttu-id="8ef0b-116">Мы предпочитаем использовать формат SVG и считаем, что это лучший способ представления значков в веб-решениях.</span><span class="sxs-lookup"><span data-stu-id="8ef0b-116">We like SVGs and we think they're the way to display icons on the web.</span></span> <span data-ttu-id="8ef0b-117">Так как значки Open Iconic представляют собой обычные SVG-изображения, мы советуем использовать их так же, как и другие изображения (обязательно укажите атрибут `alt`).</span><span class="sxs-lookup"><span data-stu-id="8ef0b-117">Since Open Iconic are just basic SVGs, we suggest you display them like you would any other image (don't forget the `alt` attribute).</span></span>

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a><span data-ttu-id="8ef0b-118">Использование SVG-спрайтов Open Iconic</span><span class="sxs-lookup"><span data-stu-id="8ef0b-118">Using Open Iconic's SVG Sprite</span></span>

<span data-ttu-id="8ef0b-119">Значки Open Iconic также предоставляются в виде SVG-спрайтов, что позволяет отобразить все значки в наборе с помощью одного запроса.</span><span class="sxs-lookup"><span data-stu-id="8ef0b-119">Open Iconic also comes in a SVG sprite which allows you to display all the icons in the set with a single request.</span></span> <span data-ttu-id="8ef0b-120">Это похоже на использование иконочного шрифта, но без дополнительной нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8ef0b-120">It's like an icon font, without being a hack.</span></span>

<span data-ttu-id="8ef0b-121">Значки из SVG-спрайта добавляются немного иначе, чем вы привыкли, но это сделать так же легко.</span><span class="sxs-lookup"><span data-stu-id="8ef0b-121">Adding an icon from an SVG sprite is a little different than what you're used to, but it's still a piece of cake.</span></span> <span data-ttu-id="8ef0b-122">*Совет. Чтобы легко адаптировать значки под стиль, мы советуем добавить общий класс в тег*  `<svg>` *, а уникальное имя класса для каждого отдельного значка в тег* `<use>` *.*</span><span class="sxs-lookup"><span data-stu-id="8ef0b-122">*Tip: To make your icons easily style able, we suggest adding a general class to the* `<svg>` *tag and a unique class name for each different icon in the* `<use>` *tag.*</span></span>  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

<span data-ttu-id="8ef0b-123">Для изменения размера значков используются только основные таблицы стилей CSS.</span><span class="sxs-lookup"><span data-stu-id="8ef0b-123">Sizing icons only needs basic CSS.</span></span> <span data-ttu-id="8ef0b-124">Все значки представлены в виде квадрата, поэтому просто укажите тег `<svg>` с одинаковыми значениями ширины и высоты.</span><span class="sxs-lookup"><span data-stu-id="8ef0b-124">All the icons are in a square format, so just set the `<svg>` tag with equal width and height dimensions.</span></span>

```
.icon {
  width: 16px;
  height: 16px;
}
```

<span data-ttu-id="8ef0b-125">Изменить цвет значков еще проще.</span><span class="sxs-lookup"><span data-stu-id="8ef0b-125">Coloring icons is even easier.</span></span> <span data-ttu-id="8ef0b-126">Вам нужно просто указать правило `fill` в теге `<use>`.</span><span class="sxs-lookup"><span data-stu-id="8ef0b-126">All you need to do is set the `fill` rule on the `<use>` tag.</span></span>

```
.icon-account-login {
  fill: #f00;
}
```

<span data-ttu-id="8ef0b-127">Дополнительные сведения о SVG-спрайтах см. в [руководстве Крис Койера (Chris Coyier)](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).</span><span class="sxs-lookup"><span data-stu-id="8ef0b-127">To learn more about SVG Sprites, read [Chris Coyier's guide](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).</span></span>

#### <a name="using-open-iconics-icon-font"></a><span data-ttu-id="8ef0b-128">Использование иконочных значков Open Iconic:</span><span class="sxs-lookup"><span data-stu-id="8ef0b-128">Using Open Iconic's Icon Font...</span></span>


##### <a name="with-bootstrap"></a><span data-ttu-id="8ef0b-129">С Bootstrap</span><span class="sxs-lookup"><span data-stu-id="8ef0b-129">…with Bootstrap</span></span>

<span data-ttu-id="8ef0b-130">Наши таблицы стилей для Bootstrap можно найти здесь: `font/css/open-iconic-bootstrap.{css, less, scss, styl}`</span><span class="sxs-lookup"><span data-stu-id="8ef0b-130">You can find our Bootstrap stylesheets in `font/css/open-iconic-bootstrap.{css, less, scss, styl}`</span></span>


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a><span data-ttu-id="8ef0b-131">С Foundation</span><span class="sxs-lookup"><span data-stu-id="8ef0b-131">…with Foundation</span></span>

<span data-ttu-id="8ef0b-132">Наши таблицы стилей для Foundation можно найти здесь: `font/css/open-iconic-foundation.{css, less, scss, styl}`</span><span class="sxs-lookup"><span data-stu-id="8ef0b-132">You can find our Foundation stylesheets in `font/css/open-iconic-foundation.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a><span data-ttu-id="8ef0b-133">В исходном формате</span><span class="sxs-lookup"><span data-stu-id="8ef0b-133">…on its own</span></span>

<span data-ttu-id="8ef0b-134">Наши стандартные таблицы стилей можно найти здесь: `font/css/open-iconic.{css, less, scss, styl}`</span><span class="sxs-lookup"><span data-stu-id="8ef0b-134">You can find our default stylesheets in `font/css/open-iconic.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a><span data-ttu-id="8ef0b-135">Лицензия</span><span class="sxs-lookup"><span data-stu-id="8ef0b-135">License</span></span>

### <a name="icons"></a><span data-ttu-id="8ef0b-136">Значки</span><span class="sxs-lookup"><span data-stu-id="8ef0b-136">Icons</span></span>

<span data-ttu-id="8ef0b-137">Весь код (включая разметку SVG) предоставляется по [лицензии MIT](http://opensource.org/licenses/MIT).</span><span class="sxs-lookup"><span data-stu-id="8ef0b-137">All code (including SVG markup) is under the [MIT License](http://opensource.org/licenses/MIT).</span></span>

### <a name="fonts"></a><span data-ttu-id="8ef0b-138">Шрифты</span><span class="sxs-lookup"><span data-stu-id="8ef0b-138">Fonts</span></span>

<span data-ttu-id="8ef0b-139">Все шрифты предоставляются по [лицензии SIL](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).</span><span class="sxs-lookup"><span data-stu-id="8ef0b-139">All fonts are under the [SIL Licensed](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).</span></span>
