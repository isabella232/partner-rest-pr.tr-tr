---
title: İş Ortağı API kimlik doğrulaması
description: Kimlik doğrulaması için Azure AD ile Iş ortağı API 'sini kullanmak üzere kimlik doğrulama ayarlarınızı yapılandırın.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: c5810678dccc2be1c3c084c901299961d6ba7820
ms.sourcegitcommit: 3c165938f544ff226cbe11ca21ed5aa00448d9b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "97770617"
---
# <a name="partner-api-authentication"></a>İş Ortağı API kimlik doğrulaması

Aşağıdakiler cihazlar için geçerlidir:

- İş ortağı API 'SI

Iş ortağı API 'SI kimlik doğrulaması için Azure Active Directory (Azure AD) kullanır. Iş ortağı API 'siyle etkileşim kurarken, bir Azure AD uygulamasını doğru bir şekilde yapılandırmanız ve bir erişim belirteci edinmeniz gerekir. [Uygulama ve Kullanıcı erişimi](#application-and-user-access) ya da [yalnızca uygulama erişimi](#application-only-access)için erişim belirteçleri elde edebilirsiniz.

## <a name="application-and-user-access"></a>Uygulama ve Kullanıcı erişimi

Bu yöntem, API 'ye **uygulama ve Kullanıcı erişimi** ayarlamak için önerilir.

1. [Azure portalında](https://portal.azure.com/) oturum açın.
2. **Azure Active Directory** hizmeti seçin.
3. **Uygulama kayıtları** ve ardından **Yeni uygulama kaydı**' nı seçin.
4. Yeni uygulamanızı oluşturun. **Uygulama türü** için **Yerel**' i seçin. Bir ad ve URL girip **Oluştur**' u seçin.
5. Uygulama için **API izinleri** seçin. **API Izinleri iste** ekranında, **izin Ekle**' yi seçin, sonra **Kuruluşumun kullandığı API 'leri** seçin
6. *Microsoft Iş ortağı* (*Microsoft geliştirme merkezi*) API 'si () için arama yapın `4990cffe-04e8-4e8b-808a-1175604b879f` .

    ![Microsoft Iş ortağı API 'SI araması ile Istek API 'SI izinleri ekranının ekran görüntüsü](../images/SearchGatewayApi.png)

7. **Temsilci Izinleri** **iş ortağı merkezi**'ne ayarlayın.

    ![Microsoft Iş ortağı API 'SI için temsilci izinleri yapılandırma ekranının ekran görüntüsü](../images/SelectUserPermission.png)
    
8. *Microsoft Iş ortağı* (*Microsoft iş ortağı merkezi*) API 'si () için arama yapın `fa3d9a0c-3fb0-42cc-9193-47c7ecd2edbd` .

    ![Microsoft Iş Ortağı Merkezi API araması ile Istek API 'SI izinleri ekranının ekran görüntüsü](../images/SearchPCApi.png)
    
9. **Microsoft Iş Ortağı Merkezi** ' ni seçin ve **user_impersonation** denetleyin.

10. **Temsilci Izinleri** **iş ortağı merkezi**'ne ayarlayın.

    ![Microsoft Iş Ortağı Merkezi API 'SI için temsilci izinleri yapılandırma ekranının ekran görüntüsü](../images/SelectPCUserPermission.png)

## <a name="application-only-access"></a>Yalnızca uygulama erişimi

Bu yöntem, API 'lere **yalnızca uygulama erişimi** kurulumu için önerilir.

> [!IMPORTANT]
> Azure AD uygulamanızdan uygulama KIMLIĞI, uygulama anahtarı ve dizin KIMLIĞI sağlamanız gerekir.

1. [Azure portalında](https://portal.azure.com/) oturum açın.
2. **Azure Active Directory** hizmeti seçin.
3. **Uygulama kayıtları** ve ardından **Yeni uygulama kaydı**' nı seçin.
4. Yeni uygulamanızı oluşturun. **Uygulama türü** için **Web uygulaması/API**' yi seçin. Bir uygulama **adı** ve **URL** girin. Ardından **Oluştur**’u seçin.
5. Uygulama için **API izinleri** seçin. **Izin Ekle**' yi seçin, sonra **Kuruluşumun kullandığı API 'leri** seçin
6. *Microsoft Iş ortağı* (*Microsoft geliştirme merkezi*) API 'si () için arama yapın `4990cffe-04e8-4e8b-808a-1175604b879f` .

    ![Microsoft Iş ortağı API 'SI araması ile Istek API 'SI izinleri ekranının ekran görüntüsü](../images/SearchGatewayApi.png)

7. **Temsilci Izinleri** **iş ortağı merkezi**'ne ayarlayın.

    ![Microsoft Iş ortağı API 'SI için temsilci izinleri yapılandırma ekranının ekran görüntüsü](../images/SelectUserPermission.png)

8. Kaydettiğiniz uygulama için **Özellikler** ' i seçin ve ardından **uygulama kimliğini Kopyala**' yı seçin.
9. **Ayarlar**' ı ve ardından **Sertifikalar & parolaları**' nı seçin. **Yeni Istemci parolası** ' nı seçin ve **süre sonu** ' nu **süresiz olarak ayarlayın**. Sonra **Kaydet**' i seçin.
10. **Anahtarlar** menüsünde, **anahtar değerini Kopyala**' yı seçin. Bu değerin bir kopyasını kaydedin.

> [!WARNING]
> Oluşturduğunuz anahtar için anahtar değerinin bir kopyasını kaydettiğinizden emin olun. Bir belirteç almak için bu anahtar değerini daha sonra kullanmanız gerekir.

## <a name="partner-consent"></a>İş ortağı onayı

Azure Yönetim Portalı ' nda **Kurumsal uygulamalar**' ı seçin. Önceki bölümde oluşturduğunuz uygulamayı arayın ve bu uygulamayı seçin. **İzinler** ' i seçin ve ardından **iş ortağı hesabı Için yönetici onayı ver**' i seçin
