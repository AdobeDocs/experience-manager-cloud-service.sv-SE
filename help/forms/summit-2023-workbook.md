---
title: Bygg engagerande Forms med kärnkomponenter och headless
seo-title: Build Engaging Forms Using Core Components and Headless
description: Bygg engagerande Forms med kärnkomponenter och headless
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
hide: true
hidefromtoc: true
source-git-commit: aa278ca4b2a617593512cab45100d8d4e15fd6eb
workflow-type: tm+mt
source-wordcount: '7032'
ht-degree: 10%

---


# Bygg engagerande Forms med kärnkomponenter och headless

## Lab-översikt

I detta praktiska labb lär du dig:

Hur man använder AEM Forms för att enkelt skapa anpassningsbara formulär med hjälp av de senaste kärnkomponenterna som är förenliga med AEM Sites, möjliggör datainhämtning i flera kanaler genom att leverera de adaptiva formulären som headless-formulär till webben, mobiler och chatt. Du får också lära dig de effektivaste strategierna när det gäller format, anpassningar och gränssnittsutveckling.

## Viktiga uppgifter

* **Affärsflexibilitet**: Som affärsanvändare kan jag enkelt skapa formulärupplevelser för flera kanaler.

* **Framåtutvecklare**: Som frontutvecklare kan jag styra användarupplevelsen med headless-formulär.

* **Utvecklarhastighet**: Som utvecklare kan jag enkelt och konsekvent anpassa webbplatser och Forms-komponenter.

## Förutsättningar

