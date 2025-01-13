---
title: Kundhanterade nycklar för AEM as a Cloud Service
description: Lär dig hantera krypteringsnycklar för AEM as a Cloud Service
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 100ddbf2-9c63-406f-a78d-22862501a085
source-git-commit: 18fe0125351c635c226bebf0f309710634230e64
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# Inställningar för kundhanterade nycklar för AEM as a Cloud Service {#cusomer-managed-keys-for-aem-as-a-cloud-service}

AEM as a Cloud Service lagrar för närvarande kunddata i Azure Blob Storage och MongoDB, och använder krypteringsnycklar som hanteras av providerleverantörer som standard för att skydda data. Även om den här konfigurationen uppfyller säkerhetskraven för många organisationer, kan företag i reglerade branscher eller de som behöver utökad datahemvist söka större kontroll över sin krypteringssed. För organisationer som prioriterar datasäkerhet, efterlevnad och möjlighet att hantera sina krypteringsnycklar erbjuder CMK-lösningen (Customer-Managed Keys) en viktig förbättring.

## Problemet som löses {#the-problem-being-solved}

Leverantörshanterade nycklar kan skapa bekymmer för företag inom sektorer som finans, sjukvård och myndigheter, där strikta regler kräver omfattande kontroll över datasäkerheten. Utan kontroll över nyckelhanteringen kan organisationer möta utmaningar när det gäller att uppfylla regelkrav, implementera anpassade säkerhetspolicyer och säkerställa fullständig datahemvist.

Införandet av kundhanterade nycklar (CMK) löser dessa problem genom att ge AEM möjlighet att ha full kontroll över sina krypteringsnycklar. Genom att autentisera via Microsoft Entra ID (tidigare Azure Active Directory) ansluter AEM CS säkert till kundens Azure Key Vault, vilket gör att de kan hantera livscykeln för sina krypteringsnycklar, som omfattar skapande av nycklar, rotation och återkallning.

CMK har flera fördelar:

* **Förbättrade skyddsinställningar:** Kunder kan se till att krypteringsrutinerna uppfyller specifika säkerhetskrav, vilket ger dem sinnesro när det gäller dataskydd.
* **Kompatibilitetsflexibilitet:** Med fullständig kontroll över nyckellivscykeln kan företag enkelt anpassa sig till nya standarder som GDPR, HIPAA eller CCPA och säkerställa att deras regelefterlevnadsläge förblir starkt.
* **Sömlös integrering:** CMK-lösningen integreras direkt med Azure Blob Storage och MongoDB i AEM CS, så att inga avbrott i lagringsåtgärder eller användbarhet uppstår samtidigt som kunderna får kraftfulla krypteringsfunktioner.

Genom att använda CMK kan kunderna få bättre kontroll över datasäkerhet och krypteringsrutiner, bättre regelefterlevnad och mindre risker samtidigt som de får samma skalbarhet och flexibilitet som AEM CS.

Med AEM as a Cloud Service kan du få dina egna krypteringsnycklar för att kunna kryptera data i vila. Den här guiden innehåller steg för att konfigurera en kundhanterad nyckel (CMK) i Azure Key Vault för AEM as a Cloud Service.

>[!WARNING]
>
>När du har konfigurerat CMK kan du inte återgå till systemhanterade nycklar. Du ansvarar för att hantera dina nycklar på ett säkert sätt och ge åtkomst till dina Key Vault-, Key- och CMK-appar i Azure för att förhindra att åtkomsten till dina data går förlorad.

Du får även hjälp med följande steg när du skapar och konfigurerar den nödvändiga infrastrukturen:

1. Konfigurera din miljö
1. Hämta ett program-ID från Adobe
1. Skapa en ny resursgrupp
1. Skapa en tangentkabel
1. Bevilja Adobe åtkomst till tangentkabeln
1. Skapa en krypteringsnyckel

Du måste dela nyckelvalvs-URL:en, krypteringsnyckelns namn och information om nyckelvalvet med Adobe.

## Konfigurera miljön {#setup-your-environment}

Azure Command Line Interface (CLI) är det enda kravet för den här guiden. Om du inte redan har Azure CLI installerat följer du de officiella installationsanvisningarna [här](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli).

