# 1. Introduction to Wizard

You should now have Completed the Following things:

1. Importing Implemented Artefacts

Next you add the required controls to the first step of the wizard and wire it with the rest of the application.

# 2. Implementation Task

## Introduction

Each step of the wizard is implemented as a separate screen within the same custom page. In the default the ability to create multiple screens is disabled. The screenshot below shows the setting if you want to create your own application:

<br><img src="./images/wiz_layout_mul_scr_setUntitled.png" /><br>

In that step you will implement the first half of the first step of the wizard which enables the user to edit or create a new import. In the first half you will create the main content page. 

<br><img src="./images/wiz_layout_scope_tasks.png" /><br>

After having completed everything the application will display an information message when you click the submit button.

The learning goals are as stated before:
* Layouting controls
* Working with the form control (New Mode)
* Expressions for navigation

## Layouting Form and Button

As you know it from other environments our application shall support responsive layout so we will avoid pixel based statements. A key are containers that allow to layout their child components based on relative a measurement such as a percentage. Container layout their children either horizontally or vertically and can be nested. We already implemented the first container for you that uses the expressions `Parent.Width`and `Parent.Height` to occupy all space of the screen. The screenshot below shows the starting point. As you can see theer is a gap in the sense that the main content is missing:

<br><img src="./images/wiz_layout_start_point.png" /><br>

Let's now implement the content for which we need an additional container (to block the bulk of the screen) and the child controls (Form and button). We will start with the vertical container for the content. Adding controls always follows the same pattern which is as follows:
* Select the parent control `WizardLayout_Create` on the canvas
* Pick the control from the list `+Insert`

  This will add the new container to the end of the children list. That is not what we want, since it must be placed between header and footer.

* Reorder newly added container

  You have to click on the context menu (...) dots of the control in the tree view. There you find the option to move it as shown below:
  <br><img src="./images/wiz_layout_reorder.png" /><br>

* Adjust properties

  First we have to make sure that container fills the bulk of the screen. The screenshot belows shows the relevant settings:
  <br><img src="./images/wiz_layout_fill.png" /><br>
  Adjust the following peoperties as follows:
  * Activate flexible height if not already done
  * Set the first figure of `Fill posrtions' to `0.8`which corresonds to 80 percent of the space
  * make sure that the `Alignment in container` is as shown

* Rename the newly added control to `Content_Create`

Insert the remaining controls according in the same way and name them accordingly:

|Control   |Name Parent   |Name  |
|---|---|---|
|EditForm   |Content_Create   |up to you   |
|Button   |Content_Create   |up to you  |

## Configure Form and Button

In this step of the wizard we either create or update the header of an existing import. We will use a form to achieve that combined with a button that is triggering create or edit. As a first intermediate step the button will first display the values of the form in an alert window.

To add the form as child control select the newly added container. Pick the control `EditForm` in the same way as you did the container. All further explanation refer to the newly added form. 

First we have to wire our form with the underlying IMP_CO2_CONS_RAW_HDR table. Go to the data source property and select the table.

<br><img src="./images/wiz_layout_ctrls_frm_ds.png" /><br>

Next we have to pick all relevant columns. Click on `Edit fields` and select all custom columns that start with `CST`. Select them as indicated in the screenshot.

<br><img src="./images/wiz_layout_ctrls_frm_sel_cols.png" /><br>

Creating or editing is defined by the property mode. The value depends in our case of the context that was passed when the first step was called. That is the first case where we need a formula to determine the correct value. That is not possible using the predefined values at the right-hand side. We have to use formular bar that is similar to excel as shown below:

<br><img src="./images/wiz_layout_ctrls_frm_mode_fx.png" /><br>

To enter any formular for a given property do the following:
* select the name of the property on the left-hand side (here DefaultMode)
* set the expression on the right hand side after the Fx icon

  The expression in our case is a simple if expression: `If(TODOVarMode, FormMode.New, FormMode.Edit)`. The tested expression refers to the context wizard. The setting of the value for `TODOVarMode` we alraedy implemented for you when you click the buttons on the overview page. 

For the mode `New` we have completed all major fields. However in case of edit the control has no idea which record we want to edit. The control provides the Item property we want to edit (In the mode New the value is ignored). Set the expression as follows: `TODOSelectedItem`. The setting of the value for `TODOSelectedItem` we alraedy implemented for you when you click the buttons on the overview page. 

As a last step we set the relative height so that the form occupies minimum space. Set `Fill portions` to `0.2`.

We are fnished and can switch over to the button. Select the newly added container again. Pick the control `Button` in the same way as you did the 

Change the Text property to `Submit`. The property `OnSelect` contains the action when the button is pressed. For now we will just display an information that proofs we can access the values in the form. Enter the following expression in the "OnSelect" property: `Notify(<name of the value below the card within the form>, NotificationType.Information)`. The name can be obtained by the tree view as shown below:

<br><img src="./images/wiz_layout_ctrls_btn_frm_value.png" /><br>

## Navigation

As you have already seen there are a lot of different artefacts like screens and pages that need to be linked. Our page is not yet correctly wired.

Both buttons `Next` and `Home` at the footer still need to be configured.

`Next`means we just refer to another screen within the same page. The `Navigate(<name of screen>)` taks you there. Set the `OnSelect` property of this expression with the name of the screen as parameter.

The `Home` button is a bit more difficult since the code shall jump back to the overview custom page we come from. When you search the internet you find various options. Therefore a quick overview:
* Referencing by URL

  Custom pages have URL of the following format: `https://<orgname>.crm16.dynamics.com/main.aspx?appid=<app id>&pagetype=custom&name=<internal name of page>`. The expressions to use this are `Launch(URL)`. On the targeted custom page you can read the with `Param` (Sources: [URL Format](https://powerusers.microsoft.com/t5/Building-Power-Apps/Navigating-from-one-custom-page-to-another-with-parameters/td-p/1418875), [MS Docs](https://learn.microsoft.com/en-us/power-platform/power-fx/reference/function-param)).

  Although technically feasible it is not recommended for the following reasons:
  * Works only in final app and not in the emedded testing app
  * No check support since url is black box