* AEM Forms som Cloud Service, sandlåda

   <table>
        <thead>
            <tr><th>name</th><th>program-ID</th><th>miljö-ID</th><th>användarnamn</th><th>pipeline-utlösare vid implementering</th><th>databas-URL</th><th>front end - branch and repo</th><th>namn på front end-repo</th><th>frontend-pipeline</th><th>länk</th><th>program-URL</th><th>URL för miljölista</th><th>front end repo url</th><th>växlar url</th></tr>           
        </thead>
        <tbody>
            <tr><td>L716001</td><td>105303</td><td>986623</td><td>L716+001@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716001-p105303-uk94266/</td><td>ja</td><td>wknd</td><td>ja</td><td>https://author-p105303-e986623.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/105303</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/105303</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wkndtheme</td><td>https://author-p105303-e986623.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716002</td><td>106405</td><td>993047</td><td>L716+002@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716002-p106405-uk30744/</td><td>ja</td><td>wknd2</td><td>ja</td><td>https://author-p106405-e993047.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106405</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106405</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wkndtheme2/</td><td>https://author-p106405-e993047.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716003</td><td>106406</td><td>993049</td><td>L716+003@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716003-p106406-uk82969/</td><td>ja</td><td>wknd3</td><td>ja</td><td>https://author-p106406-e993049.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106406</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106406</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wkndtheme3/</td><td>https://author-p106406-e993049.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716004</td><td>106398</td><td>993114</td><td>L716+004@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716004-p106398-uk62851/</td><td>ja</td><td>wknd4</td><td>ja</td><td>https://author-p106398-e993114.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106398</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106398</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wkndtheme4/</td><td>https://author-p106398-e993114.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716005</td><td>106407</td><td>993048</td><td>L716+005@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716005-p106407-uk76414/</td><td>ja</td><td>wknd5</td><td>ja</td><td>https://author-p106407-e993048.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106407</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106407</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wkndtheme5/</td><td>https://author-p106407-e993048.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716006</td><td>106408</td><td>993155</td><td>L716+006@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716006-p106408-uk98879/</td><td>ja</td><td>wknd6</td><td>ja</td><td>https://author-p106408-e993155.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106408</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106408</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wkndtheme6/</td><td>https://author-p106408-e993155.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716007</td><td>106343</td><td>993067</td><td>L716+007@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716007-p106343-uk17215/</td><td>ja</td><td>wknd7</td><td>ja</td><td>https://author-p106343-e993067.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106343</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106343</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wkndtheme7</td><td>https://author-p106343-e993067.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716008</td><td>106399</td><td>993108</td><td>L716+008@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716008-p106399-uk50450/</td><td>ja</td><td>wknd8</td><td>ja</td><td>https://author-p106399-e993108.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106399</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106399</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wkndtheme8</td><td>https://author-p106399-e993108.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716009</td><td>106344</td><td>993064</td><td>L716+009@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716009-p106344-uk63538/</td><td>ja</td><td>wknd9</td><td>ja</td><td>https://author-p106344-e993064.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106344</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106344</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wkndtheme9/</td><td>https://author-p106344-e993064.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716010</td><td>106409</td><td>993051</td><td>L716+010@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716010-p106409-uk19656/</td><td>ja</td><td>wknd10</td><td>ja</td><td>https://author-p106409-e993051.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106409</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106409</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd10</td><td>https://author-p106409-e993051.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716011</td><td>106345</td><td>993060</td><td>L716+011@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716011-p106345-uk54192/</td><td>ja</td><td>wknd11</td><td>ja</td><td>https://author-p106345-e993060.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106345</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106345</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd11</td><td>https://author-p106345-e993060.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716012</td><td>106346</td><td>993061</td><td>L716+012@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716012-p106346-uk49638/</td><td>ja</td><td>wknd12</td><td>ja</td><td>https://author-p106346-e993061.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106346</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106346</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd12</td><td>https://author-p106346-e993061.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716013</td><td>106410</td><td>993153</td><td>L716+013@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716013-p106410-uk94707/</td><td>ja</td><td>wknd13</td><td>ja</td><td>https://author-p106410-e993153.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106410</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106410</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd13</td><td>https://author-p106410-e993153.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716014</td><td>106502</td><td>993073</td><td>L716+014@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716014-p106502-uk23328/</td><td>ja</td><td>wknd14</td><td>ja</td><td>https://author-p106502-e993073.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106502</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106502</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd14</td><td>https://author-p106502-e993073.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716015</td><td>106401</td><td>993112</td><td>L716+015@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716015-p106401-uk94501/</td><td>ja</td><td>wknd15</td><td>ja</td><td>https://author-p106401-e993112.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106401</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106401</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd15</td><td>https://author-p106401-e993112.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716016</td><td>106452</td><td>993115</td><td>L716+016@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716016-p106452-uk35087/</td><td>ja</td><td>wknd16</td><td>ja</td><td>https://author-p106452-e993115.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106452</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106452</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd16</td><td>https://author-p106452-e993115.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716017</td><td>106453</td><td>993113</td><td>L716+017@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716017-p106453-uk55732/</td><td>ja</td><td>wknd17</td><td>ja</td><td>https://author-p106453-e993113.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106453</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106453</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd17</td><td>https://author-p106453-e993113.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716018</td><td>106411</td><td>993050</td><td>L716+018@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716018-p106411-uk77613/</td><td>ja</td><td>wknd18</td><td>ja</td><td>https://author-p106411-e993050.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106411</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106411</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd18</td><td>https://author-p106411-e993050.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716019</td><td>106454</td><td>993116</td><td>L716+019@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716019-p106454-uk19216/</td><td>ja</td><td>wknd19</td><td>ja</td><td>https://author-p106454-e993116.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106454</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106454</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd19</td><td>https://author-p106454-e993116.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716020</td><td>106347</td><td>993063</td><td>L716+020@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716020-p106347-uk53952/</td><td>ja</td><td>wknd20</td><td>ja</td><td>https://author-p106347-e993063.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106347</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106347</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd20</td><td>https://author-p106347-e993063.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716021</td><td>106455</td><td>993109</td><td>L716+021@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716021-p106455-uk24058/</td><td>ja</td><td>wknd21</td><td>ja</td><td>https://author-p106455-e993109.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106455</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106455</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd21</td><td>https://author-p106455-e993109.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716022</td><td>106456</td><td>993110</td><td>L716+022@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716022-p106456-uk26793/</td><td>ja</td><td>wknd22</td><td>ja</td><td>https://author-p106456-e993110.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106456</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106456</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd22</td><td>https://author-p106456-e993110.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716023</td><td>106466</td><td>993291</td><td>L716+023@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716023-p106466-uk93719/</td><td>ja</td><td>wknd23</td><td>ja</td><td>https://author-p106466-e993291.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106466</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106466</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd23</td><td>https://author-p106466-e993291.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716024</td><td>106413</td><td>993156</td><td>L716+024@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716024-p106413-uk10856/</td><td>ja</td><td>wknd24</td><td>ja</td><td>https://author-p106413-e993156.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106413</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106413</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd24</td><td>https://author-p106413-e993156.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716025</td><td>106348</td><td>993066</td><td>L716+025@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716025-p106348-uk76381/</td><td>ja</td><td>wknd25</td><td>ja</td><td>https://author-p106348-e993066.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106348</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106348</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd25</td><td>https://author-p106348-e993066.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716026</td><td>106414</td><td>993154</td><td>L716+026@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716026-p106414-uk93983/</td><td>ja</td><td>wknd26</td><td>ja</td><td>https://author-p106414-e993154.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106414</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106414</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd26</td><td>https://author-p106414-e993154.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716027</td><td>106349</td><td>993065</td><td>L716+027@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716027-p106349-uk75744/</td><td>ja</td><td>wknd27</td><td>ja</td><td>https://author-p106349-e993065.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106349</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106349</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd27</td><td>https://author-p106349-e993065.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716028</td><td>106415</td><td>993152</td><td>L716+028@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716028-p106415-uk24248/</td><td>ja</td><td>wknd28</td><td>ja</td><td>https://author-p106415-e993152.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106415</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106415</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd28</td><td>https://author-p106415-e993152.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716029</td><td>106350</td><td>993068</td><td>L716+029@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716029-p106350-uk06304/</td><td>ja</td><td>wknd29</td><td>ja</td><td>https://author-p106350-e993068.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106350</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106350</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd29</td><td>https://author-p106350-e993068.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716030</td><td>106351</td><td>993062</td><td>L716+030@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716030-p106351-uk95707/</td><td>ja</td><td>wknd30</td><td>ja</td><td>https://author-p106351-e993062.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106351</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106351</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd30</td><td>https://author-p106351-e993062.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716031</td><td>106417</td><td>993158</td><td>L716+031@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716031-p106417-uk50022/</td><td>ja</td><td>wknd31</td><td>ja</td><td>https://author-p106417-e993158.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106417</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106417</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd31</td><td>https://author-p106417-e993158.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716032</td><td>106418</td><td>993159</td><td>L716+032@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716032-p106418-uk75663/</td><td>ja</td><td>wknd32</td><td>ja</td><td>https://author-p106418-e993159.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106418</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106418</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd32</td><td>https://author-p106418-e993159.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716033</td><td>106503</td><td>993080</td><td>L716+033@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716033-p106503-uk29541/</td><td>ja</td><td>wknd33</td><td>ja</td><td>https://author-p106503-e993080.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106503</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106503</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd33</td><td>https://author-p106503-e993080.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716034</td><td>106457</td><td>993125</td><td>L716+034@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716034-p106457-uk91438/</td><td>ja</td><td>wknd34</td><td>ja</td><td>https://author-p106457-e993125.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106457</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106457</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd34</td><td>https://author-p106457-e993125.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716035</td><td>106504</td><td>993081</td><td>L716+035@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716035-p106504-uk46573/</td><td>ja</td><td>wknd35</td><td>ja</td><td>https://author-p106504-e993081.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106504</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106504</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd35</td><td>https://author-p106504-e993081.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716036</td><td>106458</td><td>993120</td><td>L716+036@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716036-p106458-uk91382/</td><td>ja</td><td>wknd36</td><td>ja</td><td>https://author-p106458-e993120.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106458</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106458</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd36</td><td>https://author-p106458-e993120.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716037</td><td>106419</td><td>993160</td><td>L716+037@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716037-p106419-uk99235/</td><td>ja</td><td>wknd37</td><td>ja</td><td>https://author-p106419-e993160.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106419</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106419</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd37</td><td>https://author-p106419-e993160.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716038</td><td>106420</td><td>993162</td><td>L716+038@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716038-p106420-uk24222/</td><td>ja</td><td>wknd38</td><td>ja</td><td>https://author-p106420-e993162.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106420</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106420</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd38</td><td>https://author-p106420-e993162.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716039</td><td>106517</td><td>993235</td><td>L716+039@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716039-p106517-uk88649/</td><td>ja</td><td>wknd39</td><td>ja</td><td>https://author-p106517-e993235.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106517</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106517</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd39</td><td>https://author-p106517-e993235.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716040</td><td>106506</td><td>993079</td><td>L716+040@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716040-p106506-uk58481/</td><td>ja</td><td>wknd40</td><td>ja</td><td>https://author-p106506-e993079.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106506</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106506</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd40</td><td>https://author-p106506-e993079.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716041</td><td>106507</td><td>993074</td><td>L716+041@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716041-p106507-uk39478/</td><td>ja</td><td>wknd41</td><td>ja</td><td>https://author-p106507-e993074.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106507</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106507</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd41</td><td>https://author-p106507-e993074.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716042</td><td>106508</td><td>993075</td><td>L716+042@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716042-p106508-uk03034/</td><td>ja</td><td>wknd42</td><td>ja</td><td>https://author-p106508-e993075.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106508</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106508</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd42</td><td>https://author-p106508-e993075.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716043</td><td>106421</td><td>993163</td><td>L716+043@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716043-p106421-uk19734/</td><td>ja</td><td>wknd43</td><td>ja</td><td>https://author-p106421-e993163.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106421</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106421</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd43</td><td>https://author-p106421-e993163.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716044</td><td>106459</td><td>993121</td><td>L716+044@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716044-p106459-uk31012/</td><td>ja</td><td>wknd44</td><td>ja</td><td>https://author-p106459-e993121.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106459</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106459</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd44</td><td>https://author-p106459-e993121.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716045</td><td>106467</td><td>993292</td><td>L716+045@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716045-p106467-uk08507/</td><td>ja</td><td>wknd45</td><td>ja</td><td>https://author-p106467-e993292.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106467</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106467</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd45</td><td>https://author-p106467-e993292.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716046</td><td>106518</td><td>993234</td><td>L716+046@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716046-p106518-uk42276/</td><td>ja</td><td>wknd46</td><td>ja</td><td>https://author-p106518-e993234.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106518</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106518</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd46</td><td>https://author-p106518-e993234.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716047</td><td>106511</td><td>993076</td><td>L716+047@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716047-p106511-uk14074/</td><td>ja</td><td>wknd47</td><td>ja</td><td>https://author-p106511-e993076.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106511</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106511</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd47</td><td>https://author-p106511-e993076.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716048</td><td>106512</td><td>993077</td><td>L716+048@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716048-p106512-uk09248/</td><td>ja</td><td>wknd48</td><td>ja</td><td>https://author-p106512-e993077.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106512</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106512</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd48</td><td>https://author-p106512-e993077.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716049</td><td>106460</td><td>993124</td><td>L716+049@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716049-p106460-uk30141/</td><td>ja</td><td>wknd49</td><td>ja</td><td>https://author-p106460-e993124.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106460</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106460</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd49</td><td>https://author-p106460-e993124.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716050</td><td>106519</td><td>993237</td><td>L716+050@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716050-p106519-uk22660/</td><td>ja</td><td>wknd50</td><td>ja</td><td>https://author-p106519-e993237.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106519</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106519</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd50</td><td>https://author-p106519-e993237.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716051</td><td>106513</td><td>993084</td><td>L716+051@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716051-p106513-uk50830/</td><td>ja</td><td>wknd51</td><td>ja</td><td>https://author-p106513-e993084.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106513</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106513</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd51</td><td>https://author-p106513-e993084.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716052</td><td>106461</td><td>993122</td><td>L716+052@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716052-p106461-uk73956/</td><td>ja</td><td>wknd52</td><td>ja</td><td>https://author-p106461-e993122.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106461</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106461</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd52</td><td>https://author-p106461-e993122.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716053</td><td>106514</td><td>993082</td><td>L716+053@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716053-p106514-uk25965/</td><td>ja</td><td>wknd53</td><td>ja</td><td>https://author-p106514-e993082.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106514</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106514</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd53</td><td>https://author-p106514-e993082.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716054</td><td>106462</td><td>993123</td><td>L716+054@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716054-p106462-uk07017/</td><td>ja</td><td>wknd54</td><td>ja</td><td>https://author-p106462-e993123.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106462</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106462</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd54</td><td>https://author-p106462-e993123.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716055</td><td>106463</td><td>993127</td><td>L716+055@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716055-p106463-uk94955/</td><td>ja</td><td>wknd55</td><td>ja</td><td>https://author-p106463-e993127.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106463</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106463</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd55</td><td>https://author-p106463-e993127.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716056</td><td>106515</td><td>993083</td><td>L716+056@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716056-p106515-uk12658/</td><td>ja</td><td>wknd56</td><td>ja</td><td>https://author-p106515-e993083.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106515</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106515</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd56</td><td>https://author-p106515-e993083.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716057</td><td>106464</td><td>993126</td><td>L716+057@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716057-p106464-uk13238/</td><td>ja</td><td>wknd57</td><td>ja</td><td>https://author-p106464-e993126.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106464</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106464</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd57</td><td>https://author-p106464-e993126.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716058</td><td>106520</td><td>993236</td><td>L716+058@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716058-p106520-uk93785/</td><td>ja</td><td>wknd58</td><td>ja</td><td>https://author-p106520-e993236.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106520</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106520</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd58</td><td>https://author-p106520-e993236.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716059</td><td>106423</td><td>993161</td><td>L716+059@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716059-p106423-uk31356/</td><td>ja</td><td>wknd59</td><td>ja</td><td>https://author-p106423-e993161.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106423</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106423</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd59</td><td>https://author-p106423-e993161.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716060</td><td>106516</td><td>993078</td><td>L716+060@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716060-p106516-uk84089/</td><td>ja</td><td>wknd60</td><td>ja</td><td>https://author-p106516-e993078.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106516</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106516</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd60</td><td>https://author-p106516-e993078.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716061</td><td>106521</td><td>993240</td><td>L716+061@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716061-p106521-uk14423/</td><td>ja</td><td>wknd61</td><td>ja</td><td>https://author-p106521-e993240.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106521</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106521</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd61</td><td>https://author-p106521-e993240.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716062</td><td>106424</td><td>993308</td><td>L716+062@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716062-p106424-uk04070/</td><td>ja</td><td>wknd62</td><td>ja</td><td>https://author-p106424-e993308.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106424</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106424</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd62</td><td>https://author-p106424-e993308.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716063</td><td>106468</td><td>993295</td><td>L716+063@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716063-p106468-uk65739/</td><td>ja</td><td>wknd63</td><td>ja</td><td>https://author-p106468-e993295.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106468</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106468</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd63</td><td>https://author-p106468-e993295.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716064</td><td>106425</td><td>993309</td><td>L716+064@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716064-p106425-uk89411/</td><td>ja</td><td>wknd64</td><td>ja</td><td>https://author-p106425-e993309.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106425</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106425</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd64</td><td>https://author-p106425-e993309.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716065</td><td>106426</td><td>993314</td><td>L716+065@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716065-p106426-uk38598/</td><td>ja</td><td>wknd65</td><td>ja</td><td>https://author-p106426-e993314.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106426</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106426</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd65</td><td>https://author-p106426-e993314.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716066</td><td>106469</td><td>993293</td><td>L716+066@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716066-p106469-uk05356/</td><td>ja</td><td>wknd66</td><td>ja</td><td>https://author-p106469-e993293.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106469</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106469</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd66</td><td>https://author-p106469-e993293.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716067</td><td>106522</td><td>993238</td><td>L716+067@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716067-p106522-uk44251/</td><td>ja</td><td>wknd67</td><td>ja</td><td>https://author-p106522-e993238.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106522</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106522</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd67</td><td>https://author-p106522-e993238.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716068</td><td>106470</td><td>993299</td><td>L716+068@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716068-p106470-uk32462/</td><td>ja</td><td>wknd68</td><td>ja</td><td>https://author-p106470-e993299.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106470</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106470</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd68</td><td>https://author-p106470-e993299.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716069</td><td>106427</td><td>993311</td><td>L716+069@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716069-p106427-uk83971/</td><td>ja</td><td>wknd69</td><td>ja</td><td>https://author-p106427-e993311.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106427</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106427</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd69</td><td>https://author-p106427-e993311.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716070</td><td>106428</td><td>993310</td><td>L716+070@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716070-p106428-uk60835/</td><td>ja</td><td>wknd70</td><td>ja</td><td>https://author-p106428-e993310.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106428</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106428</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd70</td><td>https://author-p106428-e993310.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716071</td><td>106471</td><td>993298</td><td>L716+071@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716071-p106471-uk86739/</td><td>ja</td><td>wknd71</td><td>ja</td><td>https://author-p106471-e993298.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106471</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106471</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd71</td><td>https://author-p106471-e993298.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716072</td><td>106429</td><td>993315</td><td>L716+072@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716072-p106429-uk23084/</td><td>ja</td><td>wknd72</td><td>ja</td><td>https://author-p106429-e993315.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106429</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106429</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd72</td><td>https://author-p106429-e993315.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716073</td><td>106523</td><td>993239</td><td>L716+073@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716073-p106523-uk23422/</td><td>ja</td><td>wknd73</td><td>ja</td><td>https://author-p106523-e993239.adobeaemcloud.com/</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106523</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106523</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd73</td><td>https://author-p106523-e993239.adobeaemcloud.com//etc.clientlibs/toggles.json</td></tr><tr><td>L716074</td><td>106472</td><td>993300</td><td>L716+074@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716074-p106472-uk38017/</td><td>ja</td><td>wknd74</td><td>ja</td><td>https://author-p106472-e993300.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106472</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106472</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd74</td><td>https://author-p106472-e993300.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716075</td><td>106430</td><td>993312</td><td>L716+075@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716075-p106430-uk55913/</td><td>ja</td><td>wknd75</td><td>ja</td><td>https://author-p106430-e993312.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106430</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106430</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd75</td><td>https://author-p106430-e993312.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716076</td><td>106524</td><td>993241</td><td>L716+076@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716076-p106524-uk94081/</td><td>ja</td><td>wknd76</td><td>ja</td><td>https://author-p106524-e993241.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106524</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106524</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd76</td><td>https://author-p106524-e993241.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716077</td><td>106431</td><td>993313</td><td>L716+077@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716077-p106431-uk09241/</td><td>ja</td><td>wknd77</td><td>ja</td><td>https://author-p106431-e993313.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106431</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106431</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd77</td><td>https://author-p106431-e993313.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716078</td><td>106473</td><td>993294</td><td>L716+078@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716078-p106473-uk84023/</td><td>ja</td><td>wknd78</td><td>ja</td><td>https://author-p106473-e993294.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106473</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106473</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd78</td><td>https://author-p106473-e993294.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716079</td><td>106474</td><td>993297</td><td>L716+079@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716079-p106474-uk83600/</td><td>ja</td><td>wknd79</td><td>ja</td><td>https://author-p106474-e993297.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106474</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106474</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd79</td><td>https://author-p106474-e993297.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716080</td><td>106475</td><td>993296</td><td>L716+080@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716080-p106475-uk94755/</td><td>ja</td><td>wknd80</td><td>ja</td><td>https://author-p106475-e993296.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106475</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106475</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd80</td><td>https://author-p106475-e993296.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716081</td><td>106476</td><td>993353</td><td>L716+081@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716081-p106476-uk50558/</td><td>ja</td><td>wknd81</td><td>ja</td><td>https://author-p106476-e993353.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106476</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106476</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd81</td><td>https://author-p106476-e993353.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716082</td><td>106525</td><td>993247</td><td>L716+082@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716082-p106525-uk92893/</td><td>ja</td><td>wknd82</td><td>ja</td><td>https://author-p106525-e993247.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106525</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106525</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd82</td><td>https://author-p106525-e993247.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716083</td><td>106526</td><td>993244</td><td>L716+083@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716083-p106526-uk35635/</td><td>ja</td><td>wknd83</td><td>ja</td><td>https://author-p106526-e993244.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106526</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106526</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd83</td><td>https://author-p106526-e993244.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716084</td><td>106527</td><td>993243</td><td>L716+084@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716084-p106527-uk33428/</td><td>ja</td><td>wknd84</td><td>ja</td><td>https://author-p106527-e993243.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106527</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106527</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd84</td><td>https://author-p106527-e993243.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716085</td><td>106477</td><td>993356</td><td>L716+085@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716085-p106477-uk07483/</td><td>ja</td><td>wknd85</td><td>ja</td><td>https://author-p106477-e993356.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106477</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106477</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd85</td><td>https://author-p106477-e993356.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716086</td><td>106478</td><td>993355</td><td>L716+086@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716086-p106478-uk19752/</td><td>ja</td><td>wknd86</td><td>ja</td><td>https://author-p106478-e993355.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106478</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106478</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd86</td><td>https://author-p106478-e993355.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716087</td><td>106528</td><td>993245</td><td>L716+087@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716087-p106528-uk65196/</td><td>ja</td><td>wknd87</td><td>ja</td><td>https://author-p106528-e993245.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106528</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106528</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd87</td><td>https://author-p106528-e993245.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716088</td><td>106432</td><td>993316</td><td>L716+088@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716088-p106432-uk71669/</td><td>ja</td><td>wknd88</td><td>ja</td><td>https://author-p106432-e993316.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106432</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106432</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd88</td><td>https://author-p106432-e993316.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716089</td><td>106529</td><td>993242</td><td>L716+089@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716089-p106529-uk72336/</td><td>ja</td><td>wknd89</td><td>ja</td><td>https://author-p106529-e993242.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106529</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106529</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd89</td><td>https://author-p106529-e993242.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716090</td><td>106436</td><td>993320</td><td>L716+090@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716090-p106436-uk96513/</td><td>ja</td><td>wknd90</td><td>ja</td><td>https://author-p106436-e993320.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106436</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106436</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd90</td><td>https://author-p106436-e993320.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716091</td><td>106480</td><td>993301</td><td>L716+091@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716091-p106480-uk26189/</td><td>ja</td><td>wknd91</td><td>ja</td><td>https://author-p106480-e993301.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106480</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106480</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd91</td><td>https://author-p106480-e993301.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716092</td><td>106530</td><td>993246</td><td>L716+092@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716092-p106530-uk21496/</td><td>ja</td><td>wknd92</td><td>ja</td><td>https://author-p106530-e993246.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106530</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106530</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd92</td><td>https://author-p106530-e993246.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716093</td><td>106481</td><td>993352</td><td>L716+093@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716093-p106481-uk08136/</td><td>ja</td><td>wknd93</td><td>ja</td><td>https://author-p106481-e993352.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106481</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106481</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd93</td><td>https://author-p106481-e993352.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716094</td><td>106482</td><td>993354</td><td>L716+094@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716094-p106482-uk12991/</td><td>ja</td><td>wknd94</td><td>ja</td><td>https://author-p106482-e993354.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106482</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106482</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd94</td><td>https://author-p106482-e993354.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716095</td><td>106531</td><td>993248</td><td>L716+095@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716095-p106531-uk35835/</td><td>ja</td><td>wknd95</td><td>ja</td><td>https://author-p106531-e993248.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106531</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106531</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd95</td><td>https://author-p106531-e993248.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716096</td><td>106483</td><td>993357</td><td>L716+096@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716096-p106483-uk62544/</td><td>ja</td><td>wknd96</td><td>ja</td><td>https://author-p106483-e993357.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106483</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106483</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd96</td><td>https://author-p106483-e993357.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716097</td><td>106433</td><td>993318</td><td>L716+097@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716097-p106433-uk01013/</td><td>ja</td><td>wknd97</td><td>ja</td><td>https://author-p106433-e993318.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106433</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106433</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd97</td><td>https://author-p106433-e993318.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716098</td><td>106532</td><td>993249</td><td>L716+098@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716098-p106532-uk23995/</td><td>ja</td><td>wknd98</td><td>ja</td><td>https://author-p106532-e993249.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106532</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106532</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd98</td><td>https://author-p106532-e993249.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716099</td><td>106434</td><td>993317</td><td>L716+099@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716099-p106434-uk60991/</td><td>ja</td><td>wknd99</td><td>ja</td><td>https://author-p106434-e993317.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106434</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106434</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wknd99</td><td>https://author-p106434-e993317.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr><tr><td>L716100</td><td>106435</td><td>993319</td><td>L716+100@summitlab.us</td><td>ja</td><td>https://git.cloudmanager.adobe.com/summit2023l716/L716100-p106435-uk70663/</td><td>ja</td><td>wknd100</td><td>ja</td><td>https://author-p106435-e993319.adobeaemcloud.com</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/home.html/program/106435</td><td>https://experience.adobe.com/#/@summit2023l716/cloud-manager/environments.html/program/106435</td><td>https://git.cloudmanager.adobe.com/summit2023l716/wkndtheme100</td><td>https://author-p106435-e993319.adobeaemcloud.com/etc.clientlibs/toggles.json</td></tr>
        </tbody>
    </table>

