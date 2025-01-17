---
title: Targeted .NET frameworks
ms.date: 02/06/2018
ms.topic: conceptual
helpviewer_keywords:
  - "targeting .NET Framework [Visual Studio]"
  - "framework targeting [Visual Studio]"
  - ".NET framework targeting [Visual Studio]"
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "dotnet"
---
# Framework targeting overview

In Visual Studio, you can specify the version of .NET that you want your project to target. For .NET Framework apps to run on another computer, the framework version that the application targets must be compatible with the framework version that's installed on the computer.

For more information about target frameworks, see [Target frameworks](/dotnet/standard/frameworks).

You can also create a solution that contains projects that target different versions of .NET. Framework targeting helps guarantee that the application uses only functionality that is available in the specified framework version.

> [!TIP]
> You can also target applications for different platforms. For more information, see [Multitargeting](../msbuild/msbuild-multitargeting-overview.md).

## Framework targeting features

Framework targeting includes the following features:

- When you open a project that targets an earlier framework version, Visual Studio can automatically upgrade the project or leave the target as-is.

- When you create a .NET Framework project, you can specify the version of the .NET Framework that you want to target.

- You can [target multiple frameworks](/dotnet/standard/frameworks#how-to-specify-target-frameworks) in a single project.

- You can target a different version of .NET in each of several projects in the same solution.

- You can change the version of .NET that an existing project targets.

   When you change the version of .NET that a project targets, Visual Studio makes any required changes to references and configuration files.

When you work on a project that targets an earlier framework version, Visual Studio dynamically changes the development environment, as follows:

- It filters items in the **Add New Item** dialog box, the **Add New Reference** dialog box, and the **Add Service Reference** dialog box to omit choices that are not available in the targeted version.

- It filters custom controls in the **Toolbox** to remove those that are not available in the targeted version and to show the only the most up-to-date controls when multiple controls are available.

- It filters **IntelliSense** to omit language features that aren't available in the targeted version.

- It filters properties in the **Properties** window to omit those that aren't available in the targeted version.

- It filters menu options to omit options that aren't available in the targeted version.

- For builds, it uses the version of the compiler and the compiler options that are appropriate for the targeted version.

> [!NOTE]
> - Framework targeting does not guarantee that your application will run correctly. You must test your application to make sure it runs against the targeted version.
> - You cannot target framework versions below .NET Framework 2.0.

## Select a target framework version

When you create a .NET Framework project, you can select the target .NET Framework version after you select a project template. The list of available frameworks includes the installed framework versions that are applicable to the selected template type. For non-.NET Framework project templates, for example .NET Core templates, the **Framework** drop-down list doesn't appear.

::: moniker range="vs-2017"

![Framework drop-down in VS 2017](media/vside-newproject-framework.png)

::: moniker-end

::: moniker range=">=vs-2019"

![Framework dropdown in VS 2019](media/vs-2019/configure-new-project-framework.png)

::: moniker-end

In an existing project, you can change the target .NET version in the project properties dialog box. For more information, see [How to: Target a version of .NET](../ide/how-to-target-a-version-of-the-dotnet-framework.md).

## Resolve system and user assembly references

To target a .NET version, you must first install the appropriate assembly references. You can download developer packs for different versions of .NET on the [.NET downloads](https://www.microsoft.com/net/download/windows) page.

For .NET Framework projects, the **Add Reference** dialog box disables system assemblies that do not pertain to the target .NET Framework version so that they cannot be inadvertently added to a project. (System assemblies are *.dll* files that are included in a .NET Framework version.) References that belong to a framework version that's higher than the targeted version will not resolve, and controls that depend on such a reference cannot be added. If you want to enable such a reference, reset the .NET Framework target of the project to one that includes the reference. For more information, see [How to: Target a framework version](../ide/how-to-target-a-version-of-the-dotnet-framework.md).

For more information about assembly references, see [Resolve assemblies at design time](../msbuild/resolving-assemblies-at-design-time.md).

## Enable LINQ

When you target the .NET Framework 3.5 or later, a reference to **System.Core** and a project-level import for <xref:System.Linq> (in Visual Basic only) are added automatically. If you want to use LINQ features, you must also turn `Option Infer` on (in Visual Basic only). The reference and import are removed automatically if you change the target to an earlier .NET Framework version. For more information, see [Work with LINQ](/dotnet/csharp/tutorials/working-with-linq).

## See also

- [Target frameworks](/dotnet/standard/frameworks)
- [Multitargeting (MSBuild)](../msbuild/msbuild-multitargeting-overview.md)
- [How to: Modify the target framework and platform toolset (C++)](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset)