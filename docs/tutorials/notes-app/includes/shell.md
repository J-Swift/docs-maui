---
author: adegeo
ms.author: adegeo
ms.date: 07/29/2022
ms.topic: include
---

When Visual Studio creates a .NET MAUI project, four important code files are generated. These can be seen in the **Solution Explorer** pane of Visual Studio:

:::image type="content" source="../media/shell/vs-solution-explorer.png" alt-text="Solution Explorer showing the files for a .NET MAUI project in Visual Studio.":::

These files help get the .NET MAUI app configured and running. Each file serves a different purpose, described below:

- _MauiProgram.cs_

  This is a code file that bootstraps your app. The code in this file serves as the cross-platform entry point of the app, which configures and starts the app. The template startup code points to the `App` class defined by the _App.xaml_ file.

- _App.xaml_ and _App.xaml.cs_

  Just to keep things simple, both of these files are referred to as a single file. There are generally two files with any XAML file, the _.xaml_ file itself, and a corresponding code file that is a child item of it in the **Solution Explorer**. The _.xaml_ file contains XAML markup and the code file contains code created by the user to interact with the XAML markup.

  The _App.xaml_ file contains app-wide XAML resources, such as colors, styles, or templates. The _App.xaml.cs_ file generally contains code that instantiates the Shell application. In this project, it points to the `AppShell` class.

- _AppShell.xaml_ and _AppShell.xaml.cs_

  This file defines the `AppShell` class, which is used to define visual hierarchy of the app.

- _MainPage.xaml_ and _MainPage.xaml.cs_

  This is the startup page displayed by the app. The _MainPage.xaml_ file defines the UI (user interface) of the page. _MainPage.xaml.cs_ contains the code-behind for the XAML, like code for a button click event.

## Add an "about" page

The first customization you'll do is adding another page to the project. This page is an "about" page, which represents information about this app, such as the author, version, and perhaps a link for more information.

01. In the **Solution Explorer** pane of Visual Studio, right-click on the **Notes** project > **Add** > **New Item...**.

    :::image type="content" source="../media/shell/vs-new-item.png" alt-text="Right-clicking on a project in Visual Studio and selecting New Item.":::

01. In the **Add New Item** dialog, select **.NET MAUI** in the template list on the left-side of the window. Next, select the **.NET MAUI ContentPage (XAML)** template. Name the file _AboutPage.xaml_, and then select **Add**.

    :::image type="content" source="../media/shell/vs-about-page.png" alt-text="Adding a new ContentPage to the project. The ContentPage is named AboutPage.xaml.":::

01. The _AboutPage.xaml_ file will open a new document tab, displaying all of the XAML markup that represents the UI of the page. Replace the XAML markup with the following markup:

    :::code language="xaml" source="../snippets/shell/csharp/Notes/AboutPage.xaml":::

01. Save the file by pressing <kbd>CTRL+S</kbd> or by selecting the menu **File** > **Save AboutPage.xaml**.

Let's break down the key parts of the XAML controls placed on the page:

- `<ContentPage>` is the root object for the `AboutPage` class.
- `<VerticalStackLayout>` is the only child object of the `ContentPage`. `ContentPage` can only have one child object. The `VerticalStackLayout` type can have multiple children. This layout control arranges its children vertically, one after the other.
- `<HorizontalStackLayout>` operates the same as a `<VerticalStackLayout>`, except its children are arranged horizontally.
- `<Image>` displays an image, in this case it's using the `dotnet_bot.png` image that comes with every .NET MAUI project.
- `<Label>` controls display text.
- `<Button>` controls can be pressed by the user, which raise the `Clicked` event. You can run code in response to the `Clicked` event.
- `Clicked="LearnMore_Clicked"`

  The `Clicked` event of the button is assigned to the `LearnMore_Clicked` event handler, defined in the code-behind file. You'll create this code in the next step.

## Handle the Clicked event

The next step is to add the code for the button's `Clicked` event.

01. With the XAML editor open, right-click in the middle of the `LearnMore_Clicked` text, and select **Go To Definition**.

    :::image type="content" source="../media/shell/vs-goto-definition.png" alt-text="Right-clicking on a button clicked handler, and selecting Go To Definition.":::

