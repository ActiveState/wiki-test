# Chapter 1: Adding your first ingredient

In order to add a new ingredient, it's easiest to use the state tool to create a template
ingredient file which you can add detail to.  We'll create an ingredient for the python module `pyeq2`. Run
```
state ingredient new pyeq2 --version 12.2.9 --namespace language/python
```
This will create a `pyeq2` directory under your current working directory with a single
template file `pyeq2.graphql` in it.  Th file will look like this:
```graphql
mutation Inggredient (
  name:              "pyeq2"           # name of the ingredient
  primary_namespace: "language/python" # the namespace the ingredient should belong to
  description:                         # a short description of the ingredient
  website:                             # the ingredient's website, if it has one
  versions: [
    {
       version:           "12.2.9"                      # the raw version of the ingredient
       is_stable_release: true                          # true if this release is stable, 
                                                        #   false otherwise

       copyright_text:                                  # the body of the license, optional
       release_timestamp: "1970-01-01T00:00:00.000000Z" # date/time of release
       documentation_uri:                               # URI of the documentation for this
                                                        #   version, if known 

       source_uri:                                      # URI to the source code as a zip 
                                                        #   file or tarball

       authors: [
                                                        # a list of the authors, by name, 
                                                        #   optional
       ]
       build_rule: {
         platform: []                                   # a list of platform features required 
                                                        #   for this toolchain to be selected

         toolchain:                                     # URI to a toolchain implementation
       }
       provided_features: [
         feature: "pyeq2"                               # name of the feature this version 
                                                        #   provides, usually the ingredient
                                                        #   name

         version: "12.2.9"                              # version of the feature provided
         is_default_provider: true                      # false if this is an alternative 
                                                        #   provider for a feature

         namespace: "language/python"                   # namespace of the feature, usually 
                                                        #   the same as the namespace of the 
                                                        #   ingredient
       ]
       dependency_sets: [
         dependencies: [
           {
             conditions:                                # conditions required for this 
                                                        #   dependency to apply, usually null

             feature:                                   # name of the feature we depend on, 
                                                        #   e.g. another ingredient, build 
                                                        #   tool etc.

             namespace:                                 # namespace of the feature, e.g. 
                                                        #   'language', 'image'
             requirements: {
               comparator:                              # how we should compare versions, 
                                                        #   e.g. 'gte', 'eq', 'lte'

               version:                                 # the version of the feature we require
             }
           }
         ]
         description: # description of the dependency
         original_requirement: null
         type: # type of this dependency, e.g. 'build', 'runtime', 'test'
       ]
     }
  ]
)
```