## Lektion 1

### Syfte

Bekanta dig med AEM Forms as a Cloud Service miljö.

### Lektionssammanhang

I den här lektionen lär du dig att bekanta dig med AEM Forms as a Cloud Service miljö genom att navigera i användargränssnittet.

### Utövning

1. Öppna webbläsaren och ange webbadressen till Cloud Servicens författarmiljö. Till exempel:
   [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/start.html](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/start.html)

1. Logga in i Cloud Servicens författarmiljö enligt de delade inloggningsuppgifterna. Till exempel: Användarnamn: [L716+001@summitlab.us](mailto:L716%2B001@summitlab.us)
Lösenord: 
**Adobe123!**

1. När du är inloggad navigerar du till användargränssnittet för AEM Forms. Klicka **Forms**.

   ![](/help/forms/assets/screenshot2028113829.png)

1. Klicka **Forms och dokument**. Stäng alla popup-fönster som rör inställningar eller information.

   ![](/help/forms/assets/screenshot2028113929.png)

   Alla tillgängliga formulär visas.

   ![](/help/forms/assets/screenshot2028114029.png)

## Lektion 2

### Syfte

Skapa ett adaptivt formulär med hjälp av de senaste centrala komponenterna, konfigurera och skicka in formuläret.

### Lektionssammanhang

