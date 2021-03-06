---
title: "Walkthrough: Creating Your First VSTO Add-In for Outlook | Microsoft Docs"
ms.custom: ""
ms.date: "02/02/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "office-development"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "application-level add-ins [Office development in Visual Studio], creating your first project"
  - "Office development in Visual Studio, creating your first project"
  - "add-ins [Office development in Visual Studio], creating your first project"
  - "Outlook [Office development in Visual Studio], creating your first project"
ms.assetid: 2c5c5d75-27ee-471f-9328-58f0cf05b2b7
caps.latest.revision: 28
author: "gewarren"
ms.author: "gewarren"
manager: ghogen
ms.workload: 
  - "office"
---
# Walkthrough: Creating Your First VSTO Add-In for Outlook
  This walkthrough shows you how to create a VSTO Add-in for Microsoft Office Outlook. The features that you create in this kind of solution are available to the application itself, regardless of which Outlook item is open. For more information, see [Office Solutions Development Overview &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md).  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
 This walkthrough illustrates the following tasks:  
  
-   Creating an Outlook VSTO Add-in project for Outlook.  
  
-   Writing code that uses the object model of Outlook to add text to the subject and body of a new mail message.  
  
-   Building and running the project to test it.  
  
-   Cleaning up the completed project so that the VSTO Add-in no longer runs automatically on your development computer.  
  
 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## Prerequisites  
 You need the following components to complete this walkthrough:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   Microsoft Outlook  
  
## Creating the Project  
  
#### To create a new Outlook project in Visual Studio  
  
1.  Start [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
2.  On the **File** menu, point to **New**, and then click **Project**.  
  
3.  In the templates pane, expand **Visual C#** or **Visual Basic**, and then expand **Office/SharePoint**.  
  
4.  Under the expanded **Office/SharePoint** node, select the **Office Add-ins** node.  
  
5.  In the list of project templates, choose an Outlook VSTO Add-in project.  
  
6.  In the **Name** box, type **FirstOutlookAddIn**.  
  
7.  Click **OK**.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] creates the **FirstOutlookAddIn** project and opens the **ThisAddIn** code file in the editor.  
  
## Writing Code that Adds Text to Each New Mail Message  
 Next, add code to the ThisAddIn code file. The new code uses the object model of Outlook to add text to each new mail message. By default, the ThisAddIn code file contains the following generated code:  
  
-   A partial definition of the `ThisAddIn` class. This class provides an entry point for your code and provides access to the object model of Outlook. For more information, see [Programming VSTO Add-Ins](../vsto/programming-vsto-add-ins.md). The remainder of the `ThisAddIn` class is defined in a hidden code file that you should not modify.  
  
-   The `ThisAddIn_Startup` and `ThisAddIn_Shutdown` event handlers. These event handlers are called when Outlook loads and unloads your VSTO Add-in. Use these event handlers to initialize your VSTO Add-in when it is loaded, and to clean up resources used by your VSTO Add-in when it is unloaded. For more information, see [Events in Office Projects](../vsto/events-in-office-projects.md).  
  
#### To add text to the subject and body of each new mail message  
  
