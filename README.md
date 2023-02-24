# Power Apps - Hackathon (Model-Driven Custom Pages)

## Focus

This repo contains the documentation for the Power Apps hackathon. The application to complete will be a **model driven apps with Custom Pages**. The business scenario of our example app is the import of CO2 consumption figures from a local file. They will have to approved before showing up in a consolidated table.

The hackathon includes the following technologies:
* Power Apps: Model driven apps with custom pages
* Power Automate: Flows (embedded in Power Apps)

Out of scope are the following technologies:
* Power Apps: Other app types such as Power Pages/ Canvas apps
* Model driven apps: Dashboards/ Dataverse Table based pages
* Creation of underlying dataverse data model (We provide a full implementation that only needs to be imported by you into the environment)

The following things will be provided to you:
* Power Platform Environment and user to develop our application
* Fully implemented data model
* A partially implemented application with gaps for you to fill

[This repo](https://github.com/DevOps-Gilde/Hackathon_PP_ModelDrivenApp_CstPages_Code) contains the assumed code for this documentation.

## Prerequirements

No extra tooling will be required due to the LowCode platform except for a browser. No deep GitHub/ Git know-how is required. It is only required to download the partially implemented application and the fully implemented data model from GitHub.

## Session preparation

Power Platform is loc code environment that is probably new to most of us. Therefore read the followin chapters beforehand. Otherwise you won't be able to do much coding:

1. Get familiar with Platform & Application Scenario [here](/01_PrimerPPAppScenario.md)<br>

## Session implementation tasks

The following tasks will expect you:

2. Import the already implemented artefacts [here](/02_ImportImplementedArtefacts.md)<br>

3. Implement Wizard Step Create/ Update (Part1) [here](/03_ImplementWizardStep1Part1.md)

   Part one only includes adding the control and wiring them with the rest. Learning goals of this step are:

   * Layouting controls
   * Configuring controls (EditForm, Button)
   * Defining actions when certain events happen such as a click of a button

4. Implement Wizard Step Create/ Update (Part2) [here](/04_ImplementWizardStep1Part2.md)

   Part two includes implementing the creation of a new import with a flow. Reason is a limitation of the EditForm control that does not return the values for the newly created record. For the edit case the standard functionality is sufficient.

5. **Optional advanced extra task:** Implement approval [here](/05_ImplementApprovalFlow.md)

:white_check_mark: We also created a working solution located in the branch [Solution](https://github.com/DevOps-Gilde/Hackathon_PP_ModelDrivenApp_CstPages_Doc/tree/Solution) of your forked repository that covers all tasks. The solution is provided as solution so you have to import it to your environment.
If at any Point you need assistance nevertheless do not hesitate to ask. We are here to Help you.