I den här lektionen kommer du som företagsanvändare att skapa ett anpassningsbart formulär för flera kanaler, som webben, mobiler och chatt, med hjälp av anpassningsbar formulärredigering och standardiserade OOTB-kärnkomponenter för datainhämtning.

### Utövning

1. Skapa en slutpunkt för överföring av formuläret:

   1. Öppna <https://requestbin.com/> på en ny flik i webbläsaren.
      ![](/help/forms/assets/screenshot2028114329.png)

   1. Klicka **Skapa en offentlig behållare** och kopiera slutpunkts-URL:en.
      ![](/help/forms/assets/screenshot202023-03-0120at206.10.0020pm.png)

1. Skapa ett anpassat formulär med hjälp av guidegränssnittet:

   1. Navigera till AEM Forms som Cloud Service och gå till Forms och Dokument på fliken Webbläsare som används i lektion 1.
      ![](/help/forms/assets/screenshot2028114029.png)

   1. Klicka **Skapa** och väljer Adaptiv form.
      ![](/help/forms/assets/screenshot2028114629.png)

   1. Välj **Tom med kärnkomponenter** mall från mallurvalsskärmen enligt nedan:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. Klicka på **Stil** och väljer **wknd-tema** tema enligt nedan:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. Klicka på **Inlämning** och väljer **Skicka till REST-slutpunkt** och ange det publika facket i
      **URL för begäran om POST** enligt nedan:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. Klicka **Skapa**. Ange ett namn och en rubrik för formuläret. Till exempel: **konturer**. Klicka **Skapa**.
      ![](/help/forms/assets/screenshot2028123329.png)

   1. Den adaptiva formulärredigeraren öppnas. Stäng alla popup-fönster eller dialogrutor för inställningar eller information. Klicka på komponentwebbläsaren till vänster och lägg till **Sidfot** -komponenten längst ned i det tomma formuläret.
      ![](/help/forms/assets/screenshot2028121929.png)

   1. Rubriken är en del av den adaptiva formulärmallen. Det gör det enkelt att tillhandahålla ett konsekvent sidhuvud/sidfot i alla adaptiva formulär. Du kan också välja att göra den redigerbar i formuläret, vilket visas för sidfotskomponenten i nästa steg.

   1. Lägg till en **Titel** till formulärets mitt.
      ![](/help/forms/assets/screenshot2028122129.png)

   1. Lägg till en **Textindata** efter komponenten title.
      ![](/help/forms/assets/screenshot2028122329.png)

   1. Lägg till en **Nummerindata** -komponenten.
      ![](/help/forms/assets/screenshot2028122429.png)

   1. Lägg till en **Skicka-knapp** till formuläret.
      ![](/help/forms/assets/screenshot2028122529.png)

   1. Klicka på **Titel** så att **popup-meny** visas. Klicka på **Ikonen Redigera** på menyn för att redigera etiketten.
      ![](/help/forms/assets/screenshot2028122629.png)

   1. Retur `Contact Us` som rubriktext.
      ![](/help/forms/assets/screenshot2028122829.png)

   1. Klicka på **Textindata** så att snabbmenyn visas. Klicka på **Ikonen Redigera** på menyn för att redigera etiketten.
      ![](/help/forms/assets/screenshot2028122929.png)

   1. Retur **Fullständigt namn** som fältetikett.
      ![](/help/forms/assets/screenshot2028123029.png)

   1. Klicka på **Nummerindata** så att snabbmenyn visas. Klicka på **Ikonen Redigera** på menyn för att redigera etiketten.
      ![](/help/forms/assets/screenshot2028123129.png)

   1. Ange **Telefonnummer** som fältetikett.
      ![](/help/forms/assets/screenshot2028123829.png)


