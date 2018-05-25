# SEP 4 - Remove forked version of JMS serialiser

## Introduction

Sirius currently relies on a fork of a common PHP library: JMS serialiser. A fork was created to add a new "generic accessor" annotation, this feature allows a generic method to be defined to serialize a property allowing the reuse of serialisation logic between different classes and properties. Unfortunately this fork is months behind the main line and given that the feature is unlikely to be accepted into the mainline, we have no path to get back onto the supported version. This adds a maintenance overhead for this library onto the Sirius team to support this forked version for the lifetime of the system.

## Proposal

There is a documented way in the existing library to achieve code reuse of the kind the generic accessor feature tries to provide: JMS serialiser allows custom handlers to be defined for serialising fields (see http://jmsyst.com/libs/serializer/master/handlers) the example in the documentation even covers our main use case for generic accessors: date/time fields.

We should implement a custom handler for each of the generic accessors and replace the annotation with the correct annotations for the custom handlers. This would allow dropping the generic accessor annotation and by extension our dependence on the fork.