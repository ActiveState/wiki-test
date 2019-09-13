# User Guide. Adding a Python Package
1. [Prerequisites](#prerequisites)
2. [Provide OpenJDK language definition](#provide-openjdk-language-definition)
3. [Provide OpenJDK Builder image definition](#provide-openjdk-builder-image-definition)

## Prerequisites
* Install ActiveState State Tool
* Create a folder for your work `mkdir ~/openjdk-submission`

## Provide OpenJDK language definition
* Use `~/opendjk-submission/state create` and follow the guide
	* `name: OpenJDK` 
	* `ingredient type Language(L) | Package(P) | Image(I): Language`
	* `availability (public | private): public`
* Use template generated `subl ~/openjdk-submission/openjdk/activestate-descriptor.yaml`
* Submit OpenJDK definition to platform `~/openjdk-submission/state add openjdk`. The command will fail as we are missing the OpenJDK build tools