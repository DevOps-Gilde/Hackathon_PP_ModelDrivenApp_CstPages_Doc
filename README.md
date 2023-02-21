# Power Apps - Hackathon (Model-Driven Custom Pages)

## Focus

This repo contains the documentation for the Power Apps hackathon that is focusing at an example scenario using **model driven apps with Custom Pages**. The hackathon includes the following technologies:
* Power Apps: Model driven apps
* Pages: Custom Pages
* Power Automate Flows (embedded in Power Apps)

Out of scope are the following technologies:
* Power Apps: Other app types such as Power Pages/ Canvas apps
* Pages: Dashboards/ Dataverse Table based pages
* Creation of underlying dataverse data model (Solution with fully implemented data model only needs to be imported by you)

The following things will be provided to you:
* Environment

  It will be the place where you develop your application. The user will be initialised with read-only permissions so that you can get used yuo the environment including knowing where to find what. During the hackathon the user will be given elevated permissions so that you implement the gaps in the application.

* Solution file to import the fully implemented data model

[This repo](https://github.com/DevOps-Gilde/S3_Code_GitHubActionsTerraform) contains the assumed code for this documentation.

## Prerequirements

No extra tooling will be required due to the LowCode platform.

## Session preparation

We strongly recommend that you carry out the tasks below before the hackathon session starts. It helps you to maximize the time for coding:

1. Get familiar with Platform & Application Scenario [here](/01_PrimerPPAppScenario.md)<br>
2. Import the database solution [here](/02_ImportDataverseDatamodel.md)<br>

## Session implementation tasks

The following implementation tasks will expect you:

3. Implement Wizard Step Create/ Update (Part1) [here](/03_ImplementWizardStep1Part1.md)

   Part one only includes adding the control and wiring them with the rest. Learning goals of this step are:

   * Layouting controls
   * Configuring controls (Form, Button)
   * Power FX expressions for navigation

4. Implement Wizard Step Create/ Update (Part2) [here](/04_ImplementWizardStep1Part2.md)

   Part two includes implementing the creation of a new import with a flow. Reason is a limitation of the form control that does not return the values for the newly created record.

5. **Optional advanced extra task:** Implement approval [here](/05_ImplementApprovalFlow.md)

:white_check_mark: We also created a working solution located in the branch [Solution](https://github.com/DevOps-Gilde/Hackathon_PP_ModelDrivenApp_CstPages_Doc/tree/Solution) of your forked repository that covers all tasks. The solution is provided as solution so you have to import it to your environment.
If at any Point you need assistance nevertheless do not hesitate to ask. We are here to Help you.