1.  In the ThisAddIn code file, declare a field named `inspectors` in the `ThisAddIn` class. The `inspectors` field maintains a reference to the collection of Inspector windows in the current Outlook instance. This reference prevents the garbage collector from freeing the memory that contains the event handler for the <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> event.  
  
     [!code-vb[Trin_OutlookAddInTutorial#1](../vsto/codesnippet/VisualBasic/Trin_OutlookAddInTutorial/ThisAddIn.vb#1)]
     [!code-csharp[Trin_OutlookAddInTutorial#1](../vsto/codesnippet/CSharp/Trin_OutlookAddInTutorial/ThisAddIn.cs#1)]  
  
2.  Replace the `ThisAddIn_Startup` method with the following code. This code attaches an event handler to the <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> event.  
  
     [!code-vb[Trin_OutlookAddInTutorial#2](../vsto/codesnippet/VisualBasic/Trin_OutlookAddInTutorial/ThisAddIn.vb#2)]
     [!code-csharp[Trin_OutlookAddInTutorial#2](../vsto/codesnippet/CSharp/Trin_OutlookAddInTutorial/ThisAddIn.cs#2)]  
  
3.  In the ThisAddIn code file, add the following code to the `ThisAddIn` class. This code defines an event handler for the <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> event.  
  
     When the user creates a new mail message, this event handler adds text to the subject line and body of the message.  
  
     [!code-vb[Trin_OutlookAddInTutorial#3](../vsto/codesnippet/VisualBasic/Trin_OutlookAddInTutorial/ThisAddIn.vb#3)]
     [!code-csharp[Trin_OutlookAddInTutorial#3](../vsto/codesnippet/CSharp/Trin_OutlookAddInTutorial/ThisAddIn.cs#3)]  
  
 To modify each new mail message, the previous code examples use the following objects:  
  
-   The `Application` field of the `ThisAddIn` class. The `Application` field returns an <xref:Microsoft.Office.Interop.Outlook.Application> object, which represents the current instance of Outlook.  
  
-   The `Inspector` parameter of the event handler for the <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> event. The `Inspector` parameter is an <xref:Microsoft.Office.Interop.Outlook.Inspector> object, which represents the Inspector window of the new mail message. For more information, see [Outlook Solutions](../vsto/outlook-solutions.md).  
  
## Testing the Project  
 When you build and run the project, verify that the text appears in the subject line and body of a new mail message.  
  
#### To test the project  
  
1.  Press **F5** to build and run your project.  
  
     When you build the project, the code is compiled into an assembly that is included in the build output folder for the project. Visual Studio also creates a set of registry entries that enable Outlook to discover and load the VSTO Add-in, and it configures the security settings on the development computer to enable the VSTO Add-in to run. For more information, see [Office Solution Build Process Overview](../vsto/walkthrough-creating-your-first-vsto-add-in-for-outlook.md).  
  
2.  In Outlook, create a new mail message.  
  
3.  Verify that the following text is added to both the subject line and body of the message.  
  
     **This text was added by using code.**  
  
4.  Close Outlook.  
  
## Cleaning up the Project  
 When you finish developing a project, remove the VSTO Add-in assembly, registry entries, and security settings from your development computer. Otherwise, the VSTO Add-in will run every time that you open Outlook on the development computer.  
  
#### To clean up your project  
  
1.  In Visual Studio, on the **Build** menu, click **Clean Solution**.  
  
## Next Steps  
 Now that you have created a basic VSTO Add-in for Outlook, you can learn more about how to develop VSTO Add-ins from these topics:  
  
-   General programming tasks that you can perform by using VSTO Add-ins for Outlook. For more information, see [Programming VSTO Add-Ins](../vsto/programming-vsto-add-ins.md).  
  
-   Using the object model of Outlook. For more information, see [Outlook Solutions](../vsto/outlook-solutions.md).  
  
-   Customizing the UI of Outlook, for example, by adding a custom tab to the Ribbon or creating your own custom task pane. For more information, see [Office UI Customization](../vsto/office-ui-customization.md).  
  
-   Building and debugging VSTO Add-ins for Outlook. For more information, see [Building Office Solutions](../vsto/building-office-solutions.md).  
  
-   Deploying VSTO Add-ins for Outlook. For more information, see [Deploying an Office Solution](../vsto/deploying-an-office-solution.md).  
  
## See Also  
 [Programming VSTO Add-Ins](../vsto/programming-vsto-add-ins.md)   
 [Outlook Solutions](../vsto/outlook-solutions.md)   
 [Office UI Customization](../vsto/office-ui-customization.md)   
 [Building Office Solutions](../vsto/building-office-solutions.md)   
 [Deploying an Office Solution](../vsto/deploying-an-office-solution.md)   
 [Office Project Templates Overview](../vsto/office-project-templates-overview.md)  
  
  