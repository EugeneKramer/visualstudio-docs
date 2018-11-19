---
title: "SccDirDiff Function | Microsoft Docs"
ms.custom: ""
ms.date: 11/15/2016
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-sdk"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SccDirDiff"
helpviewer_keywords: 
  - "SccDirDiff function"
ms.assetid: 26c9ba92-e3b9-4dd2-bd5e-76b17745e308
caps.latest.revision: 16
ms.author: gregvanl
manager: "ghogen"
---
# SccDirDiff Function
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

This function displays the differences between the current local directory on the client disk and the corresponding project under source control.  
  
## Syntax  
  
```cpp#  
SCCRTN SccDirDiff(  
   LPVOID    pContext,  
   HWND      hWnd,  
   LPCSTR    lpDirName,  
   LONG      dwFlags,  
   LPCMDOPTS pvOptions  
);  
```  
  
#### Parameters  
 pContext  
 [in] The source control plug-in context structure.  
  
 hWnd  
 [in] A handle to the IDE window that the source control plug-in can use as a parent for any dialog boxes that it provides.  
  
 lpDirName  
 [in] Fully qualified path to the local directory for which to show a visual difference.  
  
 dwFlags  
 [in] Command flags (see Remarks section).  
  
 pvOptions  
 [in] Source control plug-in-specific options.  
  
## Return Value  
 The source control plug-in implementation of this function is expected to return one of the following values:  
  
|Value|Description|  
|-----------|-----------------|  
|SCC_OK|The directory on disk is the same as the project in source code control.|  
|SCC_I_FILESDIFFER|The directory on disk is different from the project in source code control.|  
|SCC_I_RELOADFILE|A file or project needs to be reloaded.|  
|SCC_E_FILENOTCONTROLLED|The directory is not under source code control.|  
|SCC_E_NOTAUTHORIZED|The user is not allowed to perform this operation.|  
|SCC_E_ACCESSFAILURE|There was a problem accessing the source control system, probably due to network or contention issues. A retry is recommended.|  
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|Nonspecific failure.|  
|SCC_E_FILENOTEXIST|Local directory could not be found.|  
  
## Remarks  
 This function is used to instruct the source control plug-in to display to the user a list of changes to a specified directory. The plug-in opens its own window, in a format of its choice, to display the differences between the user's directory on disk and the corresponding project under version control.  
  
 If a plug-in supports comparison of directories at all, it must support comparison of directories on a file-name basis even if the "quick-diff" options are not supported.  
  
|`dwFlags`|Interpretation|  
|---------------|--------------------|  
|SCC_DIFF_IGNORECASE|Case-insensitive comparison (may be used for either quick diff or visual).|  
|SCC_DIFF_IGNORESPACE|Ignores white space (may be used for either quick-diff or visual).|  
|SCC_DIFF_QD_CONTENTS|If supported by the source control plug-in, silently compares the directory, byte by byte.|  
|SCC_DIFF_QD_CHECKSUM|If supported by plug-in, silently compares the directory via a checksum, or, if not supported, falls back to SCC_DIFF_QD_CONTENTS.|  
|SCC_DIFF_QD_TIME|If supported by plug-in, silently compares the directory via its timestamp, or, if not supported, falls back on SCC_DIFF_QD_CHECKSUM or SCC_DIFF_QD_CONTENTS.|  
  
> [!NOTE]
>  This function uses the same command flags as the [SccDiff](../extensibility/sccdiff-function.md). However, a source control plug-in may choose to not support the "quick-diff" operation for directories.  
  
## See Also  
 [Source Control Plug-in API Functions](../extensibility/source-control-plug-in-api-functions.md)
