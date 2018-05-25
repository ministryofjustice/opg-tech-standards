# SEP 5 - Remove Zend rest module

## Introduction

The new V1 API makes use of a third party library, Zend rest module, to provide request parsing and response formatting for the API. In the past it also provided error handling, however we have begun to replace that with a different implementation. The module in question is currently a fork maintained by us to fix a bug in the upstream library, which has had a pull request outstanding for nearly a year. This and the low number of installs (https://packagist.org/packages/aeris/zend-rest-module) suggests that the original module is unmaintained and thus presents a risk to the project of having to maintain a fork indefinitely. This SEP proposes removing this module and moving to handling the view and input layers ourselves, leveraging components from Apigility wherever possible.
