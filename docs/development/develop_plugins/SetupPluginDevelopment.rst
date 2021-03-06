.. _setup_plugin_for_development:

============================
Setup Plugin for Development
============================

Plugins need to be installed as python packages for the Peek Platform to run them.
This is typically done with a command similar to :command:`pip install peek-plugin-noop`.

Python packages can be installed in "development" mode, where your code being developed
is only linked into the python environment.

.. note:: For developing an existing plugin ensure there are no installed releases
   :code:`pip uninstall peek-plugin-example`.  Confirm installed peek packages with
   :code:`pip freeze | grep peek`.

This is achived with the following command in the plugin project root directory, where
setup.py is: ::

        # Check to ensure we're using the right python
        which python

        python setup.py develop


----

Configure Peek Services
```````````````````````

The python peek services, **worker**, **agent**, **client** and **server** need to have
the plugin enabled in their :file:`~/peek-{service}/config.json`.

For example: ::

        "plugin": {
            "enabled": [
                "peek_plugin_example"
            ]
        }

----

Run the Plugin
``````````````

Now that the plugin has been setup for development and the platform has been configured
to run it, running the platform will run the plugin.

See the Setup IDE procedures to run the platform and debug plugins under those.

If a platform service, (:command:`run_peek_server` for example) is run under the IDEs
debugger, it will also debug the plugins the platform loads.

Run the platform services from bash with the following commands: ::

        # Check to ensure we're using the right python
        which python

        # Run the peek server
        run_peek_server

        # Run the peek client
        run_peek_client

        # Run the peek agent
        run_peek_agent

        # Run the peek worker
        run_peek_worker


