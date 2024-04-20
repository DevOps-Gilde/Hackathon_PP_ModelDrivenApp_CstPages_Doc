# 1. Introduction to Wizard

You should now have completed the following things:

1. Importing implemented artefacts

Next you add the required controls for the first step of the wizard and wire them with the rest of the application.

# 2. Goal

Each step of the wizard is implemented as a separate screen within the same custom page. In the default setup the ability to create multiple screens is disabled. We enabled this setting already for you. The screenshot below shows where the setting can be found:

<br><img src="./images/wiz_layout_mul_scr_setUntitled.png" /><br>

The screenshot below shows the starting point. As you can see the main content of the first header step is missing. Moreover no action is implemented when you click the home or next button.

<br><img src="./images/wiz_layout_scope_tasks_start.png" /><br>

The screenshot below shows the result if you have completed all implementation tasks when you add a new record.

<br><img src="./images/wiz_layout_scope_tasks.png" /><br>

This includes
* Form and Submit button and enabling of fields accordingly
* Being able to clear the date when you press the button
* Display an information message when you click the submit button
* navigating to correct screen when you click next or home button

# 3. Implementation Tasks
## Add controls for main content

Navigate to the page for approvals named `PgManageImps` within the app as shown in the screenshot below and click the edit icon:
<br><img src="./images/wiz_layout_page_import.png" /><br>

You will notice that this page is again split into multiple screens on the left side, which can fill the whole or only parts of the page:
- OvrImports
- WizardStepImpHeader
- WizardStepUploadData
- WizardStepAppr

Click through them to see the whole page changing. We can later use `Navigate()` Buttons to travel between them with a selected amount of local variables instead of using global ones. For now we will focus on WizardStepImpHeader.

As you know it from other environments our application shall support responsive layout so we will avoid pixel based statements. A key are containers that allow to layout their child components based on relative a measurement such as a percentage. Container layout their children either horizontally or vertically and can be nested. We already implemented the first container for you that uses the expressions `Parent.Width` and `Parent.Height` to occupy all space of the screen. The screenshot below shows the starting point. As you can see there is a gap in the sense that the main content is missing:
<br><img src="./images/wiz_layout_start_point.png" /><br>

To implement the content we need first an additional container. We need it to group the form and the submit button. They are comparable to a `div`element in HTML. We will start with the vertical container for the content. Adding controls always follows the same pattern which is as follows:
* Select the parent control `WizardStepImpHdrLayout` on the canvas or in the tree on the left-hand side
* Add the control `Vertical container` from the list under `+Insert`

  If you don't see the control in the list you have to look under `Layout`. The newly added container will be added to the end of the children list. That is not what we want, since it must be placed between header and footer.

* Reorder newly added container

  Click on the context menu (...) of the container control in the tree view. There you find the option `Move up` to move it as shown below:
  <br><img src="./images/wiz_layout_reorder.png" /><br>
  You can also use `Ctrl+]` and `Ctrl+[` on keyboard layouts that don't need ALT for the brackets, because ALT is used as a quick way to simulate interactions inside the Editor without starting the simulator. [Other shortcuts can be found here](https://learn.microsoft.com/en-us/power-apps/maker/canvas-apps/keyboard-shortcuts).

* Adjust properties

  First we have to make sure that container fills the bulk of the screen. The screenshot below shows the relevant settings on the right-hand side:
  <br><img src="./images/wiz_layout_fill.png" /><br>
  Adjust the following properties as follows:
  * Activate flexible height if not already done
  * Set the first figure of `Fill portions` to `0.8` which corresonds to 80 percent of the space
  * make sure that the `Alignment in container` is as shown

  We won't need the container anymore later so the name is up to you.

Select the newly added container so that it is going to become the new parent for insert. Insert the following remaining controls in the same way and order:
* An `Edit Form` via using the `+Insert` option add the top
  When you add the form the editor will offer you options to jump right into the configuration as shown in the screenshot below. 
  <br><img src="./images/wiz_layout_form_added.png" /><br>
  We postpone that or later and continue with adding another control. Select newly added container again so that the next control is inserted with the correct parent.
* A `Button` via using the `+Insert` option add the top

The form will be referenced later in code snippets. Rename the newly added form to `WizardStepImpHdrMainView` to ensure the code snippets work. The option rename is available via context menu within the tree view that we use for reorder. You can also edit the name in the property pane at the right by clicking at the pencil icon as shown in the screenshot below. The newly added button won't be referenced so the name is up to you.
<br><img src="./images/wiz_rename_ctrl.png" /><br>

## Configure added Form
### Understanding Dataverse

