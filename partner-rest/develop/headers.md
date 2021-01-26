---
title: İş ortağı API 'SI REST üstbilgileri
description: Aşağıdaki HTTP isteği ve yanıt üst bilgileri, Iş ortağı REST API tarafından desteklenir.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 955cab07da7f3a386690e18042165015906d864a
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770601"
---
# <a name="partner-rest-api-headers"></a>İş ortağı REST API üst bilgileri

Iş ortağı REST API aşağıdaki HTTP isteği ve yanıt üst bilgilerini destekler.

> [!NOTE]
> Tüm API çağrıları tüm üst bilgileri kabul etmez.

## <a name="request-headers"></a>İstek üst bilgileri

Aşağıdaki HTTP istek üstbilgileri, Iş ortağı REST API tarafından desteklenir.

| Üst bilgi                       | Değer Türü | Description                                                                            |
|------------------------------|------------|----------------------------------------------------------------------------------------|
| Yetkilendirme           | string     | Gereklidir. Taşıyıcı belirtecindeki yetkilendirme belirteci &lt; &gt; .                    |
| Kabul Et                  | string     | "Application/JSON" istek ve yanıt türünü belirtir.                           |
| istemci-istek kimliği         | GUID       | Gereklidir. Arama için benzersiz bir tanımlayıcı, günlüklerde ve ağ izlemelerinde yararlı olarak sorun giderme hataları. Değer her çağrı için sıfırlanmalıdır. Tüm işlemler bu üstbilgiyi içermelidir. |
| IF-Match:                    | string     | Eşzamanlılık denetimi için kullanılır. Bazı API çağrıları, If-Match üst bilgisi aracılığıyla ETag 'in geçirilmesini gerektirir. ETag genellikle kaynakta bulunur ve bu nedenle en son sürümü ALMANıZı gerektirir. |

## <a name="response-headers"></a>Yanıt üst bilgileri

Aşağıdaki HTTP yanıt üst bilgileri, Iş ortağı REST API döndürebilir.

| Üst bilgi                    | Değer türü | Description                                                                                                               |
|-------------------|------------|--------------------------------------------------------------------------------------------------|
| Kabul Et                | string     | "Application/JSON" istek ve yanıt türünü belirtir.                                     |
| istek kimliği        | GUID       | Kimlik-kuvvet sağlamak için kullanılan, çağrı için benzersiz bir tanımlayıcı. Zaman aşımı durumunda, yeniden deneme çağrısı aynı değeri içermelidir. Yanıt aldıktan sonra (başarı veya iş hatası), sonraki çağrının değeri sıfırlanmalıdır. |
| istemci-istek kimliği| GUID| Çağrı için benzersiz bir tanımlayıcı olan, sorun giderme hatalarına yönelik Günlükler ve ağ izlemeleri yararlı. Değer her çağrı için sıfırlanmalıdır. Tüm işlemler bu üstbilgiyi içermelidir.                                                |
| x-MS-AGS-tanılama   | string | Hizmetten tanılama bilgilerini içeren bir dize.
| timestamp|string | API 'ye gelindiğinde isteğin zaman damgası.
|Özelliği |string | Kaynağın ETag 'i.
