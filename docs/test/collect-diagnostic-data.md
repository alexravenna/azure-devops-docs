---
title: Collect diagnostic data
description: Learn about collecting diagnostic data while testing web and desktop apps with Azure Test Plans in manual and exploratory testing.
ms.assetid: F536C364-BEFC-48A8-B977-19233941EF6A
ms.service: azure-devops-test-plans
ms.custom: UpdateFrequency3
ms.topic: conceptual
ms.author: jeom
author: rohit-batra
monikerRange: '<= azure-devops'
ms.date: 12/06/2021
ms.update-cycle: 1095-days
---

# Collect diagnostic data while testing

[!INCLUDE [version-lt-eq-azure-devops](../includes/version-lt-eq-azure-devops.md)] 

Collect diagnostic data while you test your apps. This data is included in the bugs you file 
during the test. You can collect diagnostic data from web apps and from desktop apps, and view it in Azure Test Plans.

## Prerequisites

[!INCLUDE [prerequisites-stakeholder](includes/prerequisites-stakeholder.md)] 

<a name="collect-web"></a>

## Collect diagnostic data from web and desktop apps

For web apps under test, you can use web-based Microsoft Test Runner. 
For desktop apps, download and install the [Test Runner desktop client](https://aka.ms/ATPTestRunnerDownload) to collect the following data on demand:

- [Screen captures](#web-screenshot)
- [Image action log](#web-log)
- [Screen recordings](#web-recording)

For more information, see [Exploratory test and submit feedback directly from your browser](perform-exploratory-tests.md).

<a name="web-screenshot"></a>
<a name="collect-desktop"></a>

## Capture your screen

Do the following steps to capture annotated screenshots from your app. 

1. Open Test Runner and choose the **Capture screenshot** icon. 
   Ensure that the app from which you want to capture data is selected.

   ![Screenshot showing capturing a screenshot from the app.](media/shared/collect-diagnostic-data-01.png) 

1. Drag to select the area of the screen you want to capture, or just capture the full screen.

   ![Screenshot showing selecting the area of the screen to capture.](media/collect-diagnostic-data/collect-diagnostic-data-03.png) 

1. If necessary, edit the title of the screenshot and add annotations and text to it using the icons in the toolbar.

   ![Screenshot showing annotating the screenshot.](media/collect-diagnostic-data/collect-diagnostic-data-04.png) 
 
1. Save your screenshot.  

   ![Screenshot showing saving the screenshot.](media/collect-diagnostic-data/collect-diagnostic-data-05.png) 

<a name="web-log"></a>

## Capture interactions as an image action log

Do the following steps to capture your interactions with the web or desktop app as an image action log that provides context.

1. Open or switch to the Test Runner and choose the **Capture user actions...** icon. 
   Ensure that the app from which you want to capture data is selected.

   ![Screenshot showing capturing an image action log from the app.](media/shared/collect-diagnostic-data-06.png) 

2. The Test Runner records all the actions you take
   on the app's browser tab or in the desktop app.
 
   ![Screenshot showing recording in progress for a web app.](media/collect-diagnostic-data/collect-diagnostic-data-08.png) 

   If you create a bug while recording your actions, all the 
   data collected up to that point is included in the bug. 

3. Select **Stop** to finish capturing your actions, The action log is added to the test results 
   as an attachment.

   ![Screenshot showing stopping a recording for a web app.](media/collect-diagnostic-data/collect-diagnostic-data-08a.png) 

4. Select the **ActionLog...** link to view the data captured in the action log.

   ![Screenshot showing opening the image action log.](media/collect-diagnostic-data/collect-diagnostic-data-09.png) 

   The log opens in your web browser.

   ![Screenshot showing viewing the data captured in the image action log.](media/collect-diagnostic-data/collect-diagnostic-data-10.png) 

<a name="web-recording"></a>

## Record your screen

Do the following steps to capture screen recordings from your apps.

1. Open or switch to the Test Runner and choose the **Record screen** icon. 

   ![Screenshot showing capturing a screen recording from the app.](media/shared/collect-diagnostic-data-11.png) 

1. Choose the entire screen, or choose an app to start recording.

   ::: moniker range=">=azure-devops-2020"
   ![Screenshot showing selection of the screen or app to share.](media/collect-diagnostic-data/choose-test-feedback-share.png)
   ::: moniker-end
   

   If you create a bug while recording your screen, the 
   recording automatically stops and is added to the bug. 

1. Finish recording your actions by choosing
   the **Stop** button. The recording is added to the test results 
   as an attachment.

   ![Screenshot showing stopping a screen recording.](media/collect-diagnostic-data/collect-diagnostic-data-13.png) 

   If you don't stop the recording after 10 minutes, it stops
   automatically and is saved as an attachment to your test results.
   Restart the recording the **Record screen** icon if necessary. 

1. Choose the **ScreenRecording...** link at the bottom of the window
   to view the captured recording.

   ![Screenshot showing viewing the screen recording.](media/collect-diagnostic-data/collect-diagnostic-data-14.png) 

<a name="view-data"></a>

## View the diagnostic data

When you create a bug while capturing diagnostic data, all the data captured 
up to that point gets included in the bug that you create. You can view it before you save the bug.

![Screenshot showing viewing the diagnostic data in the bug you are creating.](media/collect-diagnostic-data/collect-diagnostic-data-15.png) 

[How do I play the video recordings I created with the extension?](reference-qa.yml#recording-playback)

To collect advanced diagnostic data such as code coverage, IntelliTrace, and Test Impact data (in addition to the previously listed data items), you must [configure the data collectors](/previous-versions/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests) and other run settings in Microsoft Test Manager and run your tests using Microsoft Test Manager. For more information, see 
[Run manual tests with Microsoft Test Manager](/previous-versions/azure/devops/test/mtm/plan-manual-tests-with-microsoft-test-manager).

> [!NOTE]
> If you have an older version of Microsoft Test Manager, we recommend you upgrade to the latest version.
> However, if you have Microsoft Test Manager 2015 or an earlier version installed, you can choose **Microsoft Test Runner 2015 and earlier** when you launch the test runner using **Run with options**.
> You must [configure the data collectors](/previous-versions/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests) and other run settings in Microsoft Test Manager and specify these as the default settings for the test plan.
> For more information, see [Run manual tests with Microsoft Test Manager](/previous-versions/azure/devops/test/mtm/plan-manual-tests-with-microsoft-test-manager).

## Related content

- [Exploratory test and submit feedback directly from your browser](perform-exploratory-tests.md)
- [Overview of manual and exploratory testing](index.yml)
- [Testing different configurations](test-different-configurations.md)
- [Manage test results](how-long-to-keep-test-results.md)
- [FAQs for manual testing](reference-qa.yml#repeatdifferent)
