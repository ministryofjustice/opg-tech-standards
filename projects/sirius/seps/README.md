# Sirius Enhancement Proposals (SEPs)

This page tree exists to record Sirius Enhancement Proposals: technical projects to improve the health of the code base or deliver non-functional improvements.

JIRA issues related to a SEP should be labelled with the SEP number eg SEP-1 to allow a list of JIRA issues to be presented on the SEP page.

## SEP formatting guide

An SEP should consist of the following sections:

### Introduction

A brief introduction to the problem and it's impact on Sirius users, developers or general project health. You could also include a short description of the solution, where appropriate. 

### Proposal

A detailed description of how the SEP will resolve the issue(s) highlighted previously. If you do not yet know what the solution might be, the proposal should be a description of how you intend to find a solution (a spike)

### Benefits

A short list of the benefits to the Sirius project of performing this work; could be Performance, Availability, high dev velocity etc.

### Scope (optional)

This section is used to describe the scope of the change eg it could be limited to just the backend even though the change could equally be applied to other areas. Explain the reasoning for limiting the scope.

### List of JIRA issues

Once there are any JIRA issues relating to your SEP, include a section which lists them all using the confluence macro. To make this easier you can add a label to all the issues in JIRA with your SEP number eg sep-3 and create a filter based on this label.

## SEP Workflow

An SEP goes through the following stages:

### Draft

An SEP is in Draft status until the primary editor(s) are finished writing up the initial version of the SEP. A proposal in draft status can be either moved into the Abandoned state or the Under consideration state.

### Under Consideration

In this stage an SEP will be reviewed by stakeholders and questions raised. The main goal of this phase is to decide if this is something worth doing and if the proposed solution solves the problem adequately. Prioritisation and estimation shouldn't feature heavily in these discussions, they should be focused on the technical outcomes. From here an SEP can move back to draft (if further work is required to address concerns), to Accepted (if it is agreed that the problem is worth solving and the solution will work) or to Declined (if the proposal simply isn't worthwhile or has serious flaws which can't be addressed)

### Accepted

In this stage there should be work done to produce tickets in JIRA for the implementation along with estimates. Once this has been done, the tech council can discuss prioritisation upon weighing up the cost/benefits and risks of carrying out the proposal.

### In progress

Once prioritisation has been agreed and the work has been assigned into sprints, the SEP moves into in progress. It will remain in progress until all the tasks related to it are completed.

### Completed

An SEP can be moved into the completed state and archived once all work on it is completed

### Abandoned

An SEP can be moved into abandoned from the draft state if work on it stops. If someone wishes to pick it up again, it can be moved back into the draft state.

## Currently active SEP's
1	SEP 1 - Deprecate Membrane	Draft
2	SEP 2 - Upgrade Sirius to PHP 7	
Completed

3	SEP 3 - Upgrade Sirius to Zend framework 3	Draft
4	SEP 4 - Remove forked version of JMS serialiser	Draft
5	SEP 5 - Remove Zend rest module	Draft
6	SEP 6 - Improve API error reporting + validation	Draft
7	SEP 7 - Replace timeline events system	Draft

| SEP | Status |
|:-------------:|:-------------:|
| 1   | Draft |
| 2   | Completed |
| 3   | Draft |