# Packaging

We provide several Packagers that will take Artifacts out of the Build Graph and convert them to a format that
you can use natively. Packagers have an number of common required arguments and fields in common. These
describe the Artifacts that the packager needs.

## Commonn



```graphql

query {
   ; packager using atTime/requirements
   packager(atTime=1234, platform="II-X") {
      fields...
   }
   
   ; packager referencing an order
   packager(commitId = "AA7-IXX...") {
      fields...
   }

}
```

### Common arguments
In addition to packager specific arguments all packager's require one of more of the following attributes.


  | Argument             | Descrption                                                                 |
  |----------------------|----------------------------------------------------------------------------|
  | **atTime**           | Mandatory, only changes to graph at or before this time will be considered |
  | **requirments**      |  List of requriments and constraints. Either  `requirments` can be specified or `orderId` but not both. |
  | **order**            | A Url to an order which contains the timestamp and requirments. Either an order can be specified or you must use `requirments` and `atTime` but not both. |
  | **platform**         | Id of a platform which represents an operating system, hardware arcihtecture|

### Common Fields

| Field                | Descrption                                                                 |
|----------------------|----------------------------------------------------------------------------|
| **timestamp**        | Timestamp needed to reproduce this package exatly |
|----------------------|----------------------------------------------------------------------------|
| **requirments**      |  List of requriments and constraints. Either  `requirments` can be         |
|                      |  specified or `orderId` but not both                                       |
|----------------------|----------------------------------------------------------------------------|
| **order**            | A Url to an order which contains the timestamp and requirments. Either an  |
|                      | order can be specified or you must use `requirments` and `atTime` but not  |
|                      | both.                                                                      |

## Artifacts

You've already been introduced to the  fundamental  packager query `artifacts` it can retrive the artifacts from one or more ingredients
start building them if they haven't been built otherwise returning the results.

## Docker

Is a packager that will take an artifact from the Build Graph and package it's content into a docker image that can be deployed to a repository somewhere.

## Legacy Installer

You've already been introduced to the  fundamental  packager query `artifacts` it can retrive the artifacts from one or more ingredients
start building them if they haven't been built otherwise returning the results.


## Python Wheels

This will package all python requirments into a list of wheels. Note it is an error to specify requirments that are not Python. We'll have to figure out how to distinguisg system libraries
from python packages. Will we do this by namespace? Or do we let you build anything and ship you the wheel we find? 