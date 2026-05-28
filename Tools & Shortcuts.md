# Keyboard SHORTCUTS

**Desktop**
- `Windows+V` = open clipboard
- `Clt+O` = opens a document from folder
- `Alt+Tab` = switch between open application
- `Win+Up/Down` = minimize/maximize a window

**Browser**
- `Clt+N` = opens a new window
- `Clt+Sht+N` = new incognito window
- `Clt+T` = opens a new tab
- `Clt+W` = close current tab
- `Alt+F4` = close current application
- `Only F5` = refresh webpage
- `Clt+D` = bookmark current webpage
- `Clt+L` = highlights address bar

**Basic**
- `Clt+0` = resets zoom to 100%
- `Clt+'-'` = zoom out
- `Clt+'+'` = zoom in
- `Clt+X` = cut
- `Clt+C` = copy
- `Clt+V` = paste
- `Clt+P` = print
- `Clt+A` = select all
- `Clt+S` = save
- `Clt+Z` = undo
- `Clt+Y` = redo
- `Clt+F` = find next

---

# Terminal

- `mkdir [folder_name]` to create into a directory
- `cd [folder_name]` to move into a directory
- `cd ..` to move out from a directory
- `dir` to display files and folder of current directory
- `ren [old_name] [new_name]` to rename a file/directory
- `del [file/folder]` to delete a file/directory
- `Clt+C` to stop terminal process

---

# VS Code

**VS code setup**
- Download x64 file from code.visualstudio.com
- Download python extension from extensions.
- Install and then select python interpreter from vs code.

**Shortcuts**
- `code .` = opens vs code from folder in the current path
- `cmd` = opens cmd from folder in the current path
- `Clt+/` = comments a line or section
- `Clt+B` = opens/closes  left side bar

**Python**
- Use text[::-1] for reversing a string.
- Use """text""" or '''text''' for multiline string.
- Use Clt+C to stop terminal processes.
- Use Tab twice in the terminal to show autocomplete.
- Binary - [1.10.11.100] [101.110.111.1000]
- Binary AND, OR, XOR:

| A | B | AND | OR | XOR |
| - | - | --- | ---| --- |
| 0 | 0 |  0  |  0 |  0  |
| 0 | 1 |  0  |  1 |  1  |
| 1 | 0 |  0  |  1 |  1  |
| 1 | 1 |  1  |  1 |  0  |

- Tutorials: https://wiki.python.org/moin/BeginnersGuide/Programmers
---

# Django Project

**Create & activate virtual environment**
```bash
python -m venv .venv
call .venv\Scripts\activate.bat
```

**Install basic packages**
```bash
pip install django whitenoise[brotli] pillow
```

**Install required packages from `requirements.txt` file**
```bash
pip install -r requirements.txt
```

**Create Django project & apps**
```bash
django-admin startproject core .
python manage.py startapp main
```

## Test Project on Local Network
To make your Django project accessible from all devices on your local network (via your router), you need to run the server on your machine’s local IP address.

- **Step-1** Find your local IP address (IPv4 Address): e.g. 192.168.x.x
```bash
ipconfig
```
- **Step-2** Run Django on that IP:
```bash
python manage.py runserver 192.168.x.x:8000
```
- **Step-3** You may need to add '192.168.x.x' to ALLOWED_HOSTS in settings.py
```python
ALLOWED_HOSTS = ['192.168.x.x']
```