1. Lägg till valideringar i formuläret:

   1. Klicka på **Telefonnummer** så att snabbmenyn visas. Klicka på **Ikon för skiftnyckel** på menyn för att konfigurera fältet.
      ![](/help/forms/assets/screenshot2028123429.png)

   1. Öppna **valideringsflik** markerar du fältet **Obligatoriskt** och klicka **Klar**. Meddelandet om att åtgärden lyckades visas.
      ![](/help/forms/assets/screenshot2028123529.png)

      ![](/help/forms/assets/screenshot2028123629.png)

   1. Klicka **Förhandsgranska** för att förhandsgranska formuläret ur ett slutanvändarperspektiv.
      ![](/help/forms/assets/screenshot2028125529.png)

   1. Fyll i formuläret med provdata
      ![](/help/forms/assets/screenshot2028125629.png)

   1. Skicka formuläret
      ![](/help/forms/assets/screenshot2028125729.png)

   1. Kontrollera skickade data på fliken Begäranbehållare.
      ![](/help/forms/assets/screenshot2028125829.png)

Använd ett föriskapat registreringsformulär för den återstående övningen.

1. Öppna AEM Forms gränssnitt, till exempel `https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`och väljer registreringsformuläret.

   ![](/help/forms/assets/screenshot2028115529.png)

