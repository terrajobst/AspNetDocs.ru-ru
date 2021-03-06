---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: Создание действия (VB) | Документация Майкрософт
author: microsoft
description: Узнайте, как добавить новое действие в контроллер MVC ASP.NET. Сведения о требованиях к методу для действия.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: b1b53bea899deecef203551b23c087944e3990ab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470160"
---
# <a name="creating-an-action-vb"></a>Создание действия (VB)

по [Майкрософт](https://github.com/microsoft)

> Узнайте, как добавить новое действие в контроллер MVC ASP.NET. Сведения о требованиях к методу для действия.

Цель этого учебника — объяснить, как можно создать новое действие контроллера. Вы узнаете о требованиях к методу действия. Вы также узнаете, как запретить доступ к методу в качестве действия.

## <a name="adding-an-action-to-a-controller"></a>Добавление действия к контроллеру

Новое действие добавляется к контроллеру путем добавления нового метода к контроллеру. Например, контроллер в листинге 1 содержит действие с именем index () и действие с именем SayHello (). Оба метода предоставляются как действия.

**Листинг 1. Контроллерс\хомеконтроллер.ВБ**

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

Чтобы обеспечить доступ к Вселенной в качестве действия, метод должен отвечать определенным требованиям:

- Метод должен быть открытым.
- Метод не может быть статическим методом.
- Метод не может быть методом расширения.
- Метод не может быть конструктором, методом считывания или Setter.
- Метод не может иметь открытые универсальные типы.
- Метод не является методом базового класса контроллера.
- Метод не может содержать параметры **ref** или **out** .

Обратите внимание, что нет ограничений на возвращаемый тип действия контроллера. Действие контроллера может возвращать строку, значение типа DateTime, экземпляр класса Random или void. Платформа ASP.NET MVC преобразует любой тип возвращаемого значения, который не является результатом действия, в строку и подготавливает строку к просмотру в браузере.

При добавлении любого метода, который не нарушает эти требования, метод предоставляется как действие контроллера. Будьте внимательны. Действие контроллера может быть вызвано любым пользователем, подключенным к Интернету. Не следует, например, создать действие контроллера Делетемивебсите ().

## <a name="preventing-a-public-method-from-being-invoked"></a>Предотвращение вызова открытого метода

Если необходимо создать открытый метод в классе контроллера и вы не хотите предоставлять этот метод как действие контроллера, можно предотвратить вызов метода с помощью атрибута &lt;не&gt;ного действия. Например, контроллер в листинге 2 содержит открытый метод с именем Компанисекретс (), дополненный&gt;ным атрибутом &lt;.

**Листинг 2. Контроллерс\воркконтроллер.ВБ**

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

Если вы попытаетесь вызвать действие контроллера Компанисекретс (), введя/Ворк/компанисекретс в адресной строке браузера, вы получите сообщение об ошибке на рис. 1.

[![вызова метода, не вызывающего действия](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)

**Рис. 01**. вызов метода, не[поддерживающего действия (щелкните, чтобы просмотреть изображение с полным размером](creating-an-action-vb/_static/image2.png))

> [!div class="step-by-step"]
> [Назад](creating-a-controller-vb.md)
> [Вперед](aspnet-mvc-controllers-overview-cs.md)