Innan du fortsätter med resten av den här guiden loggar du in på ditt CLI med `az login`.

>[!NOTE]
>
>Den här guiden använder Azure CLI, men det går att utföra samma åtgärder via Azure-konsolen. Om du föredrar att använda Azure-konsolen använder du kommandona nedan som referens.

## Hämta ett program-ID från Adobe {#obtain-an-application-id-from-adobe}

Adobe ger dig ett program-ID för Entra som du behöver i resten av den här guiden. Om du inte redan har ett program-ID kontaktar du Adobe för att få ett.

## Skapa en ny resursgrupp {#create-a-new-resource-group}

Skapa en ny resursgrupp på valfri plats.

```powershell
# Choose a location and a name for the resource group.
$location="<AZURE LOCATION>"
$resourceGroup="<RESOURCE GROUP>"

# Create the resource group.
az group create --location $location --resource-group $resourceGroup
```

Om du redan har en resursgrupp kan du använda den i stället. I resten av den här guiden identifieras platsen för resursgruppen och dess namn med `$location` respektive `$resourceGroup`.

## Skapa ett nyckelvalv {#create-a-key-vault}

Du måste skapa ett nyckelvalv som innehåller din krypteringsnyckel. Töm skydd måste vara aktiverat för nyckelvalvet. Rensningsskydd krävs för kryptering av vilande data från andra Azure-tjänster. Åtkomst till offentliga nätverk måste också aktiveras för att klientorganisationen Adobe ska kunna komma åt nyckelvalvet.

>[!IMPORTANT]
>När nyckelvalvet med offentlig nätverksåtkomst inaktiverat skapas måste alla nyckelvalsrelaterade åtgärder, som skapande av nyckel eller rotation, utföras från en miljö som har nätverksåtkomst till KeyVault, till exempel en virtuell dator som har åtkomst till KeyVault.

```powershell
# Reuse this information from the previous step.
$location="<AZURE LOCATION>"
$resourceGroup="<RESOURCE GROUP>"

# Choose a name for the key vault.
$keyVaultName="<KEY VAULT NAME>"

# Create the key vault.
az keyvault create `
  --location $location `
  --resource-group $resourceGroup `
  --name $keyVaultName `
  --default-action=Deny `
  --enable-purge-protection `
  --enable-rbac-authorization `
  --public-network-access Enabled
```

## Ge Adobe åtkomst till nyckelvalvet {#grant-adone-access-to-the-key-vault}

I det här steget ger du Adobe åtkomst till ditt nyckelvalv via ett Entra-program. ID:t för Entra-programmet ska redan ha angetts av Adobe.

Först måste du skapa ett huvudnamn som är kopplat till Entra-programmet och tilldela det rollerna **Key Vault Reader** och **Key Vault Crypto User** till det. Rollerna är begränsade till nyckelvalvet som skapas i den här guiden.

```powershell
# Reuse this information from the previous steps.
$resourceGroup="<RESOURCE GROUP>"
$keyVaultName="<KEY VAULT NAME>"

# The application ID is provided by Adobe.
$appId="<APPLICATION ID>"

# Retrieve the ID of the key vault.
$keyVaultId=(az keyvault show --resource-group $resourceGroup --name $keyVaultName --query id --output tsv)

# Create a new service principal.
$servicePrincipalId=(az ad sp create --id $appId --query id --out tsv)

# Assign the roles to the service principal.
az role assignment create --assignee $servicePrincipalId --role "Key Vault Reader" --scope $keyVaultId
az role assignment create --assignee $servicePrincipalId --role "Key Vault Crypto User" --scope $keyVaultId
```

## Skapa en krypteringsnyckel {#create-an-ecryption-key}

Slutligen kan du skapa en krypteringsnyckel i nyckelvalvet. Observera att du behöver rollen **Nyckelvalvkryptograf** för att slutföra det här steget. Om den inloggade användaren inte har den här rollen kontaktar du systemadministratören och ber någon som redan har den rollen att slutföra det här steget åt dig.

Nätverksåtkomst till nyckelvalvet krävs för att skapa krypteringsnyckeln. Verifiera först att du har åtkomst till nyckelvalvet och fortsätt med att skapa nyckeln:

```powershell
# Reuse this information from the previous steps.
$keyVaultName="<KEY VAULT NAME>"

