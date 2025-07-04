---
title: Utvecklarreferenser för  [!DNL Assets]
description: Med [!DNL Assets] API:er och utvecklarreferensinnehåll kan du hantera resurser, inklusive binära filer, metadata, återgivningar, kommentarer och  [!DNL Content Fragments].
contentOwner: AG
feature: Assets HTTP API
role: Developer, Architect, Admin
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager Assets] användningsfall för utvecklare, API:er och referensmaterial {#assets-cloud-service-apis}

Artikeln innehåller rekommendationer, referensmaterial och resurser för utvecklare av [!DNL Assets] som [!DNL Cloud Service]. Den innehåller en ny modul för överföring av resurser, API-referens och information om stödet som ges i arbetsflöden efter bearbetning.

## [!DNL Experience Manager Assets] API:er och åtgärder {#use-cases-and-apis}

[!DNL Assets] som [!DNL Cloud Service] innehåller flera API:er för programmässig interaktion med digitala resurser. Varje API har stöd för särskilda användningsfall, vilket framgår av tabellen nedan. [!DNL Assets]-användargränssnittet, [!DNL Experience Manager]-datorprogrammet och [!DNL Adobe Asset Link] stöder alla eller vissa åtgärder.

>[!CAUTION]
>
>Vissa API:er finns fortfarande men stöds inte aktivt (anges med en ×). Använd inte dessa API:er i största möjliga utsträckning.

| Supportnivå | Beskrivning |
| ------------- | --------------------------- |
| ✓ | Stöds |
| x | Stöds inte. Använd inte. |
| - | Inte tillgängligt |

| Använd skiftläge | [aem-upload](https://github.com/adobe/aem-upload) | [Java-API:er för Experience Manager/Sling/JCR](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | [Resursberäkningstjänst](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html?lang=sv-SE) | [[!DNL Assets] HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html?lang=sv-SE#create-an-asset) | Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html)-servlets | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=sv-SE) |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **Ursprunglig binär** |  |  |  |  |  |  |
| Skapa original | ✓ | x | - | x | x | - |
| Läs original | - | x | ✓ | ✓ | ✓ | - |
| Uppdatera original | ✓ | x | ✓ | x | x | - |
| Ta bort original | - | ✓ | - | ✓ | ✓ | - |
| Kopiera original | - | ✓ | - | ✓ | ✓ | - |
| Flytta original | - | ✓ | - | ✓ | ✓ | - |
| **Metadata** |  |  |  |  |  |  |
| Skapa metadata | - | ✓ | ✓ | ✓ | ✓ | - |
| Läs metadata | - | ✓ | - | ✓ | ✓ | - |
| Uppdatera metadata | - | ✓ | ✓ | ✓ | ✓ | - |
| Ta bort metadata | - | ✓ | ✓ | ✓ | ✓ | - |
| Kopiera metadata | - | ✓ | - | ✓ | ✓ | - |
| Flytta metadata | - | ✓ | - | ✓ | ✓ | - |
| **Innehållsfragment (CF)** |  |  |  |  |  |  |
| Skapa CF | - | ✓ | - | ✓ | - | - |
| Läs CF | - | ✓ | - | ✓ | - | ✓ |
| Uppdatera CF | - | ✓ | - | ✓ | - | - |
| Ta bort CF | - | ✓ | - | ✓ | - | - |
| Kopiera CF | - | ✓ | - | ✓ | - | - |
| Flytta CF | - | ✓ | - | ✓ | - | - |
| **Versioner** |  |  |  |  |  |  |
| Skapa version | ✓ | ✓ | - | - | - | - |
| Läsversion | - | ✓ | - | - | - | - |
| Ta bort version | - | ✓ | - | - | - | - |
| **Mappar** |  |  |  |  |  |  |
| Skapa mapp | ✓ | ✓ | - | ✓ | - | - |
| Läs mapp | - | ✓ | - | ✓ | - | - |
| Ta bort mapp | ✓ | ✓ | - | ✓ | - | - |
| Kopiera mapp | ✓ | ✓ | - | ✓ | - | - |
| Flytta mapp | ✓ | ✓ | - | ✓ | - | - |

## Överföring av tillgångar {#asset-upload}

I [!DNL Experience Manager] som [!DNL Cloud Service] kan du överföra resurserna direkt till molnlagringen med hjälp av HTTP API. Stegen för att överföra en binär fil visas nedan. Utför dessa steg i ett externt program och inte i JVM [!DNL Experience Manager].

1. [Skicka en HTTP-begäran](#initiate-upload). Den informerar [!DNL Experience Manage]r-distributionen om din avsikt att överföra en ny binär fil.
1. [PUT innehållet i binärfilen ](#upload-binary) till en eller flera URI:er som tillhandahålls av initieringsbegäran.
1. [Skicka en HTTP-begäran](#complete-upload) för att informera servern om att innehållet i binärfilen har överförts.

![Översikt över protokollet för direkt binär överföring](assets/add-assets-technical.png)

>[!IMPORTANT]
>
>Utför stegen ovan i ett externt program och inte i JVM [!DNL Experience Manager].

Metoden ger en skalbar och mer effektiv hantering av överföringar av resurser. Skillnaderna jämfört med [!DNL Experience Manager] 6.5 är:

* Binärfiler går inte igenom [!DNL Experience Manager], vilket nu helt enkelt koordinerar överföringsprocessen med det binära molnlagringsutrymmet som är konfigurerat för distributionen.
* Binär molnlagring fungerar med ett CDN-nätverk (Content Delivery Network) eller Edge-nätverk. Ett CDN väljer en slutpunkt för överföring som är närmare för en klient. När data flyttas kortare tid till en närliggande slutpunkt förbättras överföringsprestanda och användarupplevelsen, särskilt för geografiskt utspridda team.

>[!NOTE]
>
>Se klientkoden för att implementera den här metoden i det öppna källbiblioteket [aem-upload](https://github.com/adobe/aem-upload).
>
>[!IMPORTANT]
>
>Under vissa omständigheter kan det hända att ändringar inte sprids helt mellan begäranden till Experience Manager på grund av att lagringsutrymmet i Cloud Service så småningom är konsekvent. Detta leder till 404 svar på initiering eller slutförande av överföringsanrop på grund av att de nödvändiga mappprojekten inte sprids. Kunderna bör förvänta sig 404 svar och hantera dem genom att implementera ett nytt försök med en strategi för backoff-hantering.

### Initiera överföring {#initiate-upload}

Skicka en HTTP POST-begäran till önskad mapp. Assets skapas eller uppdateras i den här mappen. Inkludera väljaren `.initiateUpload.json` för att ange att begäran är att initiera överföring av en binär fil. Sökvägen till mappen där resursen ska skapas är till exempel `/assets/folder`. POST-begäran är `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

Innehållstypen för begärandetexten ska vara `application/x-www-form-urlencoded` formulärdata, som innehåller följande fält:

* `(string) fileName`: Krävs. Namnet på resursen så som den visas i [!DNL Experience Manager].
* `(number) fileSize`: Krävs. Filstorleken, i byte, för resursen som överförs.

En enda begäran kan användas för att initiera överföringar för flera binärfiler, förutsatt att varje binärfil innehåller de obligatoriska fälten. Om det lyckas svarar begäran med en `201`-statuskod och en brödtext som innehåller JSON-data i följande format:

```json
{
    "completeURI": "(string)",
    "folderPath": "(string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ],
            "minPartSize": (number),
            "maxPartSize": (number)
        }
    ]
}
```

* `completeURI` (sträng): Anropa den här URI:n när den binära filen har överförts. URI:n kan vara en absolut eller relativ URI och klienterna bör kunna hantera båda. Värdet kan alltså vara `"https://[aem_server]:[port]/content/dam.completeUpload.json"` eller `"/content/dam.completeUpload.json"` Se [fullständig överföring](#complete-upload).
* `folderPath` (sträng): Fullständig sökväg till mappen som binärfilen överförs till.
* `(files)` (matris): En lista med element vars längd och ordning matchar längden och ordningen för listan med binär information som tillhandahålls i initieringsbegäran.
* `fileName` (sträng): Namnet på motsvarande binärfil, som anges i initieringsbegäran. Detta värde bör inkluderas i den fullständiga begäran.
* `mimeType` (sträng): MIME-typen för motsvarande binärfil, som anges i initieringsbegäran. Detta värde bör inkluderas i den fullständiga begäran.
* `uploadToken` (sträng): En överföringstoken för motsvarande binär fil. Detta värde bör inkluderas i den fullständiga begäran.
* `uploadURIs` (matris): En lista över strängar vars värden är fullständiga URI:er som binärens innehåll ska överföras till (se [Överför binär](#upload-binary)).
* `minPartSize` (tal): Den minsta tillåtna längden i byte på data som kan anges för någon av `uploadURIs`, om det finns mer än en URI.
* `maxPartSize` (tal): Den maximala längden i byte på data som kan anges för någon av `uploadURIs`, om det finns mer än en URI.

### Ladda upp binärt {#upload-binary}

Utdata från initiering av en överföring innehåller ett eller flera överförda URI-värden. Om mer än en URI anges kan klienten dela upp binärfilen i delar och göra PUT-förfrågningar från varje del till de överförda URI:erna, i ordning. Om du väljer att dela upp binärfilen i delar ska du följa följande riktlinjer:

* Varje del, med undantag för den sista, måste ha en storlek som är större än eller lika med `minPartSize`.
* Varje del måste ha en storlek mindre än eller lika med `maxPartSize`.
* Om binärfilens storlek överstiger `maxPartSize` delar du upp binärfilen i delar för att överföra den.
* Du behöver inte använda alla URI:er.

Om binärfilens storlek är mindre än eller lika med `maxPartSize` kan du istället överföra hela binärfilen till en enda överförings-URI. Om mer än en överförings-URI anges, ska du använda den första och ignorera resten. Du behöver inte använda alla URI:er.

CDN-kantnoder snabbar upp begärd överföring av binärfiler.

Det enklaste sättet att uppnå detta är att använda värdet `maxPartSize` som delstorlek. API-kontraktet garanterar att det finns tillräckligt med överförda URI:er för att överföra din binära fil om du använder det här värdet som delstorlek. Det gör du genom att dela binärfilen i delar av storleken `maxPartSize`, med en URI för varje del, i ordning. Den sista delen kan ha en storlek som är mindre än eller lika med `maxPartSize`. Anta till exempel att binärfilens totala storlek är 20 000 byte, att `minPartSize` är 5 000 byte, att `maxPartSize` är 8 000 byte och att antalet överförings-URI är 5. Utför följande steg:

* Överför de första 8 000 byten i binärfilen med den första överförings-URI:n.
* Överför de andra 8 000 byten i binärfilen med den andra överförings-URI:n.
* Överför de sista 4 000 byten i binärfilen med den tredje överförings-URI:n. Eftersom det här är den sista delen behöver den inte vara större än `minPartSize`.
* Du behöver inte använda de två sista överförings-URI:erna. Du kan ignorera dem.

Ett vanligt fel är att beräkna delstorleken baserat på antalet överförings-URI:er som tillhandahålls av API:t. API-kontraktet garanterar inte att den här metoden fungerar och kan i själva verket resultera i delstorlekar som ligger utanför intervallet mellan `minPartSize` och `maxPartSize`. Detta kan leda till binära överföringsfel.

Det enklaste och säkraste sättet är att helt enkelt använda delar med samma storlek som `maxPartSize`.

Om överföringen lyckas svarar servern på varje begäran med en `201`-statuskod.

>[!NOTE]
>
>Mer information om överföringsalgoritmen finns i [den officiella funktionsdokumentationen](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload) och [API-dokumentationen](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/api/binary/BinaryUpload.html) i Apache Jackrabbit Oak-projektet.

### fullständig överföring {#complete-upload}

När alla delar av en binär fil har överförts skickar du en HTTP POST-begäran till den fullständiga URI som anges av initieringsdata. Innehållstypen för begärandetexten ska vara `application/x-www-form-urlencoded` formulärdata, som innehåller följande fält.

| Fält | Typ | Obligatoriskt eller inte | Beskrivning |
|---|---|---|---|
| `fileName` | Sträng | Obligatoriskt | Namnet på resursen, enligt initieringsdata. |
| `mimeType` | Sträng | Obligatoriskt | HTTP-innehållstypen för binärfilen, som angavs i initieringsdata. |
| `uploadToken` | Sträng | Obligatoriskt | Överför token för binärfilen enligt initieringsdata. |
| `createVersion` | Boolean | Valfritt | Om det finns `True` och en resurs med det angivna namnet skapar [!DNL Experience Manager] en ny version av resursen. |
| `versionLabel` | Sträng | Valfritt | Om en ny version skapas är den etikett som är associerad med den nya versionen av en resurs . |
| `versionComment` | Sträng | Valfritt | Om en ny version skapas, de kommentarer som är kopplade till versionen. |
| `replace` | Boolean | Valfritt | Om det finns `True` och en resurs med det angivna namnet, tar [!DNL Experience Manager] bort resursen och återskapar den. |
| `uploadDuration` | Nummer | Valfritt | Den totala tiden, i millisekunder, för att filen ska kunna överföras i sin helhet. Om det anges inkluderas överföringens varaktighet i systemets loggfiler för analys av överföringshastigheten. |
| `fileSize` | Nummer | Valfritt | Filens storlek i byte. Om det anges inkluderas filstorleken i systemets loggfiler för analys av överföringshastighet. |

>[!NOTE]
>
>Om resursen finns och varken `createVersion` eller `replace` har angetts, uppdaterar [!DNL Experience Manager] resursens aktuella version med den nya binärfilen.

Precis som initieringsprocessen kan fullständiga data för begäran innehålla information för mer än en fil.

Överföringen av en binär fil utförs inte förrän den fullständiga URL:en anropas för filen. En resurs bearbetas när överföringen är klar. Bearbetningen startar inte även om resursens binära fil överförs helt, men överföringen inte slutförs. Om överföringen lyckas svarar servern med statuskoden `200`.

### Exempel på Shell-skript för att överföra resurser till AEM as a Cloud Service {#upload-assets-shell-script}

Flerstegsuppladdningsprocessen för direkt binär åtkomst inom AEM as a Cloud Service illustreras i följande exempel på gränssnittsskript `aem-upload.sh`:

```bash
#!/bin/bash

# Check if pv is installed
if ! command -v pv &> /dev/null; then
    echo "Error: 'pv' command not found. Please install it before running the script."
    exit 1
fi

# Check if jq is installed
if ! command -v jq &> /dev/null; then
    echo "Error: 'jq' command not found. Please install it before running the script."
    exit 1
fi

# Set DEBUG to true to enable debug statements
DEBUG=true

# Function for printing debug statements
function debug() {
    if [ "${DEBUG}" = true ]; then
        echo "[DEBUG] $1"
    fi
}

# Function to check if a file exists
function file_exists() {
    [ -e "$1" ]
}

# Function to check if a path is a directory
function is_directory() {
    [ -d "$1" ]
}

# Check if the required number of parameters are provided
if [ "$#" -ne 4 ]; then
    echo "Usage: $0 <aem-url> <asset-folder> <file-to-upload> <bearer-token>"
    exit 1
fi

AEM_URL="$1"
ASSET_FOLDER="$2"
FILE_TO_UPLOAD="$3"
BEARER_TOKEN="$4"

# Extracting file name or folder name from the file path
NAME=$(basename "${FILE_TO_UPLOAD}")

# Step 1: Check if "file-to-upload" is a folder
if is_directory "${FILE_TO_UPLOAD}"; then
    echo "Uploading files from the folder recursively..."
    
    # Recursively upload files in the folder
    find "${FILE_TO_UPLOAD}" -type f | while read -r FILE_PATH; do
        FILE_NAME=$(basename "${FILE_PATH}")
        debug "Uploading file: ${FILE_PATH}"
        
        # You can choose to initiate upload for each file here
        # For simplicity, let's assume you use the same ASSET_FOLDER for all files
        ./aem-upload.sh "${AEM_URL}" "${ASSET_FOLDER}" "${FILE_PATH}" "${BEARER_TOKEN}"
    done
else
    # "file-to-upload" is a single file
    FILE_NAME="${NAME}"

    # Step 2: Calculate File Size
    FILE_SIZE=$(stat -c %s "${FILE_TO_UPLOAD}")

    # Step 3: Initiate Upload
    INITIATE_UPLOAD_ENDPOINT="${AEM_URL}/content/dam/${ASSET_FOLDER}.initiateUpload.json"

    debug "Initiating upload..."
    debug "Initiate Upload Endpoint: ${INITIATE_UPLOAD_ENDPOINT}"
    debug "File Name: ${FILE_NAME}"
    debug "File Size: ${FILE_SIZE}"

    INITIATE_UPLOAD_RESPONSE=$(curl -X POST \
        -H "Authorization: Bearer ${BEARER_TOKEN}" \
        -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" \
        -d "fileName=${FILE_NAME}" \
        -d "fileSize=${FILE_SIZE}" \
        ${INITIATE_UPLOAD_ENDPOINT})

    # Continue with the rest of the script...
fi


# Check if the response body contains the specified HTML content for a 404 error
if echo "${INITIATE_UPLOAD_RESPONSE}" | grep -q "<title>404 Specified folder not found</title>"; then
    echo "Folder not found. Creating the folder..."

    # Attempt to create the folder
    CREATE_FOLDER_ENDPOINT="${AEM_URL}/api/assets/${ASSET_FOLDER}"

    debug "Creating folder..."
    debug "Create Folder Endpoint: ${CREATE_FOLDER_ENDPOINT}"

    CREATE_FOLDER_RESPONSE=$(curl -X POST \
        -H "Content-Type: application/json" \
        -H "Authorization: Bearer ${BEARER_TOKEN}" \
        -d '{"class":"'${ASSET_FOLDER}'","properties":{"title":"'${ASSET_FOLDER}'"}}' \
        ${CREATE_FOLDER_ENDPOINT})

    # Check the response code and inform the user accordingly
    STATUS_CODE_CREATE_FOLDER=$(echo "${CREATE_FOLDER_RESPONSE}" | jq -r '.properties."status.code"')
    case ${STATUS_CODE_CREATE_FOLDER} in
        201)
            echo "Folder created successfully. Initiating upload again..."

            # Retry Initiate Upload after creating the folder
            INITIATE_UPLOAD_RESPONSE=$(curl -X POST \
                -H "Authorization: Bearer ${BEARER_TOKEN}" \
                -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" \
                -d "fileName=${FILE_NAME}" \
                -d "fileSize=${FILE_SIZE}" \
                ${INITIATE_UPLOAD_ENDPOINT})
            ;;
        409)
            echo "Error: Folder already exists."
            ;;
        412)
            echo "Error: Precondition failed. Root collection cannot be found or accessed."
            exit 1
            ;;
        500)
            echo "Error: Internal Server Error. Something went wrong."
            exit 1
            ;;
        *)
            echo "Error: Unexpected response code ${STATUS_CODE_CREATE_FOLDER}"
            exit 1
            ;;
    esac
fi

# Extracting values from the response
FOLDER_PATH=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.folderPath')
UPLOAD_URIS=($(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].uploadURIs[]'))
UPLOAD_TOKEN=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].uploadToken')
MIME_TYPE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].mimeType')
MIN_PART_SIZE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].minPartSize')
MAX_PART_SIZE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].maxPartSize')
COMPLETE_URI=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.completeURI')

