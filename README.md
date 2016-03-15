# Class Toolbar

## Class for AutoHotkey Toolbar custom controls

AHK version: 1.1.23.01

This class provides intuitive methods to work with Toolbar controls created via **Gui, Add, Custom, ClassToolbarWindow32**.

Note: It's recommended to call any method only after Gui, Show. Adding or modifying buttons of a toolbar in a Gui that is not yet visible might fail eventually.

## Toolbar Methods:
* Add([Options, Label1[=Text]:Icon[(Options)], Label2[=Text]:Icon[(Options)]...])
* AutoSize()
* Customize()
* Delete(Button)
* Export()
* Get([HotItem, TextRows, Rows, BtnWidth, BtnHeight, Style, ExStyle])
* GetButton(Button [, ID, Text, State, Style, Icon, Label, Index])
* GetButtonPos(Button [, OutX, OutY, OutW, OutH])
* GetButtonState(Button, StateQuerry)
* GetCount()
* GetHiddenButtons()
* Insert(Position [, Options, Label1[=Text]:Icon[(Options)], Label2[=Text]:Icon[(Options)]...])
* LabelToIndex(Label)
* ModifyButton(Button, State [, Set])
* ModifyButtonInfo(Button, Property, Value)
* MoveButton(Button, Target)
* OnMessage(CommandID)
* OnNotify(Param [, MenuXPos, MenuYPos, Label, ID, AllowCustom])
* Reset()
* SetButtonSize(W, H)
* SetDefault([Options, Label1[=Text]:Icon[(Options)], Label2[=Text]:Icon[(Options)]...])
* SetExStyle(Style)
* SetHotItem(Button)
* SetImageList(IL_Default [, IL_Hot, IL_Pressed, IL_Disabled])
* SetIndent(Value)
* SetListGap(Value)
* SetMaxTextRows([MaxRows])
* SetPadding(X, Y)
* SetRows([Rows, AddMore])
* ToggleStyle(Style)

## Presets Methods:
* Presets.Delete(Slot)
* Presets.Export(Slot, [ArrayOut])
* Presets.Import(Slot, [Options, Label1[=Text]:Icon, Label2[=Text]:Icon, Label3[=Text]:Icon...])
* Presets.Load(Slot)
* Presets.Save(Slot, Buttons)

## Useful Toolbar Styles:
Styles can be applied to Gui command options, e.g.: Gui, Add, Custom, ClassToolbarWindow32 0x0800 0x0100

* TBSTYLE_FLAT      := 0x0800 - Shows separators as bars.
* TBSTYLE_LIST      := 0x1000 - Shows buttons text on their side.
* TBSTYLE_TOOLTIPS  := 0x0100 - Shows buttons text as tooltips.
* CCS_ADJUSTABLE    := 0x0020 - Allows customization by double-click and shift-drag.
* CCS_NODIVIDER     := 0x0040 - Removes the separator line above the toolbar.
* CCS_NOPARENTALIGN := 0x0008 - Allows positioning and moving toolbars.
* CCS_NORESIZE      := 0x0004 - Allows resizing toolbars.
* CCS_VERT          := 0x0080 - Creates a vertical toolbar (add WRAP to button options).

- - -

## Add()
Add button(s) to the end the toolbar. The Buttons parameters sets target Label, text caption and icon index for each button. If not a valid label name, a function name can be used instead (parameters can be passed to the OnMessage method). To add a separator call this method without parameters. Prepend any non letter or digit symbol, such as "-" or "**" to the label to add a hidden button. Hidden buttons won't be visible when Gui is shown but will still be available in the customize window. E.g.: "-Label=New:1", "*Label:2".

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters:
* **Options** - Enter zero or more words, separated by space or tab, from the following list to set buttons' initial states and styles: Checked, Ellipses, Enabled, Hidden, Indeterminate, Marked, Pressed, Wrap, Button, Sep, Check, Group, CheckGroup, Dropdown, AutoSize, NoPrefix, ShowText, WholeDropdown. You can also set the minimum and maximum button width, for example W20-100 would set min to 20 and max to 100. This option affects all buttons in the toolbar when added or inserted but does not prevent modifying button sizes. If this parameter is blank it defaults to "Enabled", otherwise you must set this parameter to enable buttons. You may pass integer values that correspond to (a combination of) button styles. You cannot set states this way (it will always be set to "Enabled").
* **Buttons** - Buttons can be added in the following format: Label=Text:1, where "Label" is the target label to execute when the button is pressed, "Text" is caption to be displayed with the button or as a Tooltip if the toolbar has the TBSTYLE_TOOLTIPS style (this parameter can be omitted) and"1" can be any numeric value that represents the icon index in the ImageList (0 means no icon). You can include specific states and styles for a button appending them inside parenthesis after the icon. E.g.: "Label=Text:3(Enabled Dropdown)". This option can also be an Integer value, in this case the general options are ignored for that button. To add a separator between buttons specify "" or equivalent.

## AutoSize()
Auto-sizes toolbar.

### Return
TRUE if successful, FALSE if there was a problem.

## Customize()
Displays the Customize Toolbar dialog box.

### Return
TRUE if successful, FALSE if there was a problem.

## Delete()
Delete one or all buttons.

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* **Button** - 1-based index of the button. If omitted deletes all buttons.

