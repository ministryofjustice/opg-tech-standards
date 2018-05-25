# SEP 7 - Replace timeline events system

## Introduction

The timeline system in Sirius acts as an audit trail of chances made to several of the core domain entities, the current code which powers this is not really fit for purpose. It is built by hooking into the Doctrine ORM event system, this allows it to take action whenever an entity is saved or updated into the database, it uses this to check for changed fields and log timeline events as required. This is unfortunately very slow, up to two thirds of a requests processing time can be spent logging these events, further more it is not adequately covered by the automated test suites: commenting out the code which handles these events causes the unit tests to run much faster but crucially none of them fail.

There have been two proposed solutions to this, both are detailed here the selected solution will also be indicated.

## Proposal 1 (Dave Nash)

Dave has suggested that instead of using doctrine's event manager we use the Zend event manager, work towards this has started but is far from complete. Inside the V1 API each service dispatches events when it makes changes to domain entities. Once most of the code base has been migrated to V1 the plan is to add listeners to these events to build up the audit log in the same way as the Doctrine event listener currently does. This will prove to be more performant than the existing solution but will require component or integration tests to ensure adequate automated test coverage.

## Proposal 2 (Chris Riley)

My suggestion is that each domain entity shall be responsible for managing it's own timeline - that is at any point that you call a method on an object which changes it's internal state, it can make a determination as to weather it is an interaction which requires a timeline event to be created and if so, create one. This ensures that any code which changes an entity - not just a service will cause the timeline to be correctly created and since all the logic is in one place, can be unit tested easily. It also keeps all the core business logic in one place and saves developers from having to know that there are event listeners which cause side effects to happen when they are calling into a service method.

To get towards this solution, we ideally also need to stop updating entities using setters + getters and instead move towards interaction specific methods which update multiple fields at once. This makes it easier for an entity to decide if/which timeline event data needs to be stored. This is also closer to a true event sourcing model (It is not event sourcing, as our entities won't rely on the timeline events to reconstruct their own internal state)