# Chose a name for your key.
$keyName="<KEY NAME>"

# Create the key.
az keyvault key create --vault-name $keyVaultName --name $keyName
```

## Dela information om nyckelvalvet {#share-the-key-vault-information}

Nu är ni färdiga. Du behöver bara dela viss nödvändig information med Adobe, som sköter konfigurationen av din miljö åt dig.

```powershell
# Reuse this information from the previous steps.
$resourceGroup="<RESOURCE GROUP>"
$keyVaultName="<KEY VAULT NAME>"

# Retrieve the URL of your key vault.
$keyVaultUri=(az keyvault show --name $keyVaultName `
    --resource-group $resourceGroup `
    --query properties.vaultUri `
    --output tsv)

# In addition we would need the tenantId and the subscriptionId in order to setup the connection.
$tenantId=(az keyvault show --name $keyVaultName `
    --resource-group $resourceGroup `
    --query properties.tenantId `
    --output tsv)
$subscriptionId="<Subscription ID>"
```


## Konsekvenser av återkallande av nyckelåtkomst {#implications-of-revoking-key-access}

Om du återkallar eller inaktiverar åtkomsten till Key Vault-, key- eller CMK-appen kan det leda till allvarliga störningar, bland annat att plattformens åtgärder inte fungerar som de ska. När dessa tangenter har inaktiverats kan data i Platform bli oåtkomliga, och alla åtgärder längre fram i kedjan som är beroende av dessa data kommer inte att fungera. Det är viktigt att förstå effekterna i efterföljande led till fullo innan du gör några ändringar i dina nyckelkonfigurationer.

Om du bestämmer dig för att återkalla plattformsåtkomst till dina data kan du göra det genom att ta bort den användarroll som är associerad med programmet från nyckelvalvet i Azure.

## Nästa steg {#next-steps}

Kontakta Adobe och dela:

* URL:en till nyckelvalvet. Du hämtade det i det här steget och sparade det i variabeln `$keyVaultUri`.
* Namnet på krypteringsnyckeln. Du har skapat nyckeln i ett tidigare steg och sparat den i variabeln `$keyName`.
* De `$resourceGroup`, `$subscriptionId` och `$tenantId` som krävs för att konfigurera anslutningen till nyckelvalvet.

<!-- Alexandru: hiding this for now

### Private Link Approvals {#private-link-approvals}

>[!TIP]
>You can also consult the [Azure Documentation](https://learn.microsoft.com/en-us/azure/key-vault/general/private-link-service?tabs=portal#how-to-manage-a-private-endpoint-connection-to-key-vault-using-the-azure-portal) on how to approve a Private Endpoint Connection.

Afterwards, an Adobe Engineer assigned to you will contact you to confirm the creation of the private endpoints, and will request you to approve a set of required Connection Requests. The requests can be approved either using the Azure Portal UI, where you can go to **KeyVault > Settings > Networking > Private Endpoint Connections** and approve the requests with names similar to these: 

`mongodb-atlas-<REGION>-<NUMBER>`, `storage-account-private-endpoint` and `backup-storage-account-private-endpoint`. 

Notify the Adobe Engineer once this process is complete and the Private Endpoints show up as **Approved**. -->

## Kundhanterade nycklar i Private Beta {#customer-managed-keys-in-private-beta}

Ingenjörsteamet på Adobe arbetar för närvarande på en förbättrad implementering av CMK med hjälp av Azure&#39;s Private Link. Den nya implementeringen tillåter delning av din nyckel via Azure-stamnätet tack vare en direktanslutning till Private Link mellan Adobe och ditt nyckelvalv.

Den förbättrade implementeringen finns för närvarande i Private Beta och kan aktiveras för utvalda kunder som går med på att prenumerera på Private Beta och har ett nära samarbete med Adobe Engineering. Om du är intresserad av Private Beta för CMK med hjälp av Private Link kontaktar du Adobe för mer information.