* Navigate

  This is the recommended way. The required expression is `IF(TODOContext, Navigate(<name page imp>, Navigate(<name page appr>)`. 
  A special challenge is navigating to a page and passing parameters. We already did it for you at the overview pages as follows: `Navigate(<name of list>.Selected, { Page: <name of page>})` (note that the names are without single or double quotes). The biggest problem was the missing designer support for the second argument (See also [here](https://www.google.com/search?q=power+platform+passing+context+to+custom+page&rlz=1C1UEAD_enDE999DE999&oq=power+platform+passing+context+to+custom+page&aqs=chrome..69i57.14024j0j9&sourceid=chrome&ie=UTF-8#fpstate=ive&vld=cid:e81c6c9f,vid:UDmGd5Qb4rY)).
  
# 3. Testing changes

Testing changes is quite easy trough the `Play` button that is provided by the web portal as shown by the first screenshot. To finish the test mode click the `X`as shown in the second screenshot below:

<br><img src="./images/wiz_layout_test.png" /><br>
<br><img src="./images/wiz_layout_stop.png" /><br>

Don't forget to save and publish your changes before testing. You have to run the application in the right scope. That means:
* Local changes within a custom page

  In that case you don't have dependencies to other custom pages. An example is correctly layouting the controls.

* Changes that span Custom Changes

  In that case dependencies exist. Dependencies might mean targeting other pages or setting values as context for the custom page under test.

Thanks to your changes the following scenarios should now work:
|Test                                             |Scope | Expected Result                          |
|-------------------------------------------------|------|------------------------------------------|
|Wizard first step: Main content displayed correctly |Local |Next screen is displayed               |
|Wizard first step: Click on next button          |Local |Next screen is displayed                  |
|Wizard first step: Click on home button          |Global|Overview page is shown from where wizard wa striggered|
|Import Overview Page: Click on new import button |Global|Fields on the form are empty|
|Import Overview Page: Select a single record and click on edit import button|Global|Fields on the form are prefilled with the record you selected|
