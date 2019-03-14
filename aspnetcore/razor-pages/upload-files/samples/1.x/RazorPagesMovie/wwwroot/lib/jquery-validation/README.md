---
ms.openlocfilehash: 1b563a8c0674d51f893415221ca8fab574b78265
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57046551"
---
<a name="--"></a>--
================================

[![Состояние сборки](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![Состояние devDependency](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)

Подключаемый модуль проверки jQuery предоставляет проверку доступности для имеющихся форм, делая всевозможные настройки в соответствии с вашим приложением.

## <a name="help-the-projecthttppledgiecomcampaigns18159"></a>[Помощь проекту](http://pledgie.com/campaigns/18159)

[![Помощь проекту](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)

Этот проект нуждается в помощи. [Вы можете внести пожертвование в пользу проекта с помощью кампании Pledgie](http://pledgie.com/campaigns/18159) и сообщить об этом другим. Если вы использовали подключаемый модуль или планируете его использовать, подумайте о пожертвовании (поможет любая сумма).

Вы можете найти план по затратам на странице [Pledgie](http://pledgie.com/campaigns/18159).

## <a name="get-started"></a>Приступая к работе

### <a name="downloading-the-prebuilt-files"></a>Скачивание предварительно созданных файлов

Предварительно созданные файлы можно загрузить по адресу http://jqueryvalidation.org/

### <a name="downloading-the-latest-changes"></a>Скачивание последних изменений

Невыпущенные файлы разработки можно получить следующим образом:

 1. [Скачав](https://github.com/jzaefferer/jquery-validation/archive/master.zip) или выполнив разветвление репозитория.
 2. [Настроив сборку](CONTRIBUTING.md#build-setup).
 3. Запустив `grunt` для создания файлов в каталоге dist.

### <a name="including-it-on-your-page"></a>Добавление на странице

Добавьте jQuery и подключаемый модуль на странице. Выберите форму для проверки и вызовите метод `validate`.

```html
<form>
    <input required>
</form>
<script src="jquery.js"></script>
<script src="jquery.validate.js"></script>
<script>
$("form").validate();
</script>
```

Вы также можете включить jQuery и подключаемый модуль с помощью модуля requirejs.

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

Дополнительные сведения о том, как установить правила и настройки, см. в [документации](http://jqueryvalidation.org/documentation/).

## <a name="reporting-issues-and-contributing-code"></a>Сообщение о возникших проблемах и добавление кода

Дополнительные сведения см. в [рекомендациях по дополнению](CONTRIBUTING.md).

**ВАЖНОЕ ПРИМЕЧАНИЕ О ПРОВЕРКЕ ЭЛЕКТРОННОЙ ПОЧТЫ**. Начиная с версии 1.12.0, этот подключаемый модуль использует то же регулярное выражение, которое [предлагает использовать спецификация HTML5 для браузеров](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address). Мы будем следовать этому примеру и используем ту же проверку. Если вы считаете, что спецификация неправильная, обратитесь к специалистам и сообщите о проблеме. Если у вас есть различные требования, рассмотрите [использование настраиваемого метода](http://jqueryvalidation.org/jQuery.validator.addMethod/).

## <a name="license"></a>Лицензия
Авторские права &copy; принадлежат Йорну Заффереру (Jörn Zaefferer)<br>
Лицензировано с задействованием лицензии MIT.
