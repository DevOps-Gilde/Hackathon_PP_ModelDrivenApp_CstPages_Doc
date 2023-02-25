# 1. Introduction to Import Implemented Artefacts

Due to time we cannot create the data model step by step nor can we implement the complete application. We will use instead a transport mechanism to deploy a fully implemented database model and the partially implemented application as starting point. This approach can be used for any artefact that has been created within PowerPlatform. Microsoft calls deployable code packages also `Solutions`. Essentially they boil down to a Zip file that contains the artefacts in an internal Microsoft format that you should always treat as black box.

# 2. Import Implemented Artefacts

Perform the following steps:
1. Download the file `Solution_Hackathon_managed_2_0_0_0.zip` from [our code repo](https://github.com/DevOps-Gilde/Hackathon_PP_ModelDrivenApp_CstPages_Code) 

2. Switch to "Solutions" in the main menu
<br><img src="./images/imp_sol_step_start.png" /><br>

3. Click on "import solution" and select the downloaded file from the repo and click next.
<br><img src="./images/imp_sol_step_imp_sol.png" /><br>

4. Start the import by clicking the button import as shown below
<br><img src="./images/imp_sol_step_conf_imp.png" /><br>

5. Wait until the portal shows at the top the message "Solution successfully imported"
<br><img src="./images/imp_sol_step_succ.png" /><br>

6. Check success by example

   As a result you should see now the custom tables we need for our application that all start with the prefix "IMP" as sown below:
   <br><img src="./images/imp_sol_step_check.png" /><br>
