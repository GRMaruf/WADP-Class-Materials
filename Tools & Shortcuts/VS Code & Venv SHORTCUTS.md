# VS Code & Virtual Environment SETUP

**VS code setup**
- Download x64 file from code.visualstudio.com
- Download python extension from extensions.
- Install and then select python interpreter from vs code.

**Shortcuts**
- `code .` = opens vs code from folder/terminal in the current path
- `cmd` = opens cmd from folder in the current path
- `Clt+/` = comments a line or section
- `Clt+B` = opens/closes left side bar
- `Clt+Alt+B` = opens/closes right side bar

**Python**
- Tutorials: https://wiki.python.org/moin/BeginnersGuide/Programmers
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

**Create & activate virtual environment**
```bash
python -m venv .venv
call .venv\Scripts\activate.bat
```

```bash
pip install django whitenoise[brotli] pillow
```

```bash
pip install -r requirements.txt
```

```bash
django-admin startproject core .
python manage.py startapp main
```

## Testing Project on Local Network
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