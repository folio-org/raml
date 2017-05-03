# raml

Copyright (C) 2017 The Open Library Foundation

This software is distributed under the terms of the Apache License,
Version 2.0. See the file "[LICENSE](LICENSE)" for more information.

## Introduction

Repository of RAML traits and resource type files.

This repository contains traits and resource types that can be re-used
by other projects to limit duplication. It is utilized as a git submodule
in each such repository as its "raml-util" directory.

Trait examples:

 - Authorization
 - Language
 - Pagination
 - etc.

Resource types:

 - Get, Post, Delete, Put, File upload, etc.

This is the master location for the traits and resource types, while each module is the master for its own schemas, examples, and actual RAML files.

## Additional information

The [raml-module-builder](https://github.com/folio-org/raml-module-builder) framework.

Other [modules](http://dev.folio.org/source-code/#server-side).

[API reference documentation](http://dev.folio.org/doc/#api-reference).

See project [RMB](https://issues.folio.org/browse/RMB)
at the [FOLIO issue tracker](http://dev.folio.org/community/guide-issues).

Other FOLIO Developer documentation is at [dev.folio.org](http://dev.folio.org/)