1. Klicka **Publicera**.

   ![](/help/forms/assets/screenshot2028115629.png)

   Meddelandet om att åtgärden lyckades visas.

   ![](/help/forms/assets/screenshot2028115729.png)

   Publicerings-URL:en för formuläret skulle likna `https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`.

1. Om du vill visa det publicerade formuläret ska du ersätta program-ID:t (pXXXXXX) och miljö-ID:t (eXXXXXX) i ovanstående URL med ID:n för din miljö.

## Lektion 3

### Syfte

Uppdatera format med hjälp av vedertagna metoder för utveckling av klientprogram.

### Lektionssammanhang

I den här lektionen lär du dig hur du enkelt kan uppdatera format för det tidigare skapade adaptiva formuläret.

### Utövning

Konfigurera lokal databas för temat:

1. Öppna kommandotolken eller kommandotolken med administratörsbehörighet:

   ![](/help/forms/assets/screenshot2028115829.png)

1. Använd följande kommando på kommandotolken för att navigera till **c:\git** mapp

   ```Shell
   cd c:\git
   ```

1. Använd följande kommando för att klona koden för temat Framtend:

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. Använd följande kommando i den listade ordningen för att navigera till **aem-forms-theme-canvas** och öppna Visual Studio Code.

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/forms/assets/screenshot2028126029.png)

1. Välj **Författarna av alla filer i den överordnade mappen är betrodda** och klicka **Ja, jag litar på författarna**.

   ![](/help/forms/assets/screenshot2028116229.png)

1. Om du vill återge formuläret som finns i molntjänstens publiceringsmiljö byter du namn på `env_template` -fil.  Om du vill byta namn på filen högerklickar du på **env_template** och väljer **Byt namn** alternativ.

   ![](/help/forms/assets/screenshot2028116429.png)

   </br>

   ![](/help/forms/assets/screenshot2028116529.png)

1. Ange följande värden för variablerna i .env-filen och spara filen:

   * **AEM_URL**: Ange molntjänstens publiceringsmiljö. Till exempel, `https://publish-p105303-e986623.adobeaemcloud.com/`

   * **AEM_ADAPTIVE_FORM**: Ange formulärets sökväg. Om formulärsökvägen till exempel är `/content/forms/af/registration`, skulle värdet för den här variabeln vara `registration`.

   ![](/help/forms/assets/screenshot2028116429.png)


1. Kör följande kommando i kommandotolken:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * Om du får ett meddelande där du ombeds att uppdatera npm via `npm notice Run npm nstall -g npm@9.6.0`ignorera meddelandet.
   > * Kör inte andra npm-kommandon om inte annat anges i arbetsboken.


1. Kör nu följande kommando för att förhandsgranska formuläret.

   ```Shell
   npm run live
   ```

   ![](/help/forms/assets/screenshot2028117229.png)

   När ovanstående kommando har körts väntar du på `webpack compiled` meddelande. Formuläret visas på en webbläsarflik.

   >[!NOTE]
   >
   >Om du får en tom skärm i webbläsaren när du har kört `npm run live` i mer än 3-4 minuter, ändra `localhost` i webbläsarens URL till 127.0.0.1 och tryck **Retur**.


   ![](/help/forms/assets/screenshot2028115129.png)


