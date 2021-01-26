---
title: Referans kaynakları
description: Başvuru kaynakları bir müşterinin, Microsoft 'un veya başka bir iş ortağının doğrudan satış lideri olduğunu gösterir.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 08438d208da57a4df40aeb609b14b6b6a6128d45
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770597"
---
# <a name="referral-resources"></a>Referans kaynakları

Aşağıdakiler cihazlar için geçerlidir:

- İş Ortağı Merkezi

Bu kaynaklar bir müşterinin, Microsoft 'un veya başka bir iş ortağının doğrudan satış lideri olduğunu gösterir.

## <a name="referral"></a>Başvuruyu

Başvuruyu temsil eder.

| Özellik              | Tür                                              | Description                                                                                                       |
|-----------------------|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Id                    | string                                            | Bu başvurunun KIMLIĞI.                                                                                         |
| EngagementId          | string                                            | Bu başvuru için EngagementID. Birden çok başvuru tek bir EngagementID ilişkilendirilebilir                 |
| Name                  | string                                            | Başvurunun adı.                 |
| Externalreferenceıd   | string                                            | Başvuru için bir dış tanımlayıcı. Örnek: kendi Dynamics 365 müşteri adayı/fırsat KIMLIĞINIZI depolayın                    |
| CreatedDateTime       | UTC Tarih saat biçiminde dize                    | Başvurunun oluşturulduğu tarih.                                                                                |
| UpdatedDateTime       | UTC Tarih saat biçiminde dize                    | Başvurunun en son güncelleştirildiği tarih.                                                                           |
| ExpirationDateTime    | UTC Tarih saat biçiminde dize                    | Başvurunun sona ereceği tarih.                                                                                |
| Durum                | [ReferralStatus](referral-resources.md#referralstatus)      | Başvuru durumunu gösteren değerleri içeren bir [sabit listesi](https://docs.microsoft.com/dotnet/api/system.enum) . |
| Dosya          | [ReferralSubstatus](referral-resources.md#referralsubstatus)      | Başvuru alt durumunu gösteren değerler içeren bir [enum](https://docs.microsoft.com/dotnet/api/system.enum) . |
| StatusReason          | string                                            | Durum hakkında açıklayıcı bir ileti. Örnek: başvuru neden kayboldu? |
| ReferralType          | [ReferralType](referral-resources.md#referraltype)          | Başvuru türünü temsil eder.                                                                                     |
| Eleme         | [ReferralQualification](referral-resources.md#referralqualification)| Başvurunun kalitesini temsil eder.                                                                           |
| CustomerProfile       | [CustomerProfile](referral-resources.md#customerprofile)    | Müşteriyle ilgili bilgiler.                                                                                     |
| Onay               | [Onay](referral-resources.md#consent)                    | Diğer kuruluşlarla bilgi paylaşma ve kullanıcıların kullanıcılarla iletişim kurmasına izin verme bayrakları.         |
| Ayrıntılar               | [ReferralDetails](referral-resources.md#referraldetails)    | Müşteri ayrıntıları, notlar, anlaşma değeri, para birimi kapanış tarihi.                                                                |
| Takım                  | [Üye](referral-resources.md#member)                      | Söz konusu kuruluşlardaki kullanıcıları temsil eder.                                |
| Davet edilen Tecontext         | [Davet edilen Tecontext](referral-resources.md#invitecontext)        | Bir kullanıcının iş ortağı katılımında başka bir kuruluş davet ederken sağlayasun, daha fazla bilgi temsil eder.  |
| Özelliği                  | string                                            | ETags, kaynakları güncelleştirirken eşzamanlılık denetimi için kullanılır ve gereklidir. |
| Hedef         | [ReferralTarget](referral-resources.md#target)        | Bir kullanıcının iş ortağı katılımında başka bir kuruluş davet ederken sağlayasun, daha fazla bilgi temsil eder.  |

## <a name="referralstatus"></a>ReferralStatus

Başvuru durumunu gösteren değerleri içeren bir [sabit listesi](https://docs.microsoft.com/dotnet/api/system.enum) .

| Değer           | Açıklama                                                                                |
|-----------------|---------------------------------------------------------------------------------------------|
| Hiçbiri            |                                                                                             |
| Yeni             | Yeni bir başvuruyu temsil eder.                                                                 |
| Etkin          | Etkin bir başvuruyu temsil eder.                                                             |
| Kapatıldı          | Kapalı bir başvuruyu temsil eder.                                                              |

## <a name="referralsubstatus"></a>ReferralSubstatus

Başvuru durumunu gösteren değerleri içeren bir [sabit listesi](https://docs.microsoft.com/dotnet/api/system.enum) .

| Değer           | Açıklama                                                                                |
|-----------------|--------------------------------------------------------------------------------------------|
| Hiçbiri            |                                                                                            |
| Beklemede         | Bekleyen yeni bir başvuruyu temsil eder.                                                 |
| Alındı        | Alınan yeni bir başvuruyu temsil eder.                   |
| Kabul edildi        | Kabul edilen etkin bir başvuruyu temsil eder.                                                    |
| Kazanı             | Kazanılan bir kapalı başvuruyu temsil eder.                                            |
| Mesi            | Kaybolmuş bir kapalı başvuruyu temsil eder.                                           |
| Reddedildi        | Reddedilmiş bir kapalı başvuruyu temsil eder.                                       |
| Süresi doldu         | Süresi sona ermemiş olan kapalı bir başvuruyu temsil eder.                                             |

### <a name="status--substatus-transition-states"></a>Durum & alt durum geçiş durumları

| Durum                | İzin verilen durum geçişi     | İzin verilen alt durum                |
|-----------------------|-------------------------------|---------------------------------------|
| Yeni                   | Yeni, etkin, kapalı           | Bekliyor, alındı                     |
| Etkin                | Etkin, kapalı                | Kabul edildi                              |
| Kapatıldı                | Kapatıldı                        | Kazanıldı, kaybedildi, reddedildi, zaman aşımına uğradı          |

## <a name="referraltype"></a>ReferralType

Başvuru türünü gösteren değerleri içeren bir [sabit listesi](https://docs.microsoft.com/dotnet/api/system.enum) .

| Özellik              | Açıklama                                                                     |
|-----------------------|---------------------------------------------------------------------------------|
| Paylaşılan                | Dahil edilen tüm tarafların kapatılmasını sağlayacak bir başvuruyu temsil eder.  |
| Bağımsız           | İki tarafın kapatmak için birlikte çalıştırılacağı bir başvuruyu temsil eder.           |

## <a name="referralqualification"></a>ReferralQualification

Başvuru durumunu gösteren değerleri içeren bir [sabit listesi](https://docs.microsoft.com/dotnet/api/system.enum) .

| Değer                | Açıklama                                                                                 |
|----------------------|---------------------------------------------------------------------------------------------|
| Hiçbiri                 | İlişkili kalite ölçümü olmayan bir başvuruyu temsil eder.                               |
| Direct               | Doğrudan bir müşteri tarafından oluşturulan başvuruyu temsil eder.                         |
| Pazarlama niteliği   | Microsoft Pazarlama otomasyonu sistemleri aracılığıyla oluşturulmuş bir başvuruyu temsil eder.   |
| SalesQualified       | Microsoft satış aracısından bir başvuruyu temsil eder.                                         |

## <a name="customerprofile"></a>CustomerProfile

Müşterinin iletişim bilgilerini içerir.

| Özellik | Tür                                                   | Açıklama                                            |
|----------|--------------------------------------------------------|--------------------------------------------------------|
| Ad     | string                                                 | Müşteri kuruluş adı.                        |
| Adres  | [Adres](referral-resources.md#address)                         | Müşterinin adresi.                           |
| Boyut     | string                                                 | Müşteriler kuruluşundaki çalışanların sayısı. |
| Takım     | [Üye](referral-resources.md#member)                           | Müşteri kuruluşu için kişiler.            |
| Ayrılacak      | [CustomerProfileType](referral-resources.md#customerprofiletype) | Müşterinin dış kimliklerini gösteren bir değerler [dizisi](https://docs.microsoft.com/dotnet/api/system.array) .                        |

## <a name="customerprofiletype"></a>CustomerProfileType

Müşterinin dış kimliklerini içerir.

| Özellik | Tür   | Description                                                                           |
|----------|--------|---------------------------------------------------------------------------------------|
| Dçalıştırır     | string | Müşteri için [Dun & Bradstreet numarası](https://www.dnb.com/duns-number.html) . |
| Dış | string | Kuruluşunuza özel bir müşteri KIMLIĞI.                                            |

## <a name="address"></a>Adres

Müşteri için kullanılacak bir adres.

| Özellik     | Tür   | Description                                                |
|--------------|--------|------------------------------------------------------------|
| AddressLine1 | string | Adresin ilk satırı.                             |
| AddressLine2 | string | Adresin ikinci satırı. Bu özellik isteğe bağlıdır. |
| City         | string | Şehir.                                                  |
| Durum        | string | Durum.                                                 |
| PostalCode   | string | Posta kodu veya posta kodu                                |
| Ülke      | string | [ISO ülke kodu biçimindeki](https://docs.microsoft.com/dotnet/api/system.globalization.regioninfo.threeletterisoregionname?view=netframework-4.7.2)ülke/bölge.             |
| Bölge       | string | Bölge.                                                |

## <a name="member"></a>Üye

Belirli bir kişiye ait iletişim bilgilerini açıklar.

| Özellik    | Tür   | Description                  |
|-------------|--------|------------------------------|
| FirstName   | string | Kişinin adı.    |
| LastName    | string | Kişinin soyadı.     |
| PhoneNumber | string | Kişinin telefon numarası.  |
| E-posta       | string | Kişinin e-posta adresi. |
| ContactPreference       | [ContactPreference](referral-resources.md#contactpreference) | Kişinin e-posta bildirimlerini alma tercihi. |

## <a name="contactpreference"></a>ContactPreference

E-posta bildirimleri almak için iletişim tercihlerini açıklar.

| Özellik    | Tür   | Description                  |
|-------------|--------|------------------------------|
| Yerel Ayar   | string | E-posta bildiriminin yerel ayarı. [Allkültürler](https://docs.microsoft.com/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_AllCultures), [neutralkültürleri](https://docs.microsoft.com/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_NeutralCultures)ve [specifickültürleri](https://docs.microsoft.com/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_SpecificCultures) desteklenir  |
| DisableNotifications    | bool | Kullanıcı için e-posta bildirimlerini devre dışı bırakacak.     |

## <a name="consent"></a>Onay

Diğer kuruluşlarla bilgi paylaşma ve kullanıcıların kullanıcılarla iletişim kurmasına izin verme bayrakları.

| Özellik                                         | Tür      | Description                                                                                |
|--------------------------------------------------|-----------|--------------------------------------------------------------------------------------------|
| ConsentToToShareInfoWithOthers                   | boolean   | Kişisel olarak tanımlanabilen bilgilerin (PII) başkalarıyla paylaşılmasını kabul gösterir.             |
| ConsentToContact                                 | boolean   | Kullanıcılara başvurmak için izin belirtir.  |

## <a name="invitecontext"></a>Davet edilen Tecontext

Başka bir kuruluş davet edildiğinde paylaşılabilecek ek bilgiler.

| Özellik              | Tür                                                       | Açıklama                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| Notlar                 | string                                                     | Alıcı kuruluşa yönelik ek notlar.                |
| Invitedby | [Invitedby](referral-resources.md#invitedby)                                     | Başvuruyu gönderen kuruluş KIMLIĞI.                                   |

## <a name="invitedby"></a>Invitedby

Başka bir kuruluş davet edildiğinde paylaşılabilecek ek bilgiler.

| Özellik              | Tür                                                       | Description                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| OrganizationId        | string                                                     | Başvuruyu gönderen kuruluş KIMLIĞI.                |
| OrganizationName      | string                                                     | Başvuruyu gönderen kuruluş adı.                                   |

## <a name="referraldetails"></a>ReferralDetails

Başvuru ayrıntılarını temsil eder.

| Özellik              | Tür                                                       | Açıklama                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| Notlar                 | string                                                     | Alıcı kuruluşa yönelik ek notlar.                |
| Satıcılarla değeri             | decimal                                                    | Başvurunun değeri.                                    |
| Para Birimi              | string                                                    | [Iso 4217 para birimi simgesi](https://docs.microsoft.com/dotnet/api/system.globalization.regioninfo.isocurrencysymbol?view=netframework-4.7.2)                                   |
| ClosingDateTime       | UTC Tarih saat biçiminde dize                         | Müşterinin kapatmak için kullandığı tarih.                           |
| Gereksinimler          | [ReferralRequirements](referral-resources.md#referralrequirements)   | Müşterilerin ilgilendiği sektör, ürünler, hizmet türü ve çözümler.|

## <a name="referralrequirements"></a>ReferralRequirements

Müşteri gereksinimlerini içerir.

| Özellik        | Tür                                                         | Description                                          |
|-----------------|--------------------------------------------------------------|------------------------------------------------------|
| Sektörler      | [Tag](referral-resources.md#tag)                                       | Müşterinin ilgilendiği sektörler.        |
| Ürünler        | [Tag](referral-resources.md#tag)                                       | Müşterinin İlgilendiğiniz ürünler.          |
| Hizmetler        | [Tag](referral-resources.md#tag)                                       | Müşterinin ilgilendiğiniz hizmetler.          |
| Çözümler       | [SolutionTag](referral-resources.md#solutiontag)                       | Müşterinin ilgilendiğiniz çözümler.                             |

## <a name="solutiontag"></a>SolutionTag

Çözüm ayrıntılarını içerir.

| Özellik        | Tür                                         | Description                                          |
|-----------------|----------------------------------------------|------------------------------------------------------|
| Id              | string                                       | Çözümün KIMLIĞI.        |
| Name            | string                                       | Çözümün adı.          |
| Solutıontype    | [Solutıontype](referral-resources.md#solutiontype)     | Çözüm türü.          |

## <a name="solutiontype"></a>Solutıontype

Çözüm türünü gösteren değerleri içeren bir [sabit listesi](https://docs.microsoft.com/dotnet/api/system.enum) .

| Özellik        | Açıklama                                                     |
|-----------------|-----------------------------------------------------------------|
| Hiçbiri            |                                                                  |
| Kategori        |  Önceden tanımlanmış çözüm adlarından yararlanır.                            |
| Name            |  Microsoft kataloğundan çözümlere başvurmasına olanak tanır. |

## <a name="target"></a>Hedef

Başvuru hedefini açıklar.

| Özellik                  | Tür                                                  | Description                                                   |
|---------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| Id                        | string                                                | Başvuru hedefinin KIMLIĞI. |
| Tür                      | [ReferralTargetType](referral-resources.md#targettype) | Başvuru hedefi türü |

## <a name="targettype"></a>Öğesi

Çözüm türünü gösteren değerleri içeren bir [sabit listesi](https://docs.microsoft.com/dotnet/api/system.enum) .

| Özellik        | Açıklama                                                     |
|-----------------|-----------------------------------------------------------------|
| Hiçbiri            |                                                                  |
| BusinessProfileLocation         |  İş ortağı iş profilinden profil konumu.                            |
| SolutionProfile            |  İş ortağının çözüm profili. |

## <a name="tag"></a>Etiket

Etiketini açıklar.

| Özellik                  | Tür                                                  | Description                                                   |
|---------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| Id                        | string                                                | Bu etiketin KIMLIĞI.                                          |

### <a name="products"></a>Ürünler

| Değer        |
|-----------------|
|Azure|
|Enterpriseharekete Ityandgüvenliği|
|Exchange|
|DeveloperTools|
|Dynamics365Business|
|Dynamics365Enterprise|
|DynamicsAX, GP, NAV, SL|
|Microsoft365|
|Office|
|PowerBI|
|Project|
|SharePoint|
|Sktypeınfo|
|Surface|
|SurfaceHub|
|SQL|
|Teams|
|Visio|
|Windows|
|Yammer|

### <a name="services"></a>Hizmetler

| Değer        |
|-----------------|
|Danışmantingandprofessional|
|CustomSolution (ISV)|
|DeploymentOrMigration|
|Donanım|
|Tümleştirme|
|IPServices (ISV)|
|LearningAndCertification|
|Lisanslama|
|ManagedServices|
|ProjectServices|

### <a name="industries"></a>Sektörler

| Değer        |
|-----------------|
|Tarım, ormancılık, & balıkçılık|
|İletişim & medya|
|Eğitim|
|Finansal Hizmetler|
|Kamu|
|Sağlık|
|Konaklama|
|Üretim|
|Power & yardımcı programları|
|Genel güvenlik ve ulusal güvenlik|
|Perakende & tüketici malları|
|Hizmetler|
|Seyahat & ulaşım|
|Toptan & dağıtımı|

### <a name="solutions"></a>Çözümler

| Değer        |
|-----------------|
|AdvancedAnalytics|
|Applicationıntegration|
|ArtificialIntelligence|
|AzureSecurityOperationManagement|
    |AzureStack|
    |Backupdisyıldız kurtarma|
    |BigData|
    |Blok Zinciri|
    |Sohbet botu|
    |CloudDatabaseMigration|
    |CloudMigration|
    |CloudVoice|
    |CognitiveServices|
    |Yarıştivedatabasemigration|
    |Kapsayıcılar|
    |DataWarehouse|
    |DatabaseonLinux|
    |DevelopmentandTest|
    |DevOps|
    |DigitalMedia|
    |Dynamics365forCustomerService|
    |Dynamics365forFieldService|
    |Dynamics365forFinanceOperations|
    |Dynamics365forRetail|
    |Dynamics365forSales|
    |Dynamics365forTalent|
    |DynamicsonAzure|
    |EnterpriseBusinessIntelligence|
    |Oyun|
    |HighPerformanceComputing|
    |HybridStorage|
    |Identityandaccessmanagement|
    |Informationmanagement|
    |InternetofThings|
    |MachineLearning|
    |Mikro serviceapplications|
    |MobileApplications|
    |MySQLPostgresMigrationtoAzure|
    |Ağ|
    |NoSQLMigration|
    |RedhatonAzure|
    |RegulatoryComplianceGDPR|
    |SAPonAzure|
    |Sunuculesscomputing|
    |SharepointonAzure|
    |SQLServerUpgrade|
    |ThreatProtection|
    |Web geliştirme|

### <a name="customer-size"></a>Müşteri boyutu

| Değer        |
|-----------------|
|    1to50employees|
|    51to500 çalışan|
|    Morethan500employees|
|    1to9çalışanları|
|    10 to50çalışanlar|
|    51to250çalışanları|
|    251to1000çalışanları|
|    1001to5000çalışanlar|
|    5001to10000çalışanlar|
|    10001to20000çalışanlar|
|    Morethan20000employees|
