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
# <a name="partner-api-authentication"></a><span data-ttu-id="1a0c8-103">İş Ortağı API kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="1a0c8-103">Partner API authentication</span></span>

<span data-ttu-id="1a0c8-104">Aşağıdakiler cihazlar için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="1a0c8-104">Applies to:</span></span>

- <span data-ttu-id="1a0c8-105">İş ortağı API 'SI</span><span class="sxs-lookup"><span data-stu-id="1a0c8-105">Partner API</span></span>

<span data-ttu-id="1a0c8-106">Iş ortağı API 'SI kimlik doğrulaması için Azure Active Directory (Azure AD) kullanır.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-106">The Partner API utilizes Azure Active Directory (Azure AD) for authentication.</span></span> <span data-ttu-id="1a0c8-107">Iş ortağı API 'siyle etkileşim kurarken, bir Azure AD uygulamasını doğru bir şekilde yapılandırmanız ve bir erişim belirteci edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-107">When you interact with the Partner API, you must correctly configure an Azure AD application and obtain an access token.</span></span> <span data-ttu-id="1a0c8-108">[Uygulama ve Kullanıcı erişimi](#application-and-user-access) ya da [yalnızca uygulama erişimi](#application-only-access)için erişim belirteçleri elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-108">You can obtain access tokens for [application and user access](#application-and-user-access) or [application-only access](#application-only-access).</span></span>

## <a name="application-and-user-access"></a><span data-ttu-id="1a0c8-109">Uygulama ve Kullanıcı erişimi</span><span class="sxs-lookup"><span data-stu-id="1a0c8-109">Application and user access</span></span>

<span data-ttu-id="1a0c8-110">Bu yöntem, API 'ye **uygulama ve Kullanıcı erişimi** ayarlamak için önerilir.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-110">This method is recommended to set up **application and user access** to the API.</span></span>

1. <span data-ttu-id="1a0c8-111">[Azure portalında](https://portal.azure.com/) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-111">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1a0c8-112">**Azure Active Directory** hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-112">Choose the **Azure Active Directory** service.</span></span>
3. <span data-ttu-id="1a0c8-113">**Uygulama kayıtları** ve ardından **Yeni uygulama kaydı**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-113">Choose **App registrations**, then choose **New application registration**.</span></span>
4. <span data-ttu-id="1a0c8-114">Yeni uygulamanızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-114">Create your new application.</span></span> <span data-ttu-id="1a0c8-115">**Uygulama türü** için **Yerel**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-115">For **Application type**, select **Native**.</span></span> <span data-ttu-id="1a0c8-116">Bir ad ve URL girip **Oluştur**' u seçin.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-116">Provide a name and URL, then select **Create**.</span></span>
5. <span data-ttu-id="1a0c8-117">Uygulama için **API izinleri** seçin.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-117">Choose **API permissions** for the application.</span></span> <span data-ttu-id="1a0c8-118">**API Izinleri iste** ekranında, **izin Ekle**' yi seçin, sonra **Kuruluşumun kullandığı API 'leri** seçin</span><span class="sxs-lookup"><span data-stu-id="1a0c8-118">On the **Request API permissions** screen, choose **Add a permission**, then choose **APIs my organization uses**</span></span>
6. <span data-ttu-id="1a0c8-119">*Microsoft Iş ortağı* (*Microsoft geliştirme merkezi*) API 'si () için arama yapın `4990cffe-04e8-4e8b-808a-1175604b879f` .</span><span class="sxs-lookup"><span data-stu-id="1a0c8-119">Search for the *Microsoft Partner* (*Microsoft Dev Center*) API (`4990cffe-04e8-4e8b-808a-1175604b879f`).</span></span>

    ![Microsoft Iş ortağı API 'SI araması ile Istek API 'SI izinleri ekranının ekran görüntüsü](../images/SearchGatewayApi.png)

7. <span data-ttu-id="1a0c8-121">**Temsilci Izinleri** **iş ortağı merkezi**'ne ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-121">Set the **Delegated Permissions** to **Partner Center**.</span></span>

    ![Microsoft Iş ortağı API 'SI için temsilci izinleri yapılandırma ekranının ekran görüntüsü](../images/SelectUserPermission.png)
    
8. <span data-ttu-id="1a0c8-123">*Microsoft Iş ortağı* (*Microsoft iş ortağı merkezi*) API 'si () için arama yapın `fa3d9a0c-3fb0-42cc-9193-47c7ecd2edbd` .</span><span class="sxs-lookup"><span data-stu-id="1a0c8-123">Search for the *Microsoft Partner* (*Microsoft Partner Center*) API (`fa3d9a0c-3fb0-42cc-9193-47c7ecd2edbd`).</span></span>

    ![Microsoft Iş Ortağı Merkezi API araması ile Istek API 'SI izinleri ekranının ekran görüntüsü](../images/SearchPCApi.png)
    
9. <span data-ttu-id="1a0c8-125">**Microsoft Iş Ortağı Merkezi** ' ni seçin ve **user_impersonation** denetleyin.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-125">Select **Microsoft Partner Center** and check **user_impersonation**.</span></span>

10. <span data-ttu-id="1a0c8-126">**Temsilci Izinleri** **iş ortağı merkezi**'ne ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-126">Set the **Delegated Permissions** to **Partner Center**.</span></span>

    ![Microsoft Iş Ortağı Merkezi API 'SI için temsilci izinleri yapılandırma ekranının ekran görüntüsü](../images/SelectPCUserPermission.png)

## <a name="application-only-access"></a><span data-ttu-id="1a0c8-128">Yalnızca uygulama erişimi</span><span class="sxs-lookup"><span data-stu-id="1a0c8-128">Application-only access</span></span>

<span data-ttu-id="1a0c8-129">Bu yöntem, API 'lere **yalnızca uygulama erişimi** kurulumu için önerilir.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-129">This method is recommended for **application-only access** setup to the APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a0c8-130">Azure AD uygulamanızdan uygulama KIMLIĞI, uygulama anahtarı ve dizin KIMLIĞI sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-130">You must provide the application ID, application key, and directory ID from your Azure AD application.</span></span>

1. <span data-ttu-id="1a0c8-131">[Azure portalında](https://portal.azure.com/) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-131">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1a0c8-132">**Azure Active Directory** hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-132">Select the **Azure Active Directory** service.</span></span>
3. <span data-ttu-id="1a0c8-133">**Uygulama kayıtları** ve ardından **Yeni uygulama kaydı**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-133">Choose **App registrations**, then select **New application registration**.</span></span>
4. <span data-ttu-id="1a0c8-134">Yeni uygulamanızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-134">Create your new application.</span></span> <span data-ttu-id="1a0c8-135">**Uygulama türü** için **Web uygulaması/API**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-135">For **Application type**, choose **Web app/API**.</span></span> <span data-ttu-id="1a0c8-136">Bir uygulama **adı** ve **URL** girin.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-136">Enter a an application **name** and **URL**.</span></span> <span data-ttu-id="1a0c8-137">Ardından **Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-137">Then choose **Create**.</span></span>
5. <span data-ttu-id="1a0c8-138">Uygulama için **API izinleri** seçin.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-138">Choose **API permissions** for the application.</span></span> <span data-ttu-id="1a0c8-139">**Izin Ekle**' yi seçin, sonra **Kuruluşumun kullandığı API 'leri** seçin</span><span class="sxs-lookup"><span data-stu-id="1a0c8-139">Choose **Add a permission**, then choose **APIs my organization uses**</span></span>
6. <span data-ttu-id="1a0c8-140">*Microsoft Iş ortağı* (*Microsoft geliştirme merkezi*) API 'si () için arama yapın `4990cffe-04e8-4e8b-808a-1175604b879f` .</span><span class="sxs-lookup"><span data-stu-id="1a0c8-140">Search for the *Microsoft Partner* (*Microsoft Dev Center*) API (`4990cffe-04e8-4e8b-808a-1175604b879f`).</span></span>

    ![Microsoft Iş ortağı API 'SI araması ile Istek API 'SI izinleri ekranının ekran görüntüsü](../images/SearchGatewayApi.png)

7. <span data-ttu-id="1a0c8-142">**Temsilci Izinleri** **iş ortağı merkezi**'ne ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-142">Set the **Delegated Permissions** to **Partner Center**.</span></span>

    ![Microsoft Iş ortağı API 'SI için temsilci izinleri yapılandırma ekranının ekran görüntüsü](../images/SelectUserPermission.png)

8. <span data-ttu-id="1a0c8-144">Kaydettiğiniz uygulama için **Özellikler** ' i seçin ve ardından **uygulama kimliğini Kopyala**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-144">For the application you registered, choose **Properties** and then select **copy the Application ID**.</span></span>
9. <span data-ttu-id="1a0c8-145">**Ayarlar**' ı ve ardından **Sertifikalar & parolaları**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-145">Choose **Settings**, then choose **Certificates & Secrets**.</span></span> <span data-ttu-id="1a0c8-146">**Yeni Istemci parolası** ' nı seçin ve **süre sonu** ' nu **süresiz olarak ayarlayın**.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-146">Choose **New Client Secret** and set the **Expiration**  to **Never expires**.</span></span> <span data-ttu-id="1a0c8-147">Sonra **Kaydet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-147">Then choose **Save**.</span></span>
10. <span data-ttu-id="1a0c8-148">**Anahtarlar** menüsünde, **anahtar değerini Kopyala**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-148">On the **Keys** menu, choose **Copy the key value**.</span></span> <span data-ttu-id="1a0c8-149">Bu değerin bir kopyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-149">Save a copy of this value.</span></span>

> [!WARNING]
> <span data-ttu-id="1a0c8-150">Oluşturduğunuz anahtar için anahtar değerinin bir kopyasını kaydettiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-150">Be sure to save a copy of the key value for the key you created.</span></span> <span data-ttu-id="1a0c8-151">Bir belirteç almak için bu anahtar değerini daha sonra kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-151">You will need to use this key value later to obtain a token.</span></span>

## <a name="partner-consent"></a><span data-ttu-id="1a0c8-152">İş ortağı onayı</span><span class="sxs-lookup"><span data-stu-id="1a0c8-152">Partner consent</span></span>

<span data-ttu-id="1a0c8-153">Azure Yönetim Portalı ' nda **Kurumsal uygulamalar**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-153">In the Azure management portal, select **Enterprise applications**.</span></span> <span data-ttu-id="1a0c8-154">Önceki bölümde oluşturduğunuz uygulamayı arayın ve bu uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="1a0c8-154">Search for the application you created in the previous section, and select that application.</span></span> <span data-ttu-id="1a0c8-155">**İzinler** ' i seçin ve ardından **iş ortağı hesabı Için yönetici onayı ver**' i seçin</span><span class="sxs-lookup"><span data-stu-id="1a0c8-155">Select **Permissions** , then select **Grant Admin Consent for Partner Account**.</span></span>
