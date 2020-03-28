## Build Options
Most software components on the internet that can be compiled have different options that can be set at compile time that impacts the behavior of the outputted component. For example many C-libraries let you enable Debugging which produces a binary that correlates execution statements to original lines of code in the binary (at the expensive of bigger slower binaries). 

```
./configure
make debug
```

## Build Flags

## Build Definition

```
requirements:
   - gcc
   - something else
entrypoints:
  ./bin/build.sh :
    arguments :
      os:
        description: The operating system
        type: Enum("linux", "macos")
        required: true
      flags:
        description: Arbitrary key values passed to the autoconf command line.
            examples:  Ingredient(
                          builder:
                             url:  "github.com/ActiveState/builders@somecommit",
                             arguments:
                                env: # 
                                  LD_PATH : foo # is this a replace or an append?
                                toggles:
                                   - enable-database
                                   - enable-ext-colors
                                   - enable-ext-mouse
                                flags:
                                   with-pkg-config-libdir : /usr/lib/pkgconfig # TODO: this should be some relative reference
                                   with-manpage-format : normal
                        )
        type: [KeyValue]
           
```

## Relationship between Ingredients and Builders
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjA5NzA4MzU1LDgxNTY5NTQwNV19
-->
