# Parabank PVA Ephemeral Deployment

## Description
The following example demonstrates a job that creates an ephemeral Docker container in Azure uploads/deploys/replaces a PVA on the server, and runs a health check step against it  and runs a SOAtestcli to validate it

## User Flow

1.	User checks assets into SCM. Typically this is done via git commit/push/etc or EGit plugin for Eclipse. The user may check in any or all of the following:
	1.	.pva file – virtual asset
	2.	.pvadd file - deployment details if deploy option in step 3 is set to false 
	3.	.pmpdd file – proxy (optional).
2.	Git repositories use webhooks to trigger build/test jobs – i.e. Jenkins, Ado, gitlab, etc
3.	The job will pull a SOAvirt docker container, license it, and deploy the assets in /virt folder.
   	- The job needs to call the soavirt server API to upload the file, with two optional flags: deploy=true or false; replace=true or false.
	- See:  POST /v6/files/upload on the <host>:<port>/soavirt/api REST API page for additional documentation regarding this API call.
4.	After that you run your validation or repeat step 3 for any additional servers.

## Project Structure

```
.
+-- virt
|   +-- Parabank.pva
|   +-- Parabank.pvadd
+-- .gitignore
+-- README.md
+-- azure-pipelines.yaml
``` 

