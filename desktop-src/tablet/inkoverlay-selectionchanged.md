---
Description: Occurs when the selection of ink within the control has changed, such as through alterations to the user interface, cut-and-paste procedures, or the Selection property.
ms.assetid: 6b4cd9fe-b09f-4a70-9aa5-92ef9409ff1b
title: InkOverlay.SelectionChanged event
ms.date: 05/31/2018
ms.topic: article
ms.author: windowssdkdev
ms.prod: windows
ms.technology: desktop
---

# InkOverlay.SelectionChanged event

Occurs when the selection of ink within the control has changed, such as through alterations to the user interface, cut-and-paste procedures, or the [**Selection**](/windows/win32/msinkaut/?branch=master) property.

## Syntax


```C++
void SelectionChanged();
```



## Parameters

This event has no parameters.

## Return value

This event does not return a value.

## Remarks

There are no event data.

This event method is defined in the \_IInkOverlayEvents and \_IInkPictureEvents dispatch-only interfaces (dispinterfaces) with an ID of DISPID\_IOESelectionChanged.

## Requirements



|                                     |                                                                                                                     |
|-------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows XP Tablet PC Edition \[desktop apps only\]<br/>                                                       |
| Minimum supported server<br/> | None supported<br/>                                                                                           |
| Header<br/>                   | <dl> <dt>Msinkaut.h (also requires Msinkaut\_i.c)</dt> </dl> |
| Library<br/>                  | <dl> <dt>InkObj.dll</dt> </dl>                               |



## See also

<dl> <dt>

[**InkOverlay Class**](/windows/win32/msinkaut/?branch=master)
</dt> <dt>

[**Selection Property**](/windows/win32/msinkaut/?branch=master)
</dt> </dl>

 

 



