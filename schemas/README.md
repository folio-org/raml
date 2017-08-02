When any schema file refers to an additional schema file, then also use that pathname of the referenced second schema as the "key" name in the RAML "schemas" section, and wherever that schema is utilised in RAML files.

Ideally ensure that all such referenced files are below the parent file.
It is possible to use a relative path with one set of dot-dots "../" but definitely
[not more](https://issues.folio.org/browse/RMB-30).
This is why it is beneficial to place the "raml-util" git submodule inside the "ramls" directory.