Our form will be bound to a table in dataverse to add new records and add existing ones. Before we work with the Form you should make yourself familiar with Dataverse.
Open the Data Menu on the left side and click on the `...` next to the `IMP_CO2_CONS_RAW_HDR` table to go to the minimalistic `Edit data` view. 
<br><img src="./images/wiz_layout_open_dataverse.png" /><br>

Here you can expand your view by clicking on `+24 more` and adding the column `CST_IMP_USERNAME`.
You can view each column settings by clicking on the titles and selecting `Edit column` in the upcoming context menu. The screenshot below shows displayed column information from the `CST_IMP_CODE` column.
<br><img src="./images/wiz_enter_usernames.png" /><br>
As you can see the column uses autogenerated values (Data Type = `Autonumber`) and therefore you cannot directly enter a value in the UI for it. Editing the value in the newly selected column `CST_IMP_USERNAME` is possible but not via directly typing. In this case it is not working though, because it is no text field, but a lookup field. It can only select entries from a different table it is looking at. Currently there is no entry inside to select and we are going to change that.

Open a new browser tab at [https://make.powerapps.com/](https://make.powerapps.com/) and go to `Tables`, filter `All` and click on `IMP_USER`.
<br><img src="./images/wiz_layout_open_usertable_dataverse.png" /><br>

This opens the bigger Table view where you can also inspect the Schema of the columns for their important schema and logical name under `Columns` -> `...` -> `Advanced` -> `Tools` and much more. At the bottom you see the column `CST_USERNAME` which is not the primary key of the entry, but the user-friendly "primary name column". To fill this entry simply write any text under it. Other fields will automatically set default values like the current date in the other column.
<br><img src="./images/wiz_layout_edit_usertable_dataverse.png" /><br>

After doing so you can go back to the prior `IMP_CO2_CONS_RAW_HDR` table and under the lookup column `CST_IMP_USERNAME` the option for your new username should be selectable. Create at least one row `IMP_CO2_CONS_RAW_HDR` with values for the `CST_IMP_XXX` in th screenshot below so that you can test the form also in edit mode.
<br><img src="./images/wiz_layout_add_imptable_dataverse.png" /><br>

You do not need to save this change and can close the view by discarding all changes.

### Wire form with data source/ columns

Go back to the page `PgManageImps` in edit mode and select our newly added form `WizardStepImpHdrMainView`.

First we have to wire our form with the underlying `IMP_CO2_CONS_RAW_HDR` table. Go to the `Data source` property and select the table.
<br><img src="./images/wiz_layout_ctrls_frm_ds.png" /><br>

Next we have to pick all relevant columns. Click on `Edit fields`. You see then the already selected columns.
<br><img src="./images/wiz_layout_ctrls_frm_fields.png" /><br>

Remove the column `Created On` by hovering over the entry. In the appearing context menu (...) on the right hand side you find an option to delete it. Select now all missing columns that start with `CST_IMP` by clicking on `+ Add field` as shown below:
<br><img src="./images/wiz_layout_ctrls_frm_sel_cols.png" /><br>

As a reaction you will now see additional input cards. Each card covers one column. Each card consists of multiple controls. We will need them later. Therefore naming and a better understanding of the control structure is important. The screenshot belows shows the description card:
<br><img src="./images/wiz_layout_ctrls_frm_desc_card.png" /><br>

The important take aways:
* A card contains multiple controls
* Control holding the user input => here `DataCardValue3`
* Other controls that contain other visual parts such as column label, asteriks etc.

Rename the controls **HOLDING THE USER INPUT** listed below as stated since we need them later:
|Card               |Technical Control Type| Rename To|
|-------------------|-----------------------------------|-----|
|Importing user name|ComboBox                          | WizardStepImpHdrMainViewImportUserNameDropDown|
|Year               |TextInput                         |                            WizardStepImpHdrMainViewImportYearTextBox|
|Description        |TextBox                           |WizardStepImpHdrMainViewImportDescTextBox|
|Date Timestamp     |Datepicker                           |WizardStepImpHdrMainViewImportTSDatePicker|

Set `Fill portions` of the form on the tab `Properties` to `0.2`. It ensures that the form occupies minimum space.

### Configuring DefaultMode of the form

Creating or editing is defined by the property `Default mode`. The new and the edit scenario require different values. That is the first case where we need a formula to determine the correct value. Two ways exist:
* Entering it in the properties on the right-hand side
* Formular bar

  The screen below shows it:
  <br><img src="./images/wiz_layout_ctrls_frm_mode_fx.png" /><br>

  To enter any formular for a given property do the following:
  * select the name of the property on the left-hand side (here DefaultMode)
  * set the expression on the right hand side after the Fx icon

  You can drag the bottom formular bar border downwards or click the arrow on the right side of it to expand it.

  Overwrite the existing value with the following simple if expression: 
  
  `If(locImpMode = "Edit", FormMode.Edit, FormMode.New)`
  
  Explanations regarding the expression:
  * `locImpMode` is the local variable that contains the mode. Its value is set when you jump to this screen from the import over `OvrImports`.
  * The setting of the value for `locImpMode` we already implemented for you when you click the buttons new/ edit on the import overview screen. 

For the mode `New` we have completed all major fields. Edit requires additional information about the record to edit. The control provides the `Item` property on the tab `Advanced` for that purpose (In the mode New the value is ignored). Set the expression as follows:
```
LookUp(
  IMP_CO2_CONS_RAW_HDR, 
  CST_IMP_CODE = locImpCode)
```
Explanations regarding the expression:
* `IMP_CO2_CONS_RAW_HDR` denotes the table we are looking at
* `LookUp` retrieves the record that fulfills the condition. It is a first example of the excel like [Power Fx formula](https://learn.microsoft.com/en-us/power-platform/power-fx/overview) you are working with.
* `CST_IMP_CODE = locImpCode` represents the condition that filters the currently edited record

### Customize timestamp card with reset button 

Deleting text of a Date field is not intuitive and therefore we are going to add a reset button to the card holding the timestamp.
To achieve that we first have to unlock the card to be able to edit them. Make sure you selected the card either via tree view or by clicking at it. To unlock them click on the lock icon at the top of the `Advanced` tab:
<br><img src="./images/wiz_layout_ctrls_frm_enabled_lock.png" /><br>

Select the unlocked card and insert a new button. Make the existing controls smaller so that you have enough space for the new button with a text of your own choice such as "Clear". For the desired functionality we have to implement now some custom formulas. This is the basic idea:
* We use a local variable `resetdateTS` as clearing indicator

  This variable needs to be initialized in a controled way. We will do it when the formular becomes visible. We will use the `OnVisible` property of the screen. This property allows us to bundle this initialization with potential others. Moreover it will be known immediately when we use th variable later on. Using other places might result in a temporary error in the editor that is first resolved when you run the code via the `Play` button.  

* We define a formula to override the default behavior based on the indicator
  
  In the default setup the field is wired to the corresponding fields within the data source. Controls holding a value delegate getting the value to its parent control (=card) by `Parent.Default`.

To initialize the new local variable `resetdateTS` go to the screen `WizardStepImpHeader` and select the property `OnVisible`. Add the line `UpdateContext({resetdateTS:false})`. `UpdateContext` sets the context of the associated screen with new or changed local variables such as `resetdateTS`.
In the date picker `WizardStepImpHdrMainViewImportTSDatePicker` we override the default behavior by setting the `Value` to `If(resetdateTS,Blank(),Parent.Default)`. Thanks to the `If` you see now the empty value (=`Blank()`) when this formula is applied and the local variable. 
Otherwise Parent.Default redirects to the Default value of its parent element `WizardStepImpHdrMainViewImportTS`, which is directly connected to `ThisItem.CST_IMP_TS` to overwrite its table data.

The last missing piece is the newly added button. Set its `OnSelect` property to the following expression: `UpdateContext({resetdateTS:true}); Reset(WizardStepImpHdrMainViewImportTSDatePicker);`. The expression consists of two statements:
* `UpdateContext({resetdateTS:true});` creates the prerequisite that a blank value is displayed by setting the local variable
* `Reset(WizardStepImpHdrMainViewImportTSDatePicker);` is triggering a reevaluation of the formula behind the `Value` of the named control here `WizardStepImpHdrMainViewImportTSDatePicker`

Note that the instructios only clear the date part of the timestamp. If you want include hours and minutes you have apply the same pattern.

### Customize display mode 

Due to our application setup it makes no sense that certain fields are editable. These are:
* CST_IMP_CODE = since the value is autogenerated
* CST_IMP_STATE/ CST_IMP_TS (New only) = since the values will be set later in our PowerAutomate flow

With the standard configuration the field import code is still displayed as editable but you cannot jump into it. To avoid confusion we want to disable it for creating a new record. Also the other two we want to disable but only for the edit case.

Unlock the property `DisplayMode` on the tab `Properties` also for the cards CST_IMP_CODE, CST_IMP_STATE. Overwrite the existing value with the following expression:
* CST_IMP_CODE: `DisplayMode.Disabled`
* CST_IMP_STATE/ CST_IMP_TS: `If(locImpMode = "New", DisplayMode.Disabled, Parent.DisplayMode)`

Explanations regarding the expression:
* `DisplayMode.Disabled` disables the card
* `Parent.DisplayMode` enforces the default behavior

## Configure added Submit Button

We are finished and can switch over to the button. Change the `Text` property on the tab `Properties` to `Submit`. The property `OnSelect` contains the action when the button is pressed. For now we will just display an information that proofs we can access the values in the form. Enter the following expression in the `OnSelect` property on the tab `Advanced`:

```
UpdateContext({
  myDescription: WizardStepImpHdrMainViewImportDescTextBox.Value & " This element needs a checkup on: " & Text( DateAdd( Now(), 7 ), "dd-mm-yyyy at hh:mm" )});

Notify(
  "Changes submitted for import " & WizardStepImpHdrMainViewImportDescTextBox.Value & " submitted. " & myDescription, 
  NotificationType.Information)
```

Explanations regarding the expression:
* `UpdateContext` will fill the `myDescription` variable with derived or even calculated data. Since the form card selects the new `myDescription`, it could directly insert it into our database
* `Notify` displays a message of the given type
* `&` is the operator for concatenating strings

## Navigation

As you have already seen we work with screens to separate things. They are linked and the first step of our wizard is not yet correctly wired. Both buttons `Next` and `Home` at the footer still need to be configured.

<br><img src="./images/wiz_nav_buttons.png" /><br>

`Next` means we just refer to the screen representing the second step in our wizard. In addition to that we have to pass required context information. This context information includes:
* The primary key of the newly created/ edited record
* The import state of the newly created/ edited record

The `Navigate` command allows to jump to the designated screen and to pass local parameters. This is important as we don't want to use global variables! Set the `OnSelect` property of the button to the following expression:

```
Navigate(
  WizardStepUploadData, 
  ScreenTransition.None, 
  { 
    locImpState: locImpState, 
    locImpCode: locImpCode})
```

Explanations regarding the expression:
* `{}` is an arbitrary json structure that we use to pass the information
* `WizardStepUploadData` is the name of new screen and we just pass the current values of the local variables.

The `Home` button shall reference the entry page for the importer. Passing any parameters is not required. Therefore just set the `OnSelect` of the button to `Navigate(OvrImports, ScreenTransition.None, {})`. Local variables will be correctly adjusted because in the overview page because we implemented the `OnVisible` property of the overview screen.
  
# 4. Testing changes

For testing you have the following options. For our case quicktests are sufficient. The second option is only given as information:
* Quicktests

  Ad hoc test of changes is quite easy trough the `Play` button (Triangle icon) that is provided by the web portal as shown by the first screenshot. The current screen selected in the tree view is assumed as screen under test. 
  <br><img src="./images/wiz_layout_test.png" /><br>
  
  An important setting is the icon besides the `X`. When you click on it choose the option `Canvas size` as shown below. The screen is then rendered as in the designer.
<br><img src="./images/wiz_layout_test_scr_opt.png" /><br>

  To finish the test mode click the `X` as shown in the screenshot below:
  <br><img src="./images/wiz_layout_stop.png" /><br>

  A problem of that approach is the setting of the context. In our case you can achieve it by starting with the importing overview screen. In a more complex case with many test cases this might mean a lot of clicking.

* Automated Testing

  Currently the tools from Microsoft only support canvas apps. Therefore we cannot use them. Support for model driven apps is announced.
  It allows you to define test cases that consist of steps. The two screenshots of the [`Test Studio`](https://learn.microsoft.com/en-us/power-apps/maker/canvas-apps/working-with-test-studio) below shall give you only an idea:
  <br><img src="./images/tst_start_studio.png" /><br>
  <br><img src="./images/tst_studio_define_tc.png" /><br>

  [`Test engine`](https://github.com/microsoft/PowerApps-TestEngine) is the recommended new kid in the block which is still in an experimental state. Test Engine builds upon the key use cases of Test Studio, but takes it in a new, powerful direction through open source collaboration and use of the Playwright browser testing platform.

* Running application

  In rare edge cases this is the last feedback due to observed problems in the Quicktests environment. 

We will use the quicktests. All test cases must start from the import overview screen. Therefore, make sure the import overview screen is selected in the tree view before you click at the `Play` button.

Thanks to your changes the following scenarios should now work:
|Test                                             |Expected Result                          |
|-------------------------------------------------|------------------------------------------|
|Creation of new record |Click on new import button in the import overview screen. Fields on the form are empty. Clicking on the submit button should show an additional info message.|
|Editing existing record |Filter down to a single record and click on the edit import button in the import overview screen. Fields on the form are prefilled with the record you selected. Clicking on the submit button should show an additional info message.|
|Clear Date of the timestamp|Filter down to a single record and click on the edit import button in the import overview screen. Clicking the reset button should clear the date and should be able to select a new one.|
|Next button at the wizard clicked          |Next screen is displayed                  |
|Home button at the wizard clicked         |Overview page is shown from where wizard was triggered (Correct display of list only when you run the app)|
