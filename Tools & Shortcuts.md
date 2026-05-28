# Keyboard SHORTCUTS

**Desktop**
1. Windows+V = open clipboard
2. Clt+O = opens a document from folder
3. Alt+Tab = switch between open application
4. Win+Up/Down = minimize/maximize a window

**Browser**
1. Clt+N = opens a new window
2. Clt+Sht+N = new incognito window
3. Clt+T = opens a new tab
4. Clt+W = close current tab
5. Alt+F4 = close current application
6. Only F5 = refresh webpage
7. Clt+D = bookmark current webpage
8. Clt+L = highlights address bar

**Basic**
1. Clt+0 = resets zoom to 100%
2. Clt+'-' = zoom out
3. Clt+'+' = zoom in
4. Clt+X = cut
5. Clt+C = copy
6. Clt+V = paste
7. Clt+P = print
8. Clt+A = select all
9. Clt+S = save
10. Clt+Z = undo
11. Clt+Y = redo
12. Clt+F = find next

---

# VS Code

**VS code setup**
1. Download x64 file from code.visualstudio.com
2. Download python extension from extensions.
3. Install and then select python interpreter from vs code.

**Shortcuts**
1. code . = opens vs code from folder in the current path
2. cmd = opens cmd from folder in the current path
3. Clt+/ = comments a line or section
4. Clt+B = opens/closes  left side bar

**Python**
1. Use text[::-1] for reversing a string.
2. Use """text""" or '''text''' for multiline string.
3. Use Clt+C to stop terminal processes.
4. Use Tab twice in the terminal to show autocomplete.
5. Binary - [1.10.11.100] [101.110.111.1000]
6. Binary AND, OR, XOR:

| A | B | AND | OR | XOR |
| - | - | --- | ---| --- |
| 0 | 0 |  0  |  0 |  0  |
| 0 | 1 |  0  |  1 |  1  |
| 1 | 0 |  0  |  1 |  1  |
| 1 | 1 |  1  |  1 |  0  |

7. Tutorials: https://wiki.python.org/moin/BeginnersGuide/Programmers
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
Other useful packages - djangorestframework, etc.

**Install required packages from `requirements.txt` file**
```bash
pip install -r requirements.txt
```

**Create Django project & apps**
```bash
django-admin startproject core .
python manage.py startapp main
```

### Test Project on Local Network
To make your Django project accessible from all devices on your local network (via your router), you need to run the server on your machine’s local IP address.

**Step-1** Find your local IP address (IPv4 Address): e.g. 192.168.x.x
```bash
ipconfig
```
**Step-2** Run Django on that IP:
```bash
python manage.py runserver 192.168.x.x:8000
```
**Step-3** You may need to add '192.168.x.x' to ALLOWED_HOSTS in settings.py
```python
ALLOWED_HOSTS = ['192.168.x.x']
```