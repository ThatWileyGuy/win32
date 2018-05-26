---
title: CB\_GETTOPINDEX message
description: An application sends the CB\_GETTOPINDEX message to retrieve the zero-based index of the first visible item in the list box portion of a combo box.
ms.assetid: 1e304acf-30ff-40a4-b214-6ed98ddaed3a
keywords:
- CB_GETTOPINDEX message Windows Controls
topic_type:
- apiref
api_name:
- CB_GETTOPINDEX
api_location:
- Winuser.h
api_type:
- HeaderDef
ms.date: 05/31/2018
ms.topic: article
ms.author: windowssdkdev
ms.prod: windows
ms.technology: desktop
---

# CB\_GETTOPINDEX message

An application sends the **CB\_GETTOPINDEX** message to retrieve the zero-based index of the first visible item in the list box portion of a combo box. Initially, the item with index 0 is at the top of the list box, but if the list box contents have been scrolled, another item may be at the top.

## Parameters

<dl> <dt>

*wParam* 
</dt> <dd>

Not used; must be zero.

</dd> <dt>

*lParam* 
</dt> <dd>

Not used; must be zero.

</dd> </dl>

## Return value

If the message is successful, the return value is the index of the first visible item in the list box of the combo box.

If the message fails, the return value is CB\_ERR.

## Requirements



|                                     |                                                                                                          |
|-------------------------------------|----------------------------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows Vista \[desktop apps only\]<br/>                                                           |
| Minimum supported server<br/> | Windows Server 2003 \[desktop apps only\]<br/>                                                     |
| Header<br/>                   | <dl> <dt>Winuser.h (include Windows.h)</dt> </dl> |



## See also

<dl> <dt>

[**CB\_SETTOPINDEX**](cb-settopindex.md)
</dt> </dl>

 

 




