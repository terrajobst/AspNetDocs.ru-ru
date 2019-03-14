---
ms.openlocfilehash: 24c36493284988aa45b15c78e2577c0ef96aba56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029991"
---
<a name="jquery-validation-pluginhttpsjqueryvalidationorg---form-validation-made-easy"></a>[Подключаемый модуль проверки jQuery](https://jqueryvalidation.org/) — упрощенная проверка форм
================================

[![Состояние сборки](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![Состояние devDependency](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)

Подключаемый модуль проверки jQuery предоставляет проверку доступности для имеющихся форм, делая всевозможные настройки в соответствии с вашим приложением.

## <a name="getting-started"></a>Начало работы

### <a name="downloading-the-prebuilt-files"></a>Скачивание предварительно созданных файлов

Предварительно созданные файлы можно загрузить по адресу https://jqueryvalidation.org/

### <a name="downloading-the-latest-changes"></a>Скачивание последних изменений

Невыпущенные файлы разработки можно получить следующим образом:

 1. [Скачав](https://github.com/jquery-validation/jquery-validation/archive/master.zip) или выполнив разветвление репозитория.
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

Дополнительные сведения о том, как установить правила и настройки, см. в [документации](https://jqueryvalidation.org/documentation/).

## <a name="reporting-issues-and-contributing-code"></a>Сообщение о возникших проблемах и добавление кода

Дополнительные сведения см. в [рекомендациях по дополнению](CONTRIBUTING.md).

**ВАЖНОЕ ПРИМЕЧАНИЕ О ПРОВЕРКЕ ЭЛЕКТРОННОЙ ПОЧТЫ**. Начиная с версии 1.12.0, этот подключаемый модуль использует то же регулярное выражение, которое [предлагает использовать спецификация HTML5 для браузеров](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address). Мы будем следовать этому примеру и используем ту же проверку. Если вы считаете, что спецификация неправильная, обратитесь к специалистам и сообщите о проблеме. Если у вас есть различные требования, рассмотрите [использование настраиваемого метода](https://jqueryvalidation.org/jQuery.validator.addMethod/).
Если вам нужно изменить встроенные шаблоны регулярных выражений для проверки, соблюдайте [инструкции, указанные в документации](https://jqueryvalidation.org/jQuery.validator.methods/).

**Важное примечание о методе REQUIRED**. Начиная с версии 1.14.0, этот подключаемый модуль не удаляет концевые пробелы из значения вложенного элемента. Если вы хотите сохранить прежнее поведение, используйте [`normalizer`](https://jqueryvalidation.org/normalizer/) для преобразования значения элемента перед проверкой. Эта возможность доступна, начиная с версии `v1.15.0`. Другими словами, вы можете применить что-то подобное:
``` js
$("#myForm").validate({
    rules: {
        username: {
            required: true,
            // Using the normalizer to trim the value of the element
            // before validating it.
            //
            // The value of `this` inside the `normalizer` is the corresponding
            // DOMElement. In this example, `this` references the `username` element.
            normalizer: function(value) {
                return $.trim(value);
            }
        }
    }
});
```

## <a name="license"></a>Лицензия
Авторские права &copy; принадлежат Йорну Заффереру (Jörn Zaefferer)<br>
Лицензировано с задействованием лицензии MIT.