1. I Visual Studio Code öppnar du `PROJECT\src\site\_variables.scss` -fil. Lägg märke till `$error` färg är en skugga av RED.

   ![](/help/forms/assets/screenshot2028120729.png)

1. Skicka formuläret i webbläsaren för att se den röda färgen i **Förnamn** fält.

   ![](/help/forms/assets/screenshot2028120829.png)

1. Ange **$error** färg till **#5736Web** och spara filen.

   ![](/help/forms/assets/screenshot2028120729.png)

1. Uppdatera webbläsaren och skicka formuläret. Observera att felfärgen i förnamnsfältet har ändrats i enlighet med detta.

   ![](/help/forms/assets/screenshot2028121129.png)

1. I kommandotolken trycker du på **CTRL+C**, ange **Y** och tryck **Retur** för att avsluta npm-processen. Det är viktigt att stoppa npm-servern så att den inte hamnar i konflikt med nästa uppsättning övningar.
1. Stäng fönster för Visual Studio-kod och kommandotolk.

## Lektion 4

### Syfte

Rendera formuläret till webb-/mobilgränssnitt och andra gränssnitt som en headless-form.

### Lektionssammanhang

I den här lektionen får du som frontutvecklare lära dig hur du kan återge den adaptiva formen som tidigare skapats som en headless-form med hjälp av ett ramverk för reaktionsspektrumdesign.

### Utövning

Konfigurera lokal databas med hjälp av ett reaktionsstartprojekt:

1. Öppna kommandotolken med administratörsbehörighet.

   ![](/help/forms/assets/screenshot2028115829.png)

1. Använd följande kommando på kommandotolken för att navigera till **c:\git** mapp

   ```Shell
   cd c:\git
   ```

1. Använd följande kommando för att klona startprojektet för adaptiv formulärreaktion:

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028117329.png)

1. Använd följande kommandon i den angivna ordningen för att navigera till **response-starter-kit-aem-headless-forms** och öppna Visual Studio Code.

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028117529.png)


   Fönstret Visual Studio Code öppnas.

   ![](/help/forms/assets/screenshot2028117429.png)

Så här återger du formuläret som finns i molntjänstens publiceringsmiljö:

1. Byt namn på filen env_template till .env. Om du vill byta namn högerklickar du på **env_template** och väljer **Byt namn** alternativ.

   ![](/help/forms/assets/screenshot2028117629.png)

   ![](/help/forms/assets/screenshot2028117729.png)

1. Ange följande värden för variablerna i .env-filen. Spara filen när du har uppdaterat variablerna.

   * **AEM_URL**: Ange URL:en för molntjänstens publiceringsmiljö. Till exempel, `https://publish-p105303-e986623.adobeaemcloud.com`

   * **AEM_FORM_PATH**: Ange sökvägen till det anpassade formulär som skapades i föregående lektion. Till exempel, `/content/forms/af/registration/`

      ![](/help/forms/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. Öppna kommandofönstret, kontrollera att du befinner dig i katalogen response-starter-kit-aem-headless-forms och kör följande kommando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028118029.png)


1. Kör följande kommando i kommandotolken:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028118129.png)

   Ovanstående kommando startar en lokal utvecklingsserver som skulle återge formulärdefinitionen som hämtats från AEM på ett headless sätt med hjälp av frontend-biblioteket för reaktionsspektrum.

   >[!NOTE]
   >
   > 
   > Om du får en tom skärm i webbläsaren när du har kört `npm start` i mer än 3-4 minuter, ändra `localhost` i webbläsarens URL till 127.0.0.1 och tryck **Retur**.

   ![](/help/forms/assets/screenshot2028118229.png)

Låt oss kontrollera hur reglerna verkställs i den här rubrikfria formen:

1. Välj **Markera kryssrutan för att få 5 % rabatt** alternativ. Det efterföljande alternativet för att använda kreditkort är inaktiverat.

   ![](/help/forms/assets/screenshot2028126229.png)

1. Avmarkera **Markera kryssrutan för att få 5 % rabatt** för att aktivera kreditkortsalternativet.

   ![](/help/forms/assets/screenshot2028126329.png)

Låt oss göra ändringar i formuläret på servern som företagsanvändare och automatiskt se ändringarna som återspeglas i det headless-formuläret.

1. Öppna AEM Forms gränssnitt i webbläsaren. Till exempel: [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/forms.html/content/dam/formsanddocuments](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments).

1. Välj **registrering** formulär och klicka **Redigera.** Formuläret öppnas i redigeraren för anpassade formulär.

   ![](/help/forms/assets/screenshot2028118529.png)

1. Välj **Telefonnummer** och klicka på **Ikonen Redigera (pennikonen)** i verktygsfältet. Om du inte kan se popup-verktygsfältet växlar du till redigeringsläget genom att klicka på **Redigera** överst till höger, vänster till **Förhandsgranska** -knappen.

   ![](/help/forms/assets/screenshot2028119629.png)

1. Ändra etiketten till Mobilnummer. Klicka på ett tomt utrymme i formuläret så sparas ändringarna i formuläret.

   ![](/help/forms/assets/screenshot2028119729.png)

Låt oss publicera det uppdaterade formuläret för att sprida ändringarna till publiceringsmiljön.

1. Markera registreringsformuläret på fliken för AEM Forms-hanteringsgränssnittet och klicka på **Avpublicera**. Om du inte ser **Avpublicera** går du vidare till steg 3 för att publicera ändringarna direkt.

   ![](/help/forms/assets/screenshot2028119829.png)

1. Klicka **Avpublicera**. Klicka **Stäng** i respektive dialogruta.

   ![](/help/forms/assets/screenshot2028119929.png)

   ![](/help/forms/assets/screenshot2028120029.png)


1. När webbläsaren har uppdaterats markerar du registreringsformuläret och klickar på **Publicera**.

   ![](/help/forms/assets/screenshot2028120129.png)


1. Klicka **Publicera**. Klicka **Stäng** i respektive dialogruta.

   ![](/help/forms/assets/screenshot2028120329.png)

   ![](/help/forms/assets/screenshot2028120429.png)

1. Uppdatera webbläsarfliken med det headfria formuläret synligt. Observera att telefonnummeretiketten har ändrats till Mobilnummer.

   ![](/help/forms/assets/screenshot2028120529.png)

1. Öppna kommandotolkfönstret som används för att starta **response-starter-kit-aem-headless-forms** projekt, tryck **CTRL+C** och sedan ange **Y** och tryck på Retur för att avsluta npm-processen. Det är viktigt att stoppa npm-servern så att den inte hamnar i konflikt med nästa uppsättning övningar.

