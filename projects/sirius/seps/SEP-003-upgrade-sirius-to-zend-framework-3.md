# SEP 3 - Upgrade Sirius to Zend framework 3

## Introduction

Our currently used version of Zend framework on backend is 2.3.x, this is an outdated version which is no longer actively maintained or supported. The Sirius system should aim to remain as close to the development cycle of it's core dependencies as possible allowing us to take full advantage of the open source contributions to the framework. Allowing Sirius to fall far behind is simply storing up work which needs to be done as versions of the framework fall out of support.

## Scope

This change predominately affects the Backend API.

Membrane already runs on Zend framework 2.5 which is still supported and we plan to retire the membrane service entirely so there seems less urgency in performing maintenance here

Frontend runs a version further behind, 2.2, however has minimal PHP code and the work to retire membrane will remove some of this. It is also less urgent to upgrade the frontend to the latest version and the effort to do so should be minimal.

## Proposal

The latest version of Zend framework is 3.0.x however there are quite a few changes required to get to this version. Instead we should aim to first upgrade to the 2.4.x version which has long term support whilst taking steps to improve compatibility with Zend framework 3. The next step would be to upgrade to Zend 2.5+ The upgrade to 2.5+ brings in deprecations for functionality removed in Zend 3 and splits the framework into it's constituent parts. This is a huge advantage to us as we can upgrade components one at a time starting with the ones that bring most benefit eg the service manager (this has a huge performance increase in ZF3).