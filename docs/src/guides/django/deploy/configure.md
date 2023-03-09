---
title: "Configure Django for Platform.sh"
sidebarTitle: "Configure"
weight: -100
description: |
    Review the basics of what makes up a Platform.sh project, including its three principle configuration files and how to define them for Django.
---

{{% guides/config-desc name="Django" %}}

{{% guides/config-app noExample=true /%}}

The examples vary based on using Pip, Pipenv, or Poetry to manage dependencies.

{{< codetabs >}}
+++
title=Pip
highlight=yaml
file=/static/files/fetch/appyaml/pip/django4
+++

<--->
+++
title=Pipenv
highlight=yaml
file=/static/files/fetch/appyaml/pipenv/django4
+++

<--->
+++
title=Poetry
highlight=yaml
file=/static/files/fetch/appyaml/poetry/django4
+++

{{< /codetabs >}}

### How to start your app

Each of these examples includes a command to start your app under `web.commands.start`.
It uses the Gunicorn WSGI server and Unix sockets.

{{< codetabs >}}

+++
title=Pip
+++
```yaml {location=".platform.app.yaml"}
web:
    upstream:
        socket_family: unix
    commands:
        start: "gunicorn -w 4 -b unix:$SOCKET myapp.wsgi:application"
```
<--->
+++
title=Pipenv
+++
```yaml {location=".platform.app.yaml"}
web:
    upstream:
        socket_family: unix
    commands:
        start: "pipenv run gunicorn -w 4 -b unix:$SOCKET myapp.wsgi:application"
```
<--->
+++
title=Poetry
+++
```yaml {location=".platform.app.yaml"}
web:
    upstream:
        socket_family: unix
    commands:
        start: "poetry run gunicorn -w 4 -b unix:$SOCKET myapp.wsgi:application"
```
{{< /codetabs >}}


To use this server, update the command to replace the WSGI application Gunicorn calls.
The example uses a `myapp/wsgi.py` file with a callable `application`.

To use a different web server, change this start command.
For examples of how to do so, see more about [Python web servers](../../../languages/python/server.md).

{{% guides/config-service name="Django" %}}

Below is an example configuration to make [PostgreSQL](../../../add-services/postgresql.md) available for your Django application.

{{< readFile file="static/files/fetch/servicesyaml/django4" highlight="yaml" location=".platform/servicesapp.yaml" >}}

{{% /guides/config-service %}}

{{% guides/config-routes template="django4" name="Django" %}}

{{< guide-buttons next="Customize Django" >}}