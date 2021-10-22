---
title: "Debugger"
---
# Debugger
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
The Rhino JavaScript debugger is a GUI that allows debugging of interpreted JavaScript scripts run in Rhino. Note that this debugger **will not** work with JavaScript scripts run in the mozilla browser since Rhino is not the engine used in such environments.

![](../assets/images/debugger-ui.png)

Current limitations:

- No breakpoint menu

## Using the Rhino JavaScript Debugger

The Mozilla Rhino JavaScript engine includes a source-level debugger for debugging JavaScript scripts. The debugger is itself a Java program which you may run as

```
java org.mozilla.javascript.tools.debugger.Main [options] [filename.js] [script-arguments]
```

where the options are the same as the shell.

The Rhino JavaScript Debugger can debug scripts running in multiple threads and provides facilities to set and clear breakpoints, control execution, view variables, and evaluate arbitrary JavaScript code in the current scope of an executing script.

|  Console Window  |  The debugger redirects the System.out, System.in, and System.err streams to an internal JavaScript console window which provides an editable command line for you to enter JavaScript code and view system output. The console window maintains a history of the commands you have entered. You may move backward and forward through the history list by pressing the Up/Down arrow keys on the keyboard.  |
|  Opening Scripts  |  You may select the **_File->Open_** menu item on the menu bar to load JavaScript scripts contained in files. This action will display a file-selection dialog box prompting you for the location of a script to load. The selected file will be compiled and displayed in a new window.  |
|  Running Scripts  |  You may select the **_File->Run_** menu item on the menu bar to execute JavaScript scripts contained in files. This action will display a file-selection dialog box prompting you for the location of a script to execute. The loaded script will be run in a new thread and control will be given to the debugger on its first instruction.  |

## Controlling Execution

The debugger provides the following facilities for you to control the execution of scripts you are debugging:

|  Step Into  |  To single step entering any function calls, you may do any of the following:<br> - Select the **_Debug->Step Into_**menu item on the menu bar<br>- Press the **_Step Into_** button on the toolbar<br>- Press the F11 key on the keyboard<br><br> Execution will resume. If the current line in the script contains a function call control will return to the debugger upon entry into the function. Otherwise control will return to the debugger at the next line in the current function.  |
|  Step Over  |  To single step to the next line in the current function, you may do any of the following:<br> - Select the **_Debug->Step Over_** menu item on the menu bar<br>- Press the **_Step Over_** button on the toolbar<br>- Press the F7 key on the keyboard<br><br> Execution will resume but control will return to the debugger at the next line in the current function or top-level script.  |
|  Step Out  |  To continue execution until the current function returns you may do any of the following:<br> - Select the **_Debug->Step Out_** menu item on the menu bar<br>- Press the **_Step Out_** button on the toolbar<br>- Press the F8 key on the keyboard<br><br> Execution will resume until the current function returns or a breakpoint is hit.  |
|  Go  |  To resume execution of a script you may do any of the following:<br> - Select the **_Debug->Go_** menu item on the menu bar<br>- Press the **_Go_** button on the toolbar<br>- Press the F5 key on the keyboard<br><br> Execution will resume until a breakpoint is hit or the script completes.  |
|  Break  |  To stop all running scripts and give control to the debugger you may do any of the following:<br> - Select the **_Debug->Break_** menu item on the menu bar<br>- Press the **_Break_** button on the toolbar<br>- Press the Pause/Break key on the keyboard  |
|  Break on Exceptions  |  To give control to the debugger whenever a JavaScript is exception is thrown select the **_Debug->Break on Exceptions_** checkbox from the menu bar. Whenever a JavaScript exception is thrown by a script a message dialog will be displayed and control will be given to the debugger at the location the exception is raised.  |
|  Break on Function Enter  |  Selecting **_Debug->Break on Function Enter_** will give control to the debugger whenever the execution is entered into a function or script.  |
|  Break on Function Exit  |  Selecting **_Debug->Break on Function Return_** will give control to the debugger whenever the execution is about to return from a function or script.  |
|  Moving Up and Down the Stack  |  The lower-left (dockable) pane in the debugger main window contains a combo-box labeled "Context:" which displays the current stack of the executing script. You may move up and down the stack by selecting an entry in the combo-box. When you select a stack frame the variables and watch windows are updated to reflect the names and values of the variables visible at that scope.  |
|  Setting and Clearing Breakpoints  |  The main desktop of the debugger contains file windows which display the contents of each script you are debugging. You may set a breakpoint in a script by doing one of the following:<br> - Place the cursor on the line at which you want to set a breakpoint and right-click with the mouse. This action will display a pop-up menu. Select the **_Set Breakpoint_** menu item.<br>- Simply single-click on the line number of the line at which you want to set a breakpoint.<br><br> If the selected line contains executable code a red dot will appear next to the line number and a breakpoint will be set at that location.<br><br> You may clear breakpoint in a script by doing one of the following:<br><br> - Place the cursor on the line at which you want to clear a breakpoint and right-click with the mouse. This action will display a pop-up menu. Select the **_Clear Breakpoint_** menu item.<br>- Simply single-click on the red dot or the line number of the line at which you want to clear a breakpoint.<br><br> The red dot will disappear and the breakpoint at that location will be cleared.  |

## Viewing Variables

The lower-left (dockable) pane in the debugger main window contains a tab-pane with two tabs, labeled "this" and "Locals". Each pane contains a tree-table which displays the properties of the current object and currently visible local variables, respectively.

|  This  |  The properties of the current object are displayed in the **_this_** table. If a property is itself a JavaScript object the property may be expanded to show its sub-properties. The **_this_** table is updated each time control returns to the debugger or when you change the stack location in the **_Context:_** window.  |
|  Locals  |  The local variables of the current function are displayed in the **_Locals_** table. If a variable is itself a JavaScript object the variable may be expanded to show its sub-properties. The **_Locals_** table is updated each time control returns to the debugger or when you change the stack location in the **_Context:_** window  |
|  Watch Window  |  You may enter arbitrary JavaScript expressions in the **_Watch:_** table located in the lower-right (dockable) pane in the debugger main window. The expressions you enter are re-evaluated in the current scope and their current values displayed each time control returns to the debugger or when you change the stack location in the **_Context:_** window.  |
|  Evaluation Window  |  The **_Evaluate_** pane located in the lower-right (dockable) pane in the debugger main window contains an editable command line where you may enter arbitrary JavaScript code. The code is evaluated in the context of the current stack frame. The window maintains a history of the commands you have entered. You may move backward or forward through the history by pressing the Up/Down arrow keys on the keyboard.  |