# Extracting "Affinity-cookie" from the response headers
AFFINITY_COOKIE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | grep -i 'Affinity-cookie' | awk '{print $2}')

debug "Folder Path: ${FOLDER_PATH}"
debug "Upload Token: ${UPLOAD_TOKEN}"
debug "MIME Type: ${MIME_TYPE}"
debug "Min Part Size: ${MIN_PART_SIZE}"
debug "Max Part Size: ${MAX_PART_SIZE}"
debug "Complete URI: ${COMPLETE_URI}"
debug "Affinity Cookie: ${AFFINITY_COOKIE}"
if $DEBUG; then
    i=1
    for UPLOAD_URI in "${UPLOAD_URIS[@]}"; do
        debug "Upload URI $i: "$UPLOAD_URI
        i=$((i+1))
    done
fi


# Calculate the number of parts needed
NUM_PARTS=$(( (FILE_SIZE + MAX_PART_SIZE - 1) / MAX_PART_SIZE ))
debug "Number of Parts: $NUM_PARTS"

# Calculate the part size for the last chunk
LAST_PART_SIZE=$(( FILE_SIZE % MAX_PART_SIZE ))
if [ "${LAST_PART_SIZE}" -eq 0 ]; then
    LAST_PART_SIZE=${MAX_PART_SIZE}
