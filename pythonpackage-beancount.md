# User Guide. Adding a Python Package

## Prerequisites
* Install ActiveState State Tool
* Create a folder for your work `mkdir ~/beancount-submission`

## Provide Package definition
* Use `~/beancount-submission/state create` and follow the guide
	* `name: beancount` 
	* `ingredient type Language(L) | Package(P) | Image(I): Package`
	* `availability (public | private): public`
* Use template generated `subl ~/beancount-submission/beancount/activestate-descriptor.yaml`

* Fill in the template
```yaml
name: beancount
primary_namespace: language/python
description: A double-entry accounting system that uses text files as input.
website: http://furius.ca/beancount
versions:
- version: 2.2.3
  authors:
  - Martin Blais
  copyright_text:
  "
                      GNU GENERAL PUBLIC LICENSE
                       Version 2, June 1991

    Copyright (C) 1989, 1991 Free Software Foundation, Inc.,
    51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA
    Everyone is permitted to copy and distribute verbatim copies
    of this license document, but changing it is not allowed.

                            Preamble
   ..."
                            
  release_timestamp: '2019-08-22T00:00:00.000000Z'
  documentation_uri: http://furius.ca/beancount/doc/index
  is_binary_only: false
  source_uri: https://files.pythonhosted.org/packages/69/ea/ddf75e1e88aaba807bea3ac101b0e226ddc60832ecfe83ad05cc3a8fff4a/beancount-2.2.3.tar.gz
  build_rule:
    - platform: [] # a list of platform features required for this toolchain
      toolchain: pip_builder
  is_stable_release: true
  provided_features:
  - feature: beancount
    version: 2.2.3
    is_default_provider: true
    namespace: language/python
  dependency_sets:
  - dependencies:
    - conditions: null
      feature: # name of the feature we depend on, e.g. another ingredient, build tool etc.
      namespace: # namespace of the feature, e.g. 'language', 'image'
      requirements:
      - comparator: # how we should compare versions, e.g. 'gte', 'eq', 'lte'
        version: # the version of the feature we require
    description: # description of the dependency
    original_requirement: null
    type: # type of this dependency, e.g. 'build', 'runtime', 'test'

```
* Submit definition to platform `~/beancount-submission/state add beancount`