# 1. Introduction to Wizard

You should now have Completed the Following things:

1. Importing database

Next you will implement a page within our application.

# 2. Understanding the application

Our application is centered CO2 consumption data that is uploaded by the userOnce the upload is final it must be approved. An upload is also known as "Import". Two tables hold the data for an import:
* ...RAW_HDR

  One row in this table summarizes the rows that constitute an import. It contains the importinga nd approving details such as user and timestamps. Business rules enforce consistency e.g. an approving user must be stored if the state is approved. One tracks the current state of the import which has the following state model:
  
  * Pending - Import has been done but the figures are not ready for approval
  * Finalized - Figures are ready for approval
  * Approved - Figures habe been approved and can be processed
  * Processed - Figures have been added to the accumated CO2 consumption by the system.

* ...RAW

  Each record in the table denotes a CO2 consumption. Driver refers to the substance that caused the CO2 emission.

First then it appears in the final destination table that holds the accumulated CO2 consumption per year. Therefore our application knows two types of users:
* Users that are eligible for import (all employees that are not part of the COMPLIANCE department)
* Users that are eligible for approval (all employees that are  part of the COMPLIANCE department)

The application addresses the needs of users importing... TODO

# 2. Layouting controls

TODO

# 3. Form control (Edit Mode)

TODO

# 4. Navigation

TODO