01. The code editor opens to the code-behind file, _About.xaml.cs_, and generates an empty event handler for the `Clicked` event.

    ```csharp
    private void LearnMore_Clicked(object sender, EventArgs e)
    {
    
    }
    ```

01. Replace the event handler with the following code, which opens the system browser to a specific URL:

    :::code language="csharp" source="../snippets/shell/csharp/Notes/AboutPage.xaml.cs" id="learn_more":::

    Notice that the `async` keyword was added to the method declaration, which allows the use of the `await` keyword when opening the system browser.

01. Save the file by pressing <kbd>CTRL+S</kbd> or by selecting the menu **File** > **Save AboutPage.xaml.cs**.

Now that the XAML and code-behind of the `AboutPage` is complete, you'll need to get it displayed in the app.

## Add image resources

Some controls can use images, which enhances how users interact with your app. In this section you'll download and add two images for to your app.

Download these two images:

- [Icon: About](https://raw.githubusercontent.com/dotnet/docs-maui/main/docs/tutorials/notes-app/snippets/shell/csharp/Notes/Resources/Images/icon_about.png)\
  This image is used as an icon for the about page you created earlier.

- [Icon: Notes](https://raw.githubusercontent.com/dotnet/docs-maui/main/docs/tutorials/notes-app/snippets/shell/csharp/Notes/Resources/Images/icon_notes.png)\
  This image is used as an icon for the notes page you'll create in the next part of this tutorial.

After you've downloaded the images, you can move them with File Explorer to the _Resources\Images_ folder of the project. Any file in this folder is automatically included in the project as a **MauiImage** resource. You can also use Visual Studio to add the images to your project. If you move the images by hand, skip the following procedure.

### Move the images with Visual Studio

01. In the **Solution Explorer** pane of Visual Studio, expand the **Resources** folder, which reveals the **Images** folder.

    > [!TIP]
    > You can use File Explorer to drag-and-drop the images directly into the **Solution Explorer** pane, on top of the **Images** folder. This automatically moves the files to the folder, and includes them in the project. If you choose to drag-and-drop the files, ignore the rest of this procedure.

01. Right-click on **Images** and select **Add** > **Existing Item...**.
01. Navigate to the folder that contains the downloaded images.
01. Change the filter to file type filter to **Image Files**.
01. Hold down <kbd>CTRL</kbd> and click on each of the three images you downloaded, then press **Add**

:::image type="content" source="../media/shell/vs-add-image.png" alt-text="Add three icon images to .NET MAUI project.":::

## Modify the app Shell

As noted at the start of this article, the `AppShell` class defines an app's visual hierarchy, the XAML markup used in creating the UI of the app. Update the XAML to add a `TabBar` control:

01. Double-click the _AppShell.xaml_ file in the **Solution Explorer** pane to open the XAML editor. Replace the XAML markup with the following code:

    :::code language="xaml" source="../snippets/shell/csharp/Notes/AppShell.xaml":::

01. Save the file by pressing <kbd>CTRL+S</kbd> or by selecting the menu **File** > **Save AppShell.xaml**.

Let's break down the key parts of the XAML:

- `<Shell>` is the root object of the XAML markup.
- `<TabBar>` is the content of the `Shell`.
- Two `<ShellContent>` objects inside of the `<TabBar>`. Before you replaced the template code, there was a single `<ShellContent>` object, pointing to the `MainPage` page.

The `TabBar` and its children don't represent any user interface elements, but rather the organization of the app's visual hierarchy. Shell will take these objects and produce the user interface for the content.

Each `<ShellContent>` object is pointing to a page to display. This is set by the `ContentTemplate` property.

## Run the app

Run the app by pressing <kbd>F5</kbd> or pressing the play button at the top of Visual Studio:

:::image type="content" source="../media/shell/vs-debug-button.png" alt-text="Visual Studio's Debug Target button with the text Windows Machine.":::

You'll see that there are two tabs: **Notes** and **About**. Press the **About** tab and the app navigates to the `AboutPage` you created. Press on the **Learn More...** button to open the web browser.

:::image type="content" source="../media/shell/final.png" alt-text="About page of .NET MAUI app tutorial.":::

Close the app and return to Visual Studio. If you're using the Android emulator, terminate the app in the virtual device or press the stop button at the top of Visual Studio:

:::image type="content" source="../media/shell/vs-stop-button.png" alt-text="Visual Studio's stop debugging button.":::
