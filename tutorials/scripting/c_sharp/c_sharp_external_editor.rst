.. _doc_csharp_external_editor:

Using an external text editor for C#
====================================

C# support in Godot's built-in script editor is minimal. Consider using an external
IDE or editor, such as `Visual Studio Code <https://code.visualstudio.com/>`__.
These provide autocompletion, debugging, and other useful features for C#.

To select an external editor in Godot, click on **Editor → Editor Settings** and
scroll down to **Dotnet**. Under **Dotnet**, click on **Editor**, and select your
external editor of choice. Godot currently supports the following external editors:

- :ref:`Visual Studio 2022 (Windows-only) <doc_csharp_external_editor_visual_studio>`
- Visual Studio for Mac
- :ref:`Visual Studio Code <doc_csharp_external_editor_vscode>`
- :ref:`JetBrains Rider <doc_csharp_external_editor_jetbrains_rider>`

See the following sections for how to configure an external editor:

.. _doc_csharp_external_editor_visual_studio:

Visual Studio 2022 (Windows only)
---------------------------------

Download and install the latest version of
`Visual Studio <https://visualstudio.microsoft.com/downloads/>`__.
Visual Studio will include the required SDKs if you have the correct
workloads selected, so you don't need to manually install the things
listed in the :ref:`Prerequisites <doc_c_sharp_setup>` section.

While installing Visual Studio, select this workload:

- .NET desktop development

In Godot's **Editor → Editor Settings** menu:

- Set **Dotnet** -> **Editor** -> **External Editor** to **Visual Studio**.

.. note::

    If you see an error like "Unable to find package Godot.NET.Sdk",
    your NuGet configuration may be incorrect and need to be fixed.

    A simple way to fix the NuGet configuration file is to regenerate it.
    In a file explorer window, go to ``%AppData%\NuGet``. Rename or delete
    the ``NuGet.Config`` file. When you build your Godot project again,
    the file will be automatically created with default values.

.. _doc_csharp_external_editor_vscode:

Visual Studio Code
------------------

After reading the :ref:`Prerequisites <doc_c_sharp_setup>` section, you can
download and install `Visual Studio Code <https://code.visualstudio.com/download>`__
(also known as VS Code).

In Godot's **Editor → Editor Settings** menu:

- Set **Dotnet** -> **Editor** -> **External Editor** to **Visual Studio Code**.

In Visual Studio Code:

- Install the `C# <https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp>`__ extension.

To configure a project for debugging, you need a ``tasks.json`` and ``launch.json`` file in
the ``.vscode`` folder with the necessary configuration.

Example ``launch.json`` configuration:

.. code-block:: json
    :emphasize-lines: 9

    {
        "version": "0.2.0",
        "configurations": [
            {
                "name": "Play",
                "type": "coreclr",
                "request": "launch",
                "preLaunchTask": "build",
                "program": "PATH_TO_GODOT_EXECUTABLE",
                "args": [],
                "cwd": "${workspaceFolder}",
                "console": "internalConsole",
                "stopAtEntry": false
            }
        ]
    }

Example ``tasks.json`` configuration:

.. code-block:: json

    {
        "version": "2.0.0",
        "tasks": [
            {
                "label": "build",
                "command": "dotnet",
                "type": "process",
                "args": [
                    "build"
                ],
                "problemMatcher": "$msCompile"
            }
        ]
    }

In the ``launch.json`` file, make sure the ``program`` property points to your Godot executable.
Now, when you start the debugger in Visual Studio Code, your Godot project will run.

.. _doc_csharp_external_editor_jetbrains_rider:

JetBrains Rider
---------------

After reading the :ref:`Prerequisites <doc_c_sharp_setup>` section, you can
download and install `JetBrains Rider <https://www.jetbrains.com/rider/download>`__.

In Godot's **Editor → Editor Settings** menu:

- Set **Dotnet** -> **Editor** -> **External Editor** to **JetBrains Rider and Fleet**.

In Rider:

- Set **MSBuild version** to **.NET Core**.
- Install the `**Godot support** <https://plugins.jetbrains.com/plugin/13882-godot-support>`__ plugin.
