---
title: Introduction
type: guide
version: "portland"
order: 2
---


<p class="tip-warn">
Portland is a complete fork of Cement 2, and will eventually become Cement 3. It is guaranteed to be broken! Please use Cement 2 in production until stable/3.0.0 is released.
</p>


## What is Cement?

Cement is an advanced Application Framework for Python, with a primary focus on Command Line Interfaces (CLI).  Its goal is to introduce a standard, and feature-full platform for both simple and complex command line applications as well as support rapid development needs without sacrificing quality.  Cement is flexible, and it's use cases span from the simplicity of a micro-framework to the complexity of a mega-framework. Whether it's a single file script, or a multi-tier application, Cement is the foundation you've been looking for.

The first commit to Git was on Dec 4, 2009.  Since then, the framework has seen several iterations in design, and has continued to grow and improve since it's inception.  Cement is the most stable, and complete framework for command line and backend application development.

## Core Features

Cement core features include (but are not limited to):

- Core pieces of the framework are customizable via handlers/interfaces
- Handler system connects implementation classes with Interfaces
- Extension handler interface to easily extend framework functionality
- Config handler supports parsing multiple config files into one config
- Argument handler parses command line arguments and merges with config
- Log handler supports console and file logging
- Plugin handler provides an interface to easily extend your application
- Output handler interface renders return dictionaries to console
- Cache handler interface adds caching support for improved performance
- Controller handler supports sub-commands, and nested controllers
- Hook support adds a bit of magic to apps and also ties into framework
- Zero external dependencies* (not including optional extensions)
- 100% test coverage using `pytest` and `coverage`
- 100% PEP8 and style compliant using `flake8`
- Extensive Developer Guide and API Reference Documentation
- Tested on Python 3.5+
- Does not support Python 2.x

<p class="tip-warn">Some optional extensions that are shipped with the mainline Cement sources do require external dependencies.  It is the responsibility of the application developer to include these dependencies along with their application, as Cement explicitly does not include them.</p>

## License

The Cement Framework is Open Source and is distributed under the BSD License (three clause).

```
Copyright (c) 2009-2017 Data Folk Labs, LLC
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

    * Redistributions of source code must retain the above copyright notice,
      this list of conditions and the following disclaimer.
    * Redistributions in binary form must reproduce the above copyright
      notice, this list of conditions and the following disclaimer in the
      documentation and/or other materials provided with the distribution.
    * Neither the name of Data Folk Labs, LLC. nor the names of its
      contributors may be used to endorse or promote products derived from
      this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```
