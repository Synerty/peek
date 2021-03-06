
.. _admin_configure_synerty_peek:

Configuring Platform :file:`config.json`
----------------------------------------

Update config.json files. This tells the peek platform services how to connect to each
other, connect to the database, which plugins to load, etc.

.. note:: Running the services of Peek will automatically create and fill out
    the missing parts of config.json files with defaults.  So we can start with just what
    we want to fill out.


Peek Server
```````````

This section sets up the config files for the **server** service.

----

Create following file and parent directory:

:Windows: :file:`C:\\Users\\peek\\peek-server.home\\config.json`
:Linux: :file:`/home/peek/peek-server.home/config.json`
:Mac:   :file:`/Users/peek/peek-server.home/config.json`

.. tip:: Run the service, it will create some of it's config before failing
            to connect to the db.

----

Populate the file :file:`config.json` with the
    *   SQLAlchemy connect URL (See options below)
    *   Enabled plugins

Select the right :code:`connectUrl` for your database, ensure you update :code:`PASSWORD`.

:MS Sql Server: :code:`mssql+pymssql://peek:PASSWORD@127.0.0.1/peek`
:PostgreSQL: :code:`postgresql://peek:PASSWORD@127.0.0.1/peek`

::


        {
            "plugin": {
                "enabled": [
                    "peek_plugin_inbox",
                    "peek_plugin_tutorial"
                ]
            },
            "sqlalchemy": {
                "connectUrl": "postgresql://peek:PASSWORD@127.0.0.1/peek"
            }
        }


Peek Client
```````````

This section sets up the config files for the **client** service.

----

Create following file and parent directory:

:Windows: :file:`C:\\Users\\peek\\peek-client.home\\config.json`
:Linux: :file:`/home/peek/peek-client.home/config.json`
:Mac:   :file:`/Users/peek/peek-client.home/config.json`

.. tip:: Run the service, it will create some of it's config,
            it might raise errors though.

----

Populate the file :file:`config.json` with the
    *   Enabled plugins
    *   Disable NativeScript preparing

::

        {
            "frontend": {
                "nativescriptBuildPrepareEnabled": false
            },
            "plugin": {
                "enabled": [
                    "peek_plugin_inbox",
                    "peek_plugin_tutorial"
                ]
            }
        }



Peek Agent
``````````

This section sets up the config files for the **agent** service.

----

Create following file and parent directory:

:Windows: :file:`C:\\Users\\peek\\peek-agent.home\\config.json`
:Linux: :file:`/home/peek/peek-agent.home/config.json`
:Mac:   :file:`/Users/peek/peek-agent.home/config.json`

.. tip:: Run the service, it will create some of it's config,
            it might raise errors though.

----

Populate the file :file:`config.json` with the
    *   Enabled plugins

::

        {
            "plugin": {
                "enabled": [
                    "peek_plugin_inbox",
                    "peek_plugin_tutorial"
                ]
            }
        }

Peek Client & Server SSL
````````````````````````

This section sets up SSL for the peek client and server services.

----

Combine the required SSL certificates and keys into a single PEM file
named :file:`peek-ssl-bundle.pem`.

For example, this can be done on Linux by concatenating the Key, Cert and CA files. ::

    cat key.pem cert.pem ca.pem > bundle.pem

.. note:: The file names will vary, but the file contents will start with lines like the following ::

    ==> CA cert <==
    -----BEGIN CERTIFICATE-----
    
    ==> Cert <==
    -----BEGIN CERTIFICATE-----
    
    ==> Key <==
    -----BEGIN RSA PRIVATE KEY-----



----

Place a copy of this PEM file into the server directory:

:Windows: :file:`C:\\Users\\peek\\peek-server.server\\peek-ssl-bundle.pem`
:Linux: :file:`/home/peek/peek-server.home/peek-ssl-bundle.pem`
:Mac:   :file:`/Users/peek/peek-server.home/peek-ssl-bundle.pem`

----

Restart the Peek server service.

----

Place a copy of this PEM file into the client directory:

:Windows: :file:`C:\\Users\\peek\\peek-client.server\\peek-ssl-bundle.pem`
:Linux: :file:`/home/peek/peek-client.home/peek-ssl-bundle.pem`
:Mac:   :file:`/Users/peek/peek-client.home/peek-ssl-bundle.pem`

----

Restart the Peek client service.

----

The Peek server and client should now be using SSL.
