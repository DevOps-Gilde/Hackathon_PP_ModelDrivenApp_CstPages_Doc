# 1. Introduction to Wizard

You should now have Completed the Following things:

1. Importing database

Next you will implement a page within our application.

# 2. Completing the wizard

## Introduction

Each step of the wizard is implemented as a separate screen within the same custom page. In the default the ability to create multiple screens is disabled. The screenshot below shows the setting if you want to create your own application:

TODO screenshot

In that step you will implement the first half of the first step of the wizard which enables the user to edit or create a new import. In the first half you will create the main content page. 

TODO picture

After having completed everything the application will display an information message when you click the submit button.

The learning goals are as stated before:
* Layouting controls
* Working with the form control (New Mode)
* Power FX expressions for navigation

## Layouting controls

As you know it from other environments our application shall support responsive layout so we will avoid pixel based statements. A key are containers that allow to layout their children components are horizontally or vertically. Child controls can be seized relatively based on a percentage (1 corresponds to entire space). The screenshot below shows how to layout the controls when we think in containers:

TODO picture

Let's now implement the layout with the indicated controls. We will start with the first one which is the vertical container for the content. Adding controls always follows the same pattern which is as follows:
* Select the parent control on the canvas
* Pick the control from the list
* Adjust properties
We have to do the following adjustments for our newly added container:
* Reorder
* Set fill
* Rename

Insert the remaining controls and name them accordingly:

|Control   |Name Parent   |Name  |
|---|---|---|
|Form   |   |   |
|Button   |   |   |

## Create or Edit Header

In this step of the wizard we either create or update the header of an existing import. We will use the form to achieve that combined with a button that is triggering create or edit. As a first intermediate step the button will first display the values of the form in an alert window.

First we have to wire our form with the underlying ...HDR table. Go to the data source property and select the table.

TODO screenshot

In our case we need all custom columns that start with CST. Select them as indicated in the screenshot.

TODO screenshot

Creating or editing is defined by the property mode. The value depends in our case of the context that was passed when the first step was called. Enter the following expression for property TODO. 

TODO screenshot

For the mode NEW we have completed all major fields. However in case of edit the control has no idea which record we want to edit. The control provides the Item property we want to edit (In the mode New the value is ignored). Set the expression as follows:

TODO expression
 
As a last step we set the relative height so that the form occupies minimum space.

TODO expression

Now only the button needs to be configured. Change the Text property to "Submit". The property "OnSelect" contains the action when the button is pressed. For now this shall include a popup window. You can reference each value for a given input field by following the hierarchy. E.g. the expression TODO yields the value of the TODO. Enter the following expression TODO in the "OnSelect" property.

## Navigation

As you have already seen there are a lot of different artefacts like screens and pages that need to be linked. Our page is not yet correctly wired.

Both buttons `Previous`and `Home` at the footer still need to be configured.
TODO What are the expressions

Switch to the custom page TODO. There the `OnSelect` property of the buttons `New`and `Edit` needs still to be implemented. In that case we have to achieve two things: (1) jump to the first screen within the wizard and (2) set the context accordingly.
TODO What are the expressions

# 3. Testing changes

Testing changes is quite easy trough the `Play` button that is provided by the web portal. Don't forget to save and publish your changes before testing. You have to run the application in the right scope. That means:
* Local changes within a custom page

  Just press the play button to start the custom page. The crseenshot below shows an example. Use the `X` button at the right top corner to switch back into edit mode.
  TODO screenshot

* Changes that span Custom Changes

  Make first sure you switch back to the model driven app. Press the `Back` button at the top of the screen to switch to the App. Just press the play button to start the custom page. The screenshot below shows an example. Use the `X` button at the right top corner to switch back into edit mode.
  TODO screenshot

A full test will require to test on app level due to the cross navigation.