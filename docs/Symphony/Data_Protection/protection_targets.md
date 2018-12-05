# Protection Targets

## Overview

The Protection Target is the actual physical cluster and storage pool, where the protected data will be stored.

By definition, this cluster is not the same cluster as that where the source data is located..

All Protection Target actions are performed by the Protection Manager of the Target site.

# Creating a Protection Target

**Note**: Before creating a Protection Target, verify that the Virtual IP for the Data Protection Connection has already been configured.

**To create a Protection Target**:

1. Click  **Data Protection**  >  **Protection Targets**  >  **Create****.**

The  **Create Protection Target**  dialog box appears.

2. Enter the following information:

**Name**  – enter a unique name for the Protection Target.

**Account**  - select a target account from the drop-down list.

**User**  - select a user from the drop-down list. Only users of the selected tenant with the role of Admin or Protection Manager can be selected.

**Project**  - select a project from the drop-down list.

**Storage Pool**  - select the storage pool targeted for protection.

3. Click  **OK**  to create the new protection target.

The new protection target appears in the list of protection targets, and a "Target created" message pops-up in the upper right-hand corner.

4. Click  **Send e-mail**  in the "Target created" message.

An e-mail form pops up with the Subject: "Target Details" and the following target credentials:

URL

Target Name

Account Name

Project Name

Username (of Protection Manager for this target)

Target ID

**Note**: The e-mail form pops-up only if the "Mailto" function of your browser has been configured with some e-mail client or service.

Send this e-mail to the Protection Manager of the Source cluster.

# Deleting a Protection Target

To delete a Protection Target:

1. Click  **Data Protection**  >  **Protection Targets**  > name of the protection target you want to delete >  **Delete**.

The Delete Target confirmation message appears.

2. Click  **OK**. The system deletes the target.


