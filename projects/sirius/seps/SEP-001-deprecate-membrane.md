# SEP 1 - Deprecate Membrane

## Introduction

Membrane is an authentication layer which sits between the frontend and backend api which manages users. It was introduced in a hurry to replace an MOJ system which had been discontinued. It causes an additional network hop in every communication between the Sirius app and the API and causes additional infrastructure complexity supporting a separate web service and database. This SEP proposes to remove membrane entirely and move it's user management functionality into the backend API. 

## Proposal

An initial piece of work has been carried out to introduce JWT tokens to the authentication layer, this means that the backend is secure in it's own right, without requiring membrane to intercept all traffic going to backend to ensure that a user is authenticated.

The next step to deprecate membrane is to remove the requirement for frontend to jump through it for every request. Instead frontend will acquire a JWT token from membrane and then use this to make requests directly to the backend, removing the network hop for most requests.

In order to fully deprecate the service and retire it, the functionality it provides for users needs to be merged into backend, backend already tracks some user information for their profile and roles/permissions so this work would be to extend the user functionality to include login and password reset. We will also need to come up with a migration strategy to move existing users into backend once the changes are deployed to live.