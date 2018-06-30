---
url: https://youtu.be/S-Le3PWHqZA
---

# Making sense of setup.py

Some loose but suficient definitions:
- a `package` is a folder that contains a `__init__.py` file
- a `module` is a file with the `py` extension
- a `distribution` is purely organisational, it can require, provide and/or obsolete packages and modules.

`setup.py` is a regular python file describing your package:
- name, author, website
- version (uses semantic versioning)
- modules
- entry points
- additional data files
- license and searh keywords
- compatible versions of python

Used as `python setup.py <COMMAND>`.

Install a package with `install` or `develop` commands. The former copies your module into the system folder, while the latter create a symlink, meaning that any changes you do to the package is reflected immediately.

Use the `register` command to claim a name on `PyPi`. Nothing will be available until you upload the actuall package with the `upload` command. Packages can be signed with GPG. Consider using `twine` which does SSL verification.