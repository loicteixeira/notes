---
videos:
- https://youtu.be/y_vwvqgRZK0
---

# Warpdrive, making Python web application deployment magically easy

Warpdrive provides the scripts for implementing a build and deployment system for Python web applications using Docker.

A few commands run multiple things:

- `warpdrive project` will create the virtual environment, etc
- `warpdrive setup` will run `pip install`, `migrate`, etc
- `warpdrive build` will run `collectstatic`, etc
- `warpdrive start` will bootstrap `apache` with `mod-uwsgi`, etc

Steps can be customised with hooks (`pre-build`, `build`, `deploy`, `setup`, `migrate`, `verify`, `alive`, etc).

You're essentially running your app in production (there aren't really environment anymore).

The watcher only watch "final" files, which means that for the static, it watches the output from the `collecstatic` and won't pick up the changes to your source files, forcing you to run the `build` command again.