1. Stäng fönster för Visual Studio-kod och kommandotolk.


## Lektion 5

### Syfte

Rendera formuläret som ett headless-formulär med Google Material UI

### Lektionssammanhang

I den här lektionen lär du dig att återge den adaptiva formen som tidigare skapats som ett headless-formulär med Google Material UI.

### Utövning

Konfigurera lokal databas med hjälp av huvudanvändargränssnittets startprojekt:

1. Öppna kommandotolken med administratörsbehörighet.

   ![](/help/forms/assets/screenshot2028115829.png)


1. Använd följande kommando på kommandotolken för att navigera till **c:\git** mapp:

   ```Shell
   cd c:\git
   ```

1. Kör följande kommandon i den angivna ordningen för att skapa en mapp med namnet mui och navigera till multimappen med följande kommandon:

   ```Shell
   mkdir mui
   
   cd mui
   ```

1. Använd följande kommando för att klona startprojektet för adaptiv formulärreaktion:

   ```Shell
   git clone -b mui https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028126529.png)

1. Använd följande kommando i den listade ordningen för att navigera till **response-starter-kit-aem-headless-forms** och öppna koden i Visual Studio Code:

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028126829.png)

Så här återger du formuläret som finns i molntjänstens publiceringsmiljö:

1. Byt namn på **env_template** fil till **.env** -fil. Om du vill byta namn högerklickar du på **env_template** och markera **Byt namn**.

   ![](/help/forms/assets/screenshot2028126629.png)

1. Ange följande värden för variablerna i .env-filen. Spara filen när du har uppdaterat variablerna. Använd **CTRL + S** växla kombination för att spara filen.

   * **AEM_URL**: Ange URL:en för molntjänstens publiceringsmiljö. Till exempel: [https://publish-p105303-e986623.adobeaemcloud.com](https://publish-p105303-e986623.adobeaemcloud.com/)

   * **AEM_FORM_PATH**: Ange sökvägen till det anpassade formulär som skapades i föregående lektion. Till exempel /content/forms/af/registration/

      ![](/help/forms/assets/screenshot2028126929.png)

1. Öppna kommandofönstret och kontrollera att du är vid **response-starter-kit-aem-headless-forms** och kör följande kommando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028127029.png)

1. Kör följande kommando i kommandotolken:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028127129.png)

   Kommandot startar en lokal utvecklingsserver och återger formulärdefinitionen som hämtats från AEM utan rubrik med hjälp av Google materialgränssnittets bibliotek i förgrunden.

   >[!NOTE]
   >
   >Om du får en tom skärm i webbläsaren när du har kört `npm start` i mer än 3-4 minuter, ändra `localhost` i webbläsarens URL till 127.0.0.1 och tryck **Retur**.

   ![](/help/forms/assets/screenshot2028127229.png)

1. Så här utvärderar du körningen av samma affärslogik i den här formuläråtergivningen:

   Välj **Markera kryssrutan för att få 5 % rabatt**. Det följande alternativet **Vill du ansöka om ett kreditkortsformulär för Web.Finance Corporate?** inaktiveras.

   ![](/help/forms/assets/screenshot2028127329.png)

## Lektion 6

### Syfte

Skapa ett alternativt utseende och känsla för den headless-formen med materialvariationer för UI-komponenter

### Lektionssammanhang

I den här lektionen lär du dig som gränssnittsutvecklare hur du skapar en alternativ representation av olika komponenter med hjälp av materialgränssnittet för det adaptiva formulär som tidigare skapats av företagsanvändaren.

### Utövning

Uppdatera variationen av komponenterna i det headless-projektet. Ändra varianten på textindatakomponenten i användargränssnittet till `OutlinedInput`:

1. I Visual Code navigerar du till textindatakomponenten genom att öppna `index.tsx` fil på `src/components/textinput/index.tsx`.

1. Lägg till `//` i början av kodraden 103. Raden konverteras till en kommentar.

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. Lägg till följande på rad 104 om du vill använda en annan variant av komponenten och spara filen. Använd **CTRL + S** växla kombination för att spara filen.

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/forms/assets/screenshot2028127629.png)

   Det är viktigt att använda korrekt skiftläge för &#39;OutlinedInput&#39;-varianten, annars misslyckas kompileringen. Kompileringen av den lokala utvecklingsmiljön startar automatiskt i kommandotolken. Vänta tills följande meddelande visas

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. Uppdatera webbläsaren, om den inte uppdateras automatiskt, för att se hur textinmatningskomponenten använder en annan variant.

   ![](/help/forms/assets/screenshot2028127729.png)


   Den här ändringen sker för slutanvändare utan att formulärdefinitionen på AEM Forms Server ändras och gäller specifikt för den aktuella huvudlösa kanalen. Till exempel webbkanalen i det här labbet.

   ![](/help/forms/assets/screenshot2028127529.png)


1. Stäng Visual Studio-kod och kommandotolken i Windows.

## Vanliga frågor och svar

+++ Är guiden Adaptiv blankett tillgänglig offentligt?

Ja, det finns med AEM Forms som Cloud Service.

+++


+++ Är kärnkomponenterna tillgängliga för allmänheten?

Ja, de adaptiva kärnkomponenterna i Forms finns tillgängliga med AEM Forms som Cloud Service.

+++

+++ Är headless-formulär tillgängliga för allmänheten?

Ja, formulär utan rubrik finns med AEM Forms som Cloud Service.

+++

+++ Kräver Headless-formulär en separat licens?

Nej, Headless-formulär använder samma licensvärde, antal formulärinskickade formulär.

+++

+++ Finns kärnkomponenter och headless-formulär med AEM 6.5 Forms?

Ja, både adaptiva formulär och headless-komponenter finns tillgängliga med AEM Forms 6.5 Service Pack 16 och senare.

+++


## Nästa steg

Nu när ni har lärt er att skapa anpassningsbara formulär och leverera dem till flera kanaler med hjälp av headless-formulär, bör ni försöka att använda era nya kunskaper i praktiken. Ha kul och gör det bara genom att skapa och leverera enastående datainhämtningsupplevelser till slutanvändarna, var de än är, i stor skala!

## Resurser

* [Introduktion av komponenter i adaptiva Form Core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)

* [Skapa anpassningsbara formulär med hjälp av kärnkomponenter](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html)

* [Uppdatera format för grundkomponentbaserad AF](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=en)

* [Headless adaptive forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=en)

* [Använda startkit för Headless React](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=en)


