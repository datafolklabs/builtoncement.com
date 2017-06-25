---
title: What's New
type: guide
version: "2.10"
order: 2
---

## Support for Multiple File Plugin Directories

Prior to Cement 2.10, application plugins were only supported as single files such as `myplugin.py`.  Plugins can now be a single file, or full python  modules like `myplugin/__init__.py`.

An example plugin might look like:

```
myplugin/
    __init__.py
    controllers.py
    templates/
        cmd1.mustache
        cmd2.mustache
        cmd3.mustache
```

The only thing required in a plugin is that it supply a `load()` function either in a `myplugin.py` or `myplugin/__init__.py`.  The rest is up to the developer.

See [Application Plugins](/2.10/dev/application_plugins) for more information.

Related:

- Issue 350


## Cross Platform Filesystem Event Monitoring via Watchdog

Applications can now monitor, and react to, filesystem events with a very easy wrapper around the `Watchdog <https://pypi.python.org/pypi/watchdog>`_ library.  The extension makes it possible to add a list of directories to monitor, and link them with the class to handle any events while automating the proper setup, and teardown of the backend observer.

The Watchdog Extension will make it possible in future releases to properly handle reloading a running application any time configuration files are modified (partially implemented by the `reload_config` extension that has limitations and does not support reloading the app).  Another common use case is the ability to reload a long running process any time source files are modified which will be useful for development when working on daemon-like apps so that the developer doesn't need to stop/start everytime changes are made.

See the [Watchdog Extension](/2.10/api/cement.ext.ext_watchdog) for more information.

Related:

- Issue 326
- Issue 394


## Ability To Pass Meta Defaults From `CementApp.Meta` Down To Handlers

Cement handlers are often referenced by their label, and not passed as pre-instantiated objects which requires the framework to instantiate them dynamically with no keyword arguments.

For example:

```python
from cement.core.foundation import CementApp

class MyApp(CementApp):
    class Meta:
        label = 'myapp'
        extensions = ['json']
```

In the above, Cement will load the `json` extension, which registers `JsonOutputHandler`.  When it comes time to recall that handler, it is looked up as `output.json` where `output` is the handler type (interface) and `json` is the handler label.  The class is then instantiated without any arguments or keyword arguments before use.  If a developer needed to override any meta options in `JsonOutputHandler.Meta` they would **previously** have had to sub-class it.  Consider the following example, where we sub-class `JsonOutputHandler` in order to override `JsonOutputHandler.Meta.json_module`:

```python
from cement.core.foundation import CementApp
from cement.ext.ext_json import JsonOutputHandler

class MyJsonOutputHandler(JsonOutputHandler):
    class Meta:
        json_module = 'ujson'

def override_json_output_handler(app):
    app.handler.register(MyJsonOutputHandler, force=True)

class MyApp(CementApp):
    class Meta:
        label = 'myapp'
        extensions = ['json']
        hooks = [
            ('post_setup', override_json_output_handler)
        ]
```

If there were anything else in the `JsonOutputHandler` that the developer needed to subclass, this would be fine.  However the purpose of the above is soley to override `JsonOutputHandler.Meta.json_module`, which is tedious.

As of Cement 2.10, the above can be accomplished more-easily by the following by way of `CementApp.Meta.meta_defaults` (similar to how `config_defaults` are handled:

```python
from cement.core.foundation import CementApp
from cement.utils.misc import init_defaults

META = init_defaults('output.json')
META['output.json']['json_module'] = 'ujson'

class MyApp(CementApp):
    class Meta:
        label = 'myapp'
        extensions = ['json']
        output_handler = 'json'
        meta_defaults = META
```

When `JsonOutputHandler` is instantiated, the defaults from `META['output.json']` will be passed as `**kwargs` (overriding builtin meta options).

Related:

- Issue 395


## Additional Extensions

- [Jinja2](/2.10/api/cement.ext.ext_jinja2) - Provides template based output handling using the Jinja2 templating language
- [Redis](/2.10/api/cement.ext.ext_redis) - Provides caching support using  Redis backend
- [Watchdog](/2.10/api/cement.ext.ext_watchdog) - Provides cross-platform filesystem event monitoring using the Watchdog library.
- [Handlebars](/2.10/api/cement.ext.ext_handlebars) - Provides template based output handling using the Handlebars templating language