fi

# Step 4: Upload binary to the blob store in parts
PART_NUMBER=1
for i in $(seq 1 $NUM_PARTS); do
    PART_SIZE=${MAX_PART_SIZE}
    if [ ${PART_NUMBER} -eq ${NUM_PARTS} ]; then
        PART_SIZE=${LAST_PART_SIZE}
        debug "Last part size: ${PART_SIZE}"
    fi

    PART_FILE="/tmp/${FILE_NAME}_part${PART_NUMBER}"

    # Creating part file 
    SKIP=$((PART_NUMBER - 1))
    SKIP=$((MAX_PART_SIZE * SKIP))
    dd if="${FILE_TO_UPLOAD}" of="${PART_FILE}"  bs="${PART_SIZE}" skip="${SKIP}" count="${PART_SIZE}" iflag=skip_bytes,count_bytes  > /dev/null 2>&1
    debug "Creating part file: ${PART_FILE} with size ${PART_SIZE}, skipping first ${SKIP} bytes."

    
    UPLOAD_URI=${UPLOAD_URIS[$PART_NUMBER-1]}

    debug "Uploading part ${PART_NUMBER}..."
    debug "Part Size: $PART_SIZE"
    debug "Part File: ${PART_FILE}"
    debug "Part File Size: $(stat -c %s "${PART_FILE}")"
    debug "Upload URI: ${UPLOAD_URI}"

    # Upload the part in the background
    if command -v pv &> /dev/null; then
        pv "${PART_FILE}" | curl --progress-bar -X PUT --data-binary "@-" "${UPLOAD_URI}" &
    else
        curl -# -X PUT --data-binary "@${PART_FILE}" "${UPLOAD_URI}" &
    fi

    PART_NUMBER=$((PART_NUMBER + 1))