## Export()
Returns a text string with current buttons and order in Add and Insert methods compatible format (this includes button's styles but not states). Duplicate labels are ignored.

### Return
A text string with current buttons information to be exported.

### Parameters
* **ArrayOut** - Set to TRUE to return an object array. The returned object format is compatible with Presets.Save and Presets.Load methods, which can be used to save and load layout presets.
* **HidMark** - Changes the default symbol to prepend to hidden buttons.

## Get()
Retrieves information from the toolbar.

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* **HotItem** - OutputVar to store the 1-based index of current HotItem.
* **TextRows** - OutputVar to store the number of text rows
* **Rows** - OutputVar to store the number of rows for vertical toolbars.
* **BtnWidth** - OutputVar to store the buttons' width in pixels.
* **BtnHeight** - OutputVar to store the buttons' heigth in pixels.
* **Style** - OutputVar to store the current styles numeric value.
* **ExStyle** - OutputVar to store the current extended styles numeric value.

## GetButton()
Retrieves information from the toolbar buttons.

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* **Button** - 1-based index of the button.
* **ID** - OutputVar to store the button's command ID.
* **Text** - OutputVar to store the button's text caption.
* **State** - OutputVar to store the button's state numeric value.
* **Style** - OutputVar to store the button's style numeric value.
* **Icon** - OutputVar to store the button's icon index.
* **Label** - OutputVar to store the button's associated script label or function.
* **Index** - OutputVar to store the button's text string index.

## GetButtonPos()
Retrieves position and size of a specific button, relative to the toolbar control.

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* **Button** - 1-based index of the button.
* **OutX** - OutputVar to store the button's horizontal position.
* **OutY** - OutputVar to store the button's vertical position.
* **OutW** - OutputVar to store the button's width.
* **OutH** - OutputVar to store the button's height.

## GetButtonState()
Retrieves the state of a button based on a querry.

### Return
The TRUE if the StateQuerry is true, FALSE if it's not.

### Parameters
* **StateQuerry** - Enter one of the following words to get the state of the button** - Checked, Enabled, Hidden, Highlighted, Indeterminate, Pressed.

## GetCount()
Retrieves the total number of buttons.

### Return
The total number of buttons in the toolbar.

## GetHiddenButtons()
Retrieves which buttons are hidden when the toolbar size is  smaller then the total size of the buttons it has. This method is most useful when the toolbar is a child window of a Rebar control, in order to show a menu when the chevron is pushed. It does not retrieve buttons hidden by gui size.

### Return
An array with all buttons hidden by the Rebar band. Each key in the array has 4 properties: ID, Text, Label and Icon.

## Insert()
Insert button(s) in specified postion. To insert a separator call this method without parameters.

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* **Position** - 1-based index of button position to insert the new buttons.
* **Options** - Same as Add().
* **Buttons** - Same as Add().

## LabelToIndex()
Converts a button label to its index in a toolbar.

### Return
The 1-based index for the button or FALSE if Label is invalid.

### Parameters
* **Label** - Button's associated label or function.

## ModifyButton()
Sets button states.

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* **Button** - 1-based index of the button.
* **State** - Enter one word from the follwing list to change a button's state** - Check, Enable, Hide, Mark, Press.
* **Set** - Enter TRUE or FALSE to set the state on/off.

## ModifyButtonInfo()
Sets button parameters such as Icon and CommandID.

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* **Button** - 1-based index of the button.
* **Property** - Enter one word from the following list to select the Property to be set** - Command, Image, Size, State, Style, Text, Label.
* **Value** - The value to be set in the selected Property. If Property is State or Style you can enter named values as in the Add options.

## MoveButton()
Moves a toolbar button (change order).

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* **Button** - 1-based index of the button to be moved.
* **Target** - 1-based index of the new position.

## OnMessage()
Run label associated with button's Command identifier. This method should be called from a function monitoring the WM_COMMAND message. Pass the wParam as the CommandID.

### Return
TRUE if target label or function exists, or FALSE otherwise.

### Parameters
* **CommandID** - Command ID associated with the button. This is send via WM_COMMAND message, you must pass the wParam from inside a function that monitors this message.
* **FuncParams** - In case the button is associated with a valid function, you may pass optional parameters for the function call. You can pass any number of parameters.

## OnNotify()
Handles toolbar notifications. This method should be called from a function monitoring the WM_NOTIFY message. Pass the lParam as the Param. The returned value should be used as return value for the monitoring function as well.

### Return
The required return value for the function monitoring the the WM_NOTIFY message.

### Parameters
* **Param** - The lParam from WM_NOTIFY message.
* **MenuXPos** - OutputVar to store the horizontal position for a menu.
* **MenuYPos** - OutputVar to store the vertical position for a menu.
* **BtnLabel** - OutputVar to store the label or function name associated with the button.
* **ID** - OutputVar to store the button's Command ID.
* **AllowCustom** - Set to FALSE to prevent customization of toolbars.
* **AllowReset** - Set to FALSE to prevent Reset button from restoring original buttons.
* **HideHelp** - Set to FALSE to show the Help button in the customize dialog.

## Reset()
Restores all toolbar's buttons to default layout. Default layout is set by the buttons added. This can be changed calling the SetDefault method.

### Return
TRUE if successful, FALSE if there was a problem.

## SetButtonSize()
Sets the size of buttons on a toolbar. Affects current buttons.

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* **W** - Width of buttons, in pixels
* **H** - Height of buttons, in pixels

## SetDefault()
Sets the internal default layout to be used when customizing or when the Reset method is called.

### Return
Always TRUE.

### Parameters
* **Options** - Same as Add().
* **Buttons** - Same as Add().

