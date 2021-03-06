---
title: Get started with Razor Components
author: guardrex
description: Learn how to get started with the Razor Components framework.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/03/2019
uid: razor-components/get-started
---
# Get started with Razor Components

By [Daniel Roth](https://github.com/danroth27) and [Luke Latham](https://github.com/guardrex)

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

# [Visual Studio](#tab/visual-studio)

Prerequisites:

[!INCLUDE[](~/includes/net-core-prereqs-vs-3.0.md)]

To create your first Razor Components project in Visual Studio:

1. Select **File** > **New Project** > **Web** > **ASP.NET Core Web Application**.
1. Make sure **.NET Core** and **ASP.NET Core 3.0** are selected at the top.
1. Choose the **Razor Components** template and select **OK**.

   ![New app dialog](https://msdnshared.blob.core.windows.net/media/2019/01/razor-components-template.png)

1. Press **F5** to run the app.

Congratulations! You just ran your first Razor Components app!

<!--

# [Visual Studio Code](#tab/visual-studio-code)

Prerequisites:

[!INCLUDE[](~/includes/net-core-prereqs-vsc-3.0.md)]

To create your first Razor Components project in Visual Studio Code:

1. Execute the following command from a command shell:

   ```console
   dotnet new razorcomponents -o WebApplication1
   ```

1. Open the *WebApplication1* folder in Visual Studio Code.

1. Add a *.vscode* folder.

1. Add a *tasks.json* file to the *.vscode* folder with the following content:

   [!code-json[](get-started/samples_snapshot/3.x/tasks.json)]

1. Add a *launch.json* file to the *.vscode* folder with the following content:

   [!code-json[](get-started/samples_snapshot/3.x/launch.json)]

1. Execute the app using the Visual Studio Code debugger.

1. In a browser, navigate to `https://localhost:5001`.

Congrats! You just ran your first Razor Components app!

# [Visual Studio for Mac](#tab/visual-studio-mac)

.NET Core 3.0 will be supported with Visual Studio for Mac version 8.0 or later. Visual Studio for Mac version 8.0 Preview isn't available at this time.

Use the [.NET Core CLI version of this topic](xref:razor-components/get-started?tabs=netcore-cli) on macOS.


[!INCLUDE[](~/includes/net-core-prereqs-mac-3.0.md)]

To create your first project Razor Components project in Visual Studio for Mac:

1. Select **File** > **New Solution** or **New Project**.
1. In the sidebar, select **.NET Core** > **App**.
1. Select **ASP.NET Core Razor Components** and select **Next**.
1. The **Target Framework** defaults to **.NET Core 3.0**. Select **Next**.
1. In the **Project Name** field, enter `WebApplication1`. Select **Create**.
1. Select **Run** > **Run Without Debugging** to run the app *without the debugger*. Running with the debugger isn't supported at this time.

Congratulations! You just ran your first Razor Components app!
-->

# [.NET Core CLI](#tab/netcore-cli/)

Prerequisites:

* [.NET Core SDK 3.0 Preview](https://dotnet.microsoft.com/download/dotnet-core/3.0)

To create your first Razor Components project from a command shell:

```console
dotnet new razorcomponents -o WebApplication1
cd WebApplication1
dotnet run
```

Congratulations! You just ran your first Razor Components app!

---

## Razor Components project

The solution created by the Razor Components template contains two projects:

* *WebApplication1.Server* &ndash; The server project is an ASP.NET Core project set up to host the Razor Components app.
* *WebApplication1.App* &ndash; The client-side web UI project that uses Razor Components.

The UI logic in the *WebApplication1.App* project is separated from the rest of the app due to a technical limitation in ASP.NET Core 3.0 Preview 2. The Razor file extension (*.cshtml*) used for Razor Components is also used for Razor Pages and MVC views. Currently, Razor Components and Razor Pages/MVC have different compilation models, so the Razor Components Razor files are kept separate. In a future preview, we plan to introduce a new file extension for Razor Components (*.razor*). Components, pages, and views will be hosted *in the same project*.

When the app is run, multiple pages are available from tabs in the sidebar:

* Home
* Counter
* Fetch data

On the Counter page, select the **Click me** button to increment the counter without a page refresh. Incrementing a counter in a webpage normally requires writing JavaScript, but Razor Components provides a better approach using C#.

*WebApplication1.App/Pages/Counter.cshtml*:

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter1.cshtml)]

A request for `/counter` in the browser, as specified by the `@page` directive at the top, causes the Counter component to render its content. Components render into an in-memory representation of the render tree that can then be used to update the UI in a flexible and efficient way.

Each time the **Click me** button is selected:

* The `onclick` event is fired.
* The `IncrementCount` method is called.
* The `currentCount` is incremented.
* The component is rendered again.

The runtime compares the new content to the previous content and only applies the changed content to the Document Object Model (DOM).

Add a component to another component using an HTML-like syntax. Component parameters are specified using attributes or child content. For example, a Counter component can be added to the app's homepage by adding a `<Counter />` element to the Index component.

*WebApplication1.App/Pages/Index.cshtml*:

[!code-cshtml[](get-started/samples_snapshot/3.x/Index1.cshtml?highlight=7)]

Run the app. The homepage has its own counter.

To add a parameter to the Counter component, update the component's `@functions` block:

* Add a property for `IncrementAmount` decorated with the `[Parameter]` attribute.
* Change the `IncrementCount` method to use the `IncrementAmount` when increasing the value of `currentCount`.

*WebApplication1.App/Pages/Counter.cshtml*:

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter2.cshtml?highlight=4,8)]

Specify an `IncrementAmount` parameter in the Home component's `<Counter>` element using an attribute.

*WebApplication1.App/Pages/Index.cshtml*:

[!code-cshtml[](get-started/samples_snapshot/3.x/Index2.cshtml)]

Run the app. The homepage has its own counter that increments by ten each time the **Click me** button is selected.

## Next steps

<xref:tutorials/first-razor-components-app>
