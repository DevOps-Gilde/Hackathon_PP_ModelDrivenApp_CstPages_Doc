# Power Apps - Hackathon (Model-Driven Custom Pages)

## Focus

This repo contains the documentation for the Power Apps hackathon. The application to complete will be a **model driven app with Custom Pages**.

:warning: Note this documentation is a preliminary state where not all features of the application are already implemented!

The business scenario of our example app is the import of CO2 consumption figures from a local file. They will have to approved before showing up in a consolidated table. A wizard will guide the importing user.

The hackathon includes the following technologies:
* Power Apps: Model driven apps with custom pages
* Power Automate: Flows (embedded in Power Apps)
* Using dataverse & solutions

Out of scope are the following technologies:
* Power Apps

  Other app types such as Power Pages/ Canvas apps. Model driven apps based on dashboards/ dataverse Table based pages are also out of scope.
  
* Creation of underlying dataverse data model (We provide a full implementation that only needs to be imported by you into the environment)

The following things will be provided to you:

* Power Platform Environment and user to fill the gaps in our application
* Fully implemented data model
* A partially implemented application with gaps for you to fill

[This repo](https://github.com/DevOps-Gilde/Hackathon_PP_ModelDrivenApp_CstPages_Code) contains the code for this documentation. Code includes the starting point for this hackathon and a fully implemented application.

## Prerequirements

No extra tooling will be required due to the LowCode platform except for a browser. No deep GitHub/ Git know-how is required. It is only required to download files for the partially implemented application and the fully implemented data model from GitHub.

## Session preparation

Power Platform is LowCode environment that is probably new to most of us. Therefore read the following chapters BEFORE the hackathon. Otherwise you won't be able to do much coding:

1. Get familiar with Platform & Application Scenario [here](/01_PrimerPPAppScenario.md)<br>

## Session implementation tasks

The following tasks will expect you:

2. Import the already implemented artefacts [here](/02_ImportImplementedArtefacts.md)<br>

3. Implement Wizard Step Header (Part1) [here](/03_ImplementWizardStep1Part1.md)

   This step of the wizard is about creating a new import header or editing an existing one. Part one only includes adding the control and wiring them with the rest. Learning goals of this step are:

   * Layouting controls
   * Configuring controls (EditForm, Button)
   * Defining actions when certain events happen such as a click of a button

   After that the changes are not yet persisted to dataverse.

4. Implement Wizard Step Header (Part2) [here](/04_ImplementWizardStep1Part2.md)
   
   In that step you add the missing persistence.

5. **Optional advanced extra task:** Adjust list of imports for approval [here](/05_AdjustApprovalList.md)

:white_check_mark: We also created a partially implemented application including data model located in the branch [Solution](https://github.com/DevOps-Gilde/Hackathon_PP_ModelDrivenApp_CstPages_Doc/tree/Solution) of your forked repository that covers all tasks. You only have to import it to your environment. Note that the import slightly differs in that case. Check out [here](/02_ImportImplementedArtefacts.md) how to do it.

If at any Point you need assistance nevertheless do not hesitate to ask. We are here to Help you.