done

# Wait for all background processes to finish
wait

# Step 5: Complete the upload in AEM
COMPLETE_UPLOAD_ENDPOINT="${AEM_URL}${COMPLETE_URI}"

debug "Completing the upload..."
debug "Complete Upload Endpoint: ${COMPLETE_UPLOAD_ENDPOINT}"

RESPONSE=$(curl -X POST \
    -H "Authorization: Bearer ${BEARER_TOKEN}" \
    -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" \
    -H "Affinity-cookie: ${AFFINITY_COOKIE}" \
    --data-urlencode "uploadToken=${UPLOAD_TOKEN}" \
    --data-urlencode "fileName=${FILE_NAME}" \
    --data-urlencode "mimeType=${MIME_TYPE}" \
    "${COMPLETE_UPLOAD_ENDPOINT}")
    
debug $RESPONSE

echo "File upload completed successfully."
```

### Överföringsbibliotek med öppen källkod {#open-source-upload-library}

Adobe tillhandahåller bibliotek och verktyg med öppen källkod för att lära dig mer om överföringsalgoritmerna eller för att bygga egna uppladdningsskript och verktyg:

* [Öppna källans e-postöverföringsbibliotek](https://github.com/adobe/aem-upload).
* [Kommandoradsverktyget för öppen källkod](https://github.com/adobe/aio-cli-plugin-aem).

>[!NOTE]
>
>Både aem-upload-biblioteket och kommandoradsverktyget använder [node-httptransfer library](https://github.com/adobe/node-httptransfer/)

### Inaktuella API:er för överföring av resurser {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

Den nya överföringsmetoden stöds bara för [!DNL Adobe Experience Manager] som [!DNL Cloud Service]. API:erna från [!DNL Adobe Experience Manager] 6.5 är inaktuella. Metoderna för att överföra eller uppdatera resurser eller återgivningar (all binär överföring) är ersatta i följande API:er:

* [EXPERIENCE MANAGER ASSETS HTTP API](mac-api-assets.md)
* `AssetManager` Java API, som `AssetManager.createAsset(..)`, `AssetManager.createAssetForBinary(..)`, `AssetManager.getAssetForBinary(..)`, `AssetManager.removeAssetForBinary(..)`, `AssetManager.createOrUpdateAsset(..)`, `AssetManager.createOrReplaceAsset(..)`

>[!MORELIKETHIS]
>
>* [Öppna källans e-postöverföringsbibliotek](https://github.com/adobe/aem-upload).
>* [Kommandoradsverktyget för öppen källkod](https://github.com/adobe/aio-cli-plugin-aem).
>* [Apache Jackrabbit Oak-dokumentation för direktöverföring](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload).

## Tillgångshantering och efterbearbetning av arbetsflöden {#post-processing-workflows}

I [!DNL Experience Manager] baseras resursbearbetningen på **[!UICONTROL Processing Profiles]**-konfigurationen som använder [objektmikrotjänster](asset-microservices-configure-and-use.md#get-started-using-asset-microservices). Bearbetningen kräver inga utvecklartillägg.

Använd standardarbetsflödena med tillägg med anpassade steg för konfiguration av efterbearbetning av arbetsflöde.

## Stöd för arbetsflödessteg i efterbearbetningsarbetsflödet {#post-processing-workflows-steps}

Om du uppgraderar från en tidigare version av [!DNL Experience Manager] kan du använda resursmikrotjänster för att bearbeta resurser. De molnbaserade mikrotjänsterna är enklare att konfigurera och använda. Ett fåtal arbetsflödessteg som används i arbetsflödet [!UICONTROL DAM Update Asset] i den tidigare versionen stöds inte. Mer information om klasser som stöds finns i [Java API-referensen eller Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

Följande tekniska arbetsflödesmodeller ersätts av resursmikrotjänster eller så är support inte tillgänglig:

* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.switchengine.process.SwitchEngineHandlingProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`

<!-- Commenting the previous list documented at the time of GA. Replacing it with the updated list via cqdoc-18231.

* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.ScheduledPublishBPProcess`
* `com.day.cq.dam.core.process.ScheduledUnPublishBPProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
-->

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publicera Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [[!DNL Experience Cloud] som en [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).