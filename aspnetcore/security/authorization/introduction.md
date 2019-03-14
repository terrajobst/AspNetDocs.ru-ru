---
title: Общие сведения об авторизации в ASP.NET Core
author: rick-anderson
description: Основы авторизации и принцип действия авторизации в приложениях ASP.NET Core.
ms.author: riande
ms.date: 10/14/2016
uid: security/authorization/introduction
ms.openlocfilehash: 5465eb7875ebecd77b628376ef886db0ddd05025
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57046371"
---
# <a name="introduction-to-authorization-in-aspnet-core"></a><span data-ttu-id="f5f4f-103">Общие сведения об авторизации в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="f5f4f-103">Introduction to authorization in ASP.NET Core</span></span>

<a name="security-authorization-introduction"></a>

<span data-ttu-id="f5f4f-104">Авторизация подразумевает набор процессу, который определяет, что пользователь может выполнять.</span><span class="sxs-lookup"><span data-stu-id="f5f4f-104">Authorization refers to the process that determines what a user is able to do.</span></span> <span data-ttu-id="f5f4f-105">Например пользователь с правами администратора может создать библиотеку документов, добавьте документы, редактирование документов и удалить их.</span><span class="sxs-lookup"><span data-stu-id="f5f4f-105">For example, an administrative user is allowed to create a document library, add documents, edit documents, and delete them.</span></span> <span data-ttu-id="f5f4f-106">Пользователь без прав администратора, работа с библиотекой только авторизованные ознакомиться с документами.</span><span class="sxs-lookup"><span data-stu-id="f5f4f-106">A non-administrative user working with the library is only authorized to read the documents.</span></span>

<span data-ttu-id="f5f4f-107">Авторизация является самостоятельной и не зависит от аутентификации.</span><span class="sxs-lookup"><span data-stu-id="f5f4f-107">Authorization is orthogonal and independent from authentication.</span></span> <span data-ttu-id="f5f4f-108">Тем не менее авторизации требуется механизм проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f5f4f-108">However, authorization requires an authentication mechanism.</span></span> <span data-ttu-id="f5f4f-109">Проверка подлинности — это процесс, который позволяет установить подлинность пользователя.</span><span class="sxs-lookup"><span data-stu-id="f5f4f-109">Authentication is the process of ascertaining who a user is.</span></span> <span data-ttu-id="f5f4f-110">Проверка подлинности может создать один или несколько идентификаторов для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="f5f4f-110">Authentication may create one or more identities for the current user.</span></span>

## <a name="authorization-types"></a><span data-ttu-id="f5f4f-111">Типы авторизации</span><span class="sxs-lookup"><span data-stu-id="f5f4f-111">Authorization types</span></span>

<span data-ttu-id="f5f4f-112">Авторизация ASP.NET Core предоставляет простой, декларативный [роли](xref:security/authorization/roles) и форматированного текста [на основе политик](xref:security/authorization/policies) модели.</span><span class="sxs-lookup"><span data-stu-id="f5f4f-112">ASP.NET Core authorization provides a simple, declarative [role](xref:security/authorization/roles) and a rich [policy-based](xref:security/authorization/policies) model.</span></span> <span data-ttu-id="f5f4f-113">Авторизации выражается в требованиях и обработчики оценки заявок пользователя соответствие требованиям.</span><span class="sxs-lookup"><span data-stu-id="f5f4f-113">Authorization is expressed in requirements, and handlers evaluate a user's claims against requirements.</span></span> <span data-ttu-id="f5f4f-114">Принудительных проверок может основываться на простой политики или политики, которые оценивают идентификацию пользователя и свойства ресурса, который пользователь пытается получить доступ к.</span><span class="sxs-lookup"><span data-stu-id="f5f4f-114">Imperative checks can be based on simple policies or policies which evaluate both the user identity and properties of the resource that the user is attempting to access.</span></span>

## <a name="namespaces"></a><span data-ttu-id="f5f4f-115">Пространства имен</span><span class="sxs-lookup"><span data-stu-id="f5f4f-115">Namespaces</span></span>

<span data-ttu-id="f5f4f-116">Компоненты авторизации, включая `AuthorizeAttribute` и `AllowAnonymousAttribute` атрибуты, найдены в `Microsoft.AspNetCore.Authorization` пространства имен.</span><span class="sxs-lookup"><span data-stu-id="f5f4f-116">Authorization components, including the `AuthorizeAttribute` and `AllowAnonymousAttribute` attributes, are found in the `Microsoft.AspNetCore.Authorization` namespace.</span></span>

<span data-ttu-id="f5f4f-117">См. в документации на [простой авторизации](xref:security/authorization/simple).</span><span class="sxs-lookup"><span data-stu-id="f5f4f-117">Consult the documentation on [simple authorization](xref:security/authorization/simple).</span></span>
