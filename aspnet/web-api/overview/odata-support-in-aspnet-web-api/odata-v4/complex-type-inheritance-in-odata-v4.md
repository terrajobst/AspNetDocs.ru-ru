---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: Наследование сложных типов в OData v4 с помощью веб-API ASP.NET | Документация Майкрософт
author: microsoft
description: В соответствии со спецификацией OData версии 4 сложный тип может наследовать от другого сложного типа. (Сложный тип — это структурированный тип без ключа.) Веб-API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 3d90216c8e594055f77577eb6d8b1d978ae4c24d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448134"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a>Наследование сложных типов в OData v4 с веб-API ASP.NET

по [Майкрософт](https://github.com/microsoft)

> В соответствии со [спецификацией](http://www.odata.org/documentation/odata-version-4-0/)OData версии 4 сложный тип может наследовать от другого сложного типа. ( *Сложный* тип — это структурированный тип без ключа.) Веб-API OData 5,3 поддерживает наследование сложного типа.
> 
> В этом разделе показано, как создать модель EDM со сложными типами наследования. Полный исходный код см. в разделе [Пример наследования сложных типов OData](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в этом руководстве
> 
> 
> - Веб-API OData 5,3
> - OData v4

## <a name="model-hierarchy"></a>Иерархия модели

Чтобы продемонстрировать наследование сложного типа, мы будем использовать следующую иерархию классов.

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

`Shape` является абстрактным сложным типом. `Rectangle`, `Triangle`и `Circle` являются сложными типами, производными от `Shape`, а `RoundRectangle` является производным от `Rectangle`. `Window` является типом сущности и содержит экземпляр `Shape`.

Ниже приведены классы CLR, определяющие эти типы.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a>Построение модели EDM

Чтобы создать EDM, можно использовать **одатаконвентионмоделбуилдер**, который выводит отношения наследования от типов CLR.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

Вы также можете создать EDM явным образом с помощью **одатамоделбуилдер**. Это занимает больше кода, но обеспечивает более полный контроль над EDM.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

Эти два примера создают одну и ту же схему EDM.

## <a name="metadata-document"></a>Документ метаданных

Ниже приведен документ метаданных OData, демонстрирующий наследование сложного типа.

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

Из документа метаданных можно увидеть следующее:

- Сложный тип `Shape` является абстрактным.
- `Rectangle`, `Triangle`и `Circle` сложного типа имеют базовый тип `Shape`.
- Тип `RoundRectangle` имеет `Rectangle`базового типа.

## <a name="casting-complex-types"></a>Приведение сложных типов

Приведение типов в сложных типах теперь поддерживается. Например, следующий запрос приводит `Shape` к `Rectangle`.

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

Ниже приведены полезные данные ответа:

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
