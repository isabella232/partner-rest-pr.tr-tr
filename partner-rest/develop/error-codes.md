---
title: İş ortağı API REST hata kodları
description: İş ortağı REST API 'Leri, isteğinizin başarısı veya başarısızlığı hakkında durum kodu içeren bir JSON nesnesi döndürür.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0829f48e5028b4a19e8a6f7b89fbb41d83a50cab
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770614"
---
# <a name="partner-api-rest-error-codes"></a>İş ortağı API REST hata kodları

Aşağıdakiler cihazlar için geçerlidir:

- İş ortağı API 'SI

Iş ortağı REST API 'Lerinde hata, standart HTTP durum kodları ve bir JSON hata yanıtı nesnesi kullanılarak döndürülür.

## <a name="http-status-codes"></a>HTTP durum kodu

Aşağıdaki tabloda, döndürülebilecek HTTP durum kodları listelenmektedir ve açıklanmaktadır.

| Durum kodu | Durum iletisi                  | Description                                                                                                                            |
|:------------|:--------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------|
| 400         | Hatalı İstek                     | Hatalı biçimlendirilmiş veya yanlış olduğu için istek işlenemiyor.                                                                       |
| 401         | Yetkisiz                    | Gerekli kimlik doğrulama bilgileri eksik ya da kaynak için geçerli değil.                                                   |
| 403         | Yasak                       | İstenen kaynağa erişim reddedildi. Kullanıcı yeterli izne sahip olmayabilir. **Önemli: koşullu erişim ilkeleri bir kaynağa uygulanmışsa, `HTTP 403; Forbidden error=insufficent_claims` döndürülebilir.** Microsoft Graph ve koşullu erişim hakkında daha fazla bilgi için bkz. [Azure Active Directory Koşullu erişim Için Geliştirici Kılavuzu](https://docs.microsoft.com/azure/active-directory/develop/active-directory-conditional-access-developer)  |
| 404         | Bulunamadı                       | İstenen kaynak yok.                                                                                                  |
| 405         | Yönteme Izin verilmiyor              | İstekte HTTP yöntemine izin verilmiyor.                                                                         |
| 406         | Kabul edilemez                  | Bu hizmet, Accept üst bilgisinde istenen biçimi desteklemiyor.                                                                |
| 409         | Çakışma                        | Geçerli durum isteğin beklediği değişikliklerle çakışıyor. Örneğin, belirtilen üst klasör mevcut olmayabilir.                   |
| 410         | Kayb                            | İstenen kaynak artık sunucuda yok.                                               |
| 411         | Uzunluk gerekiyor                 | İstekte bir Content-Length üst bilgisi gereklidir.                                                                                    |
| 412         | Önkoşul başarısız oldu             | İstekte belirtilen bir önkoşul (örneğin, IF-Match üst bilgisi) kaynağın geçerli durumuyla eşleşmiyor.                       |
| 413         | İstek varlığı çok büyük        | İstek boyutu üst sınırı aşıyor.                                                                                            |
| 415         | Desteklenmeyen medya türü          | İsteğin içerik türü, hizmet tarafından desteklenmeyen bir biçimdir.                                                      |
| 416         | İstenen Aralık Satisfiable değil | Belirtilen bayt aralığı geçersiz veya kullanılamıyor.                                                                                    |
| 422         | Proceslabilen varlık            | Anlam yanlış olduğundan istek işlenemiyor.                                                                        |
| 423         | Kilitli                          | Erişilmekte olan kaynak kilitli.                                                                                          |
| 429         | Çok fazla Istek               | İstemci uygulaması kısıtlandı ve bir süre geçtiğinde isteği tekrarlamaya çalışmamalıdır.                |
| 500         | İç sunucu hatası           | İstek işlenirken bir iç sunucu hatası oluştu.                                                                       |
| 501         | Uygulanmadı                 | İstenen özellik uygulanmadı.                                                                                               |
| 503         | Hizmet kullanılamıyor             | Hizmet, bakım için geçici olarak kullanılamıyor veya aşırı yüklendi. Bir gecikmeden sonra bir Retry-After üst bilgisinde belirtilemeyebilir, bu isteği yineleyebilirsiniz.|
| 504         | Ağ geçidi zaman aşımı                 | Sunucu, proxy görevi gören sırada, isteği tamamlamaya çalışırken erişmesi gereken yukarı akış sunucusundan zamanında yanıt almadı. , 503 ile birlikte gerçekleşebilir. |
| 507         | Yetersiz depolama alanı            | En fazla depolama kotasına ulaşıldı.                                                                                            |
| 509         | Bant genişliği sınırı aşıldı        | Uygulamanız maksimum bant genişliği üst sınırını aşarak kısıtlanıyor. Uygulamanız, daha fazla süre geçtikten sonra isteği yeniden deneyebilir. |

Hata yanıtı, **Error** adlı tek bir özellik içeren tek bir JSON nesnesidir. Bu nesne hatanın tüm ayrıntılarını içerir. HTTP durum koduna ek olarak veya yerine döndürülen bilgileri kullanabilirsiniz. Aşağıda, tam JSON hata gövdesinin bir örneği verilmiştir.

## <a name="error-resource-type"></a>Hata kaynağı türü

Hata yanıtı, **Error** adlı tek bir özellik içeren tek bir JSON nesnesidir. Bu nesne hatanın tüm ayrıntılarını içerir. HTTP durum koduna ek olarak veya yerine döndürülen bilgileri kullanabilirsiniz. Aşağıda, tam JSON hata gövdesinin bir örneği verilmiştir.

Aşağıdaki tablo ve kod örneği bir hata yanıtının şemasını açıklar.

| Ad        | Tür   | Description                                                                                    |
|-------------|--------|------------------------------------------------------------------------------------------------|
| kod        | string | Her zaman döndürülür. Oluşan hata türünü gösterir. Null olmayan.                          |
| message | string | Her zaman döndürülür. Ayrıntıları ayrıntılı olarak açıklar ve ek hata ayıklama bilgileri sağlar. Null olmayan, boş olmayan. Maksimum uzunluk 1024 karakterdir. |
| ınnererror        | object  | İsteğe bağlı. Üst düzey hatadan daha fazla özel olabilecek ek hata nesnesi.                                   |
| hedef      | string | Hatanın başlatıldığı hedef.                                                      |

### <a name="code-property"></a>Code özelliği

`code`Özelliği, aşağıdaki olası değerlerden birini içerir. Uygulamalarınız bu hatalardan herhangi birini işleyecek şekilde hazırlanmalıdır.

| Kod                      | Description
|:--------------------------|:--------------
| **Accessreddedildi**          | Çağıranın eylemi gerçekleştirme izni yok.
| **generalException**      | Belirtilmeyen bir hata oluştu.
| **ınvalidrequest**        | İstek hatalı oluşturulmuş veya yanlış.
| **ıtemnotfound**          | Kaynak bulunamadı.
|**preconditionFailed**     | İstekte belirtilen bir önkoşul (örneğin, IF-Match üst bilgisi) kaynağın geçerli durumuyla eşleşmiyor.
| **resourceModified**      | Kaynak, en son okuduğundan, genellikle bir eTag uyumsuzluğu olduğundan, güncelleştirilmekte olan kaynak değiştirildi.
| **serviceNotAvailable**   | Hizmet kullanılamıyor. Bir gecikmeden sonra isteği yeniden deneyin. Retry-After üst bilgisi olabilir.
| **doğrulanmayan**       | Çağıranın kimliği doğrulanmadı.

### <a name="message-property"></a>İleti özelliği

`message`Kökündeki özelliği, geliştiricinin okumasını amaçlanan bir hata iletisi içerir. Hata iletileri yerelleştirilmez ve doğrudan kullanıcıya gösterilmemelidir. Hataları işlerken, kodunuz `message` herhangi bir zamanda değiştirebildiğinden ve genellikle başarısız olan isteğe özel dinamik bilgiler içeriyorsa, kodunuzun değerleri gözden kurmamalıdır. Yalnızca özelliklerde döndürülen hata kodlarına karşı kod almalısınız `code` .

### <a name="innererror-object"></a>Innererror nesnesi

`innererror`Nesne yinelemeli `innererror` olarak ek ve daha özel hata kodlarıyla daha fazla nesne içerebilir. Bir hata işlenirken, uygulamalar kullanılabilir tüm hata kodlarını çağırmalıdır ve anladıkları en ayrıntılı olanı kullanır.

Uygulamanızın iç içe geçmiş nesneler içinde karşılaşabileceği bazı ek hatalar vardır `innererror` . Uygulamalar bunları işlemek için gerekli değildir, ancak bunları seçebilirler. Hizmet yeni hata kodları ekleyebilir veya herhangi bir zamanda eski olanları döndürmeyi durdurabilir, bu nedenle tüm uygulamaların [temel hata kodlarını] işleyebilmesi önemlidir.

```json
{
  "error": {
    "code": "unAuthorized",
    "message": "Caller is not authorized to access the resource.",
    "target": "referral",
    "innerError": {
      "code": "innerErrorCode",
      "message": "Unauthorized referral access"
    }
  }
}
```
