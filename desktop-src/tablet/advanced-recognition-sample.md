---
Description: The advanced recognition sample demonstrates advanced features of the Microsoft Tablet PC Automation application programming interface (API) used for handwriting recognition.
ms.assetid: 4c9b9f31-c317-43fd-8404-35295b41d093
title: Advanced Recognition Sample
ms.date: 05/31/2018
ms.topic: article
ms.author: windowssdkdev
ms.prod: windows
ms.technology: desktop
---

# Advanced Recognition Sample

The advanced recognition sample demonstrates advanced features of the Microsoft Tablet PC Automation application programming interface (API) used for handwriting recognition.

It includes the following features:

-   Enumerating the installed recognizer
-   Creating a recognizer context with a specific language
-   Using the recognizer object
-   Setting recognition factoid and word lists
-   Using guides to improve the recognition quality
-   Dynamic background recognition
-   Gesture recognition

The interfaces used are: [**IInkRecognizer**](/windows/win32/msinkaut/nn-msinkaut-iinkrecognizer?branch=master), **IInkRecoContext**, [**IInkRecognitionResult**](/windows/win32/msinkaut/nn-msinkaut-iinkrecognitionresult?branch=master), **IInkRecognitionGuide**, **IInkWordList**, [**IInkGesture**](/windows/win32/msinkaut/nn-msinkaut-iinkgesture?branch=master), **IInkCollector**, **IInkDisp**, **IInkRenderer**, **IInkDrawingAttributes**, **IInkStrokes**, and **IInkStroke**.

## Ink and Project Headers

First, include the headers for Tablet PC Automation interfaces. These are installed with the Tablet PC Platform SDK. The TpcError.h file contains the Tablet PC API Error Code definitions.


```C++
#include <msinkaut.h>
#include <msinkaut_i.c>
#include <TpcError.h>
```



The EventSinks.h file defines the **IInkEventsImpl** and **IInkRecognitionEventsImpl** interfaces, and sets up the [**RecognitionWithAlternates**](inkrecognizercontext-recognitionwithalternates.md), [**Stroke**](inkcollector-stroke.md), and [**Gesture**](inkcollector-gesture.md) events.


```C++
#include "EventSinks.h"
```



The ChildWnds.h file contains the definitions of the classes **CInkInputWnd** and **CRecoOutputWnd**, which are derived from the ATL's CWindowImpl and used for creating the sample's child windows.


```C++
#include "ChildWnds.h"
```



The AdvReco.h file declares the **CAdvRecoApp** class, which is the application window class for this sample.


```C++
#include "AdvReco.h"
```



## Initializing the Application Window

The window's `Run` method sets up the **CAdvRecoApp** object, loads the menu and icon for the window, creates an [**InkRecognizerContext**](/windows/win32/msinkaut/?branch=master) object for the default recognizer, and starts the window's message loop.

The window's **OnCreate** method handles the **WM\_CREATE** event and creates the child windows. An [**InkCollector**](/windows/win32/msinkaut/?branch=master) object connects to the ink collector's event source, and enables ink input on the input window. Then it creates an [**InkRecognizerGuide**](/windows/win32/msinkaut/?branch=master) object and uses the ink collector's [**Renderer**](/windows/win32/msinkaut/?branch=master) property to convert the recognition guide box rectangles to ink space. Finally, the **OnCreate** method creates an [**InkWordList**](/windows/win32/msinkaut/?branch=master) object.

## Handling Ink Collector Events

The window's **OnStroke** method handles the ink collector's [**Stroke**](inkcollector-stroke.md) event. The new [**IInkStrokeDisp**](/windows/win32/msinkaut/nn-msinkaut-iinkstrokedisp?branch=master) object is added to the [InkStrokes](/windows/win32/msinkaut/?branch=master) of the ink collector's [**Ink**](/windows/win32/msinkaut/nf-msinkaut-iinkcollector-get_ink?branch=master) property.

The window's **OnGesture** method handles the ink collector's [**Gesture**](inkcollector-gesture.md) event. The **OnGesture** method identifies the gesture, using the highest confidence gesture first, and checks if the window supports this particular gesture. If the gesture is supported, the gesture's bounding box is invalidated, as the gesture is removed from the strokes collection. If the gesture is not supported, the **Gesture** event is canceled, which causes the ink collector to raise a [**Stroke**](inkcollector-stroke.md) event. Finally, the results window is updated.

## Handling Recognizer Context Events

The window's **OnRecognitionWithAlternates** method handles the recognizer context's [**RecognitionWithAlternates**](inkrecognizercontext-recognitionwithalternates.md) event. The **OnRecognitionWithAlternates** method displays the recognition results in the results window.

## Handling Menu Commands

The window's **OnRecognizer** method handles the commands on the Recognizer menu. If the **Default** command was selected, the [**GetDefaultRecognizer**](/windows/win32/msinkaut/?branch=master) method of the [InkRecognizers](/windows/win32/msinkaut/?branch=master) is used to retrieve the default recognizer; otherwise, the selected recognizer is retrieved. Then, a recognizer context is created and used, and menu and status bar are updated.

The window's **OnFactoidWordlist** method handles the **Use Wordlist** command on the **Factoid** menu. The recognizer context's [**Strokes**](/windows/win32/msinkaut15/nf-msinkaut15-iinkdivisionresult-get_strokes?branch=master) property is set to **NULL** to reset the recognizer context. If the **Use Wordlist** option is turned off, the recognizer context's [**WordList**](/windows/win32/msinkaut/?branch=master) property is set to **NULL**; otherwise, the recognizer context's **WordList** property is set to the [**InkWordList**](/windows/win32/msinkaut/?branch=master) that was created in the **OnCreate** method. Finally, the [InkStrokes](/windows/win32/msinkaut/?branch=master) of the ink collector is reattached to the recognizer context, the recognizer context's [**BackgroundRecognizeWithAlternates**](inkrecognizercontext-backgroundrecognizewithalternates.md) method is called, and the menu is updated.

The window's **OnFactoid** method handles the factoid commands on the **Factoid** menu. It first sets the recognizer context's [**Strokes**](/windows/win32/msinkaut15/nf-msinkaut15-iinkdivisionresult-get_strokes?branch=master) property to **NULL**, sets the recognizer context's [**Factoid**](/windows/win32/msinkaut/?branch=master) property to the selected factoid, and reassigns the [InkStrokes](/windows/win32/msinkaut/?branch=master) of the ink collector to the recognizer context. If the [Factoid](factoid-constants.md) object is supported by the recognizer context, the recognizer context's [**BackgroundRecognizeWithAlternates**](inkrecognizercontext-backgroundrecognizewithalternates.md) method is called; otherwise, an error message is displayed. Finally, the menu and status bar are updated.

The window's **OnGuide** method handles the commands on the **Guide** menu. If the recognizer context supports the guide options, the **OnGuide** method sets the recognizer context's [**Strokes**](/windows/win32/msinkaut15/nf-msinkaut15-iinkdivisionresult-get_strokes?branch=master) property to **NULL**, sets the recognizer context's [**Guide**](/windows/win32/msinkaut/?branch=master) property to the selected guide setting, reassigns the [InkStrokes](/windows/win32/msinkaut/?branch=master) of the ink collector to the recognizer context, and calls the recognizer context's [**BackgroundRecognizeWithAlternates**](inkrecognizercontext-backgroundrecognizewithalternates.md) method. Otherwise, an error message is displayed. Finally, the input window, menu, and status bar are updated.

The window's **OnMode** method handles the commands on the **Mode** menu. It disables the ink collector, updates the ink collector's [**CollectionMode**](/windows/win32/msinkaut/nf-msinkaut-iinkcollector-put_collectionmode?branch=master) property, updates the menu, and shows or hides the gesture lists. Finally, the ink collector is enabled.

The window's **OnRecognize** method handles the **Recognize** command on the Ink menu. It calls the recognizer context's [**EndInkInput**](/windows/win32/msinkaut/?branch=master) method to keep ink from being added to the recognizer context. This is sometimes necessary, as not all recognizers support partial recognition. Then it calls the recognizer context's [**Recognize**](/windows/win32/msinkaut/?branch=master) method, and passes the results to the window's **OnRecognitionWithAlternates** method. Finally, the [InkStrokes](/windows/win32/msinkaut/?branch=master) of the ink collector is reassigned to the recognizer context.

The window's **OnClear** method handles the **Clear** command on the **Ink** menu. It deletes the strokes from the ink collector's [**Ink**](/windows/win32/msinkaut/nf-msinkaut-iinkcollector-get_ink?branch=master) property, releases the old strokes collection and creates a new one for the ink collector's **Ink** property, and attaches the new strokes collection to the recognizer context.

The window's **OnExit** method handles the **Exit** command on the **Ink** menu, and raises the WM\_CLOSE event.

## Helper Methods

The window's **LoadMenu** method is called from the window's **Run** method, and adds the list of supported recognizers and the list of supported factoids to the menu. First, it retrieves the [InkRecognizers](/windows/win32/msinkaut/?branch=master). Then it iterates through the available recognizers and only selects ones that have a list of languages in the **Languages** property, which it adds to the **Recognizer** menu. Finally, it populates the **Factoid** menu with the list of factoids defined as a global constant.

The window's **UseRecognizer** method is called from the window's **OnRecognizer** method when the user selects a new recognizer. It creates a recognizer context, detaches the old context from the recognizer event sink, clears and releases the old context, and attaches the new context to the recognizer event sink.

Then, the **UseRecognizer** method checks the recognizer's [**Capabilities**](/windows/win32/msinkaut/nf-msinkaut-iinkrecognizer-get_capabilities?branch=master) property, which returns an [**InkRecognizerCapabilities**](/windows/win32/msinkaut/ne-msinkaut-inkrecognizercapabilities?branch=master) value. If the recognizer supports lined input, the **Lines** command on the **Guide** menu is enabled. If the recognizer supports boxed input, the **Boxes** command is enabled. If the recognizer does not support free input, the **None** command is disabled. If the current guide selection is not supported, both the [**Guide**](/windows/win32/msinkaut/?branch=master) property of the recognizer context and the menu are updated.

Then, the **UseRecognizer** method attempts to set the [**WordList**](/windows/win32/msinkaut/?branch=master) and [**Factoid**](/windows/win32/msinkaut/?branch=master) properties of the recognizer context. If either setting is not supported by the recognizer, then the default value is used and the menu is updated.

Finally, the **UseRecognizer** method attaches the [**Strokes**](/windows/win32/msinkaut15/nf-msinkaut15-iinkdivisionresult-get_strokes?branch=master) property of the ink collector's [**InkDisp**](/windows/win32/msinkaut/?branch=master) object to the recognizer context, changes the output window's font to one supported by the language of the recognizer, resets the output window, and updates the recognition results by calling the recognizer context's [**BackgroundRecognizeWithAlternates**](inkrecognizercontext-backgroundrecognizewithalternates.md) method.

The window's **GetGestureName** method is called from the window's **OnGesture** method. It searches for the gesture and returns an index to the gesture's name, which is stored in a string table in the AdvReco.rc file.

 

 


