# Nativize

**Code-first app builder** — write HTML/CSS/JavaScript (and more), then export to **Web**, **Windows EXE + Setup**, or **Android**.

![version](https://img.shields.io/badge/version-0.2-blue)
![python](https://img.shields.io/badge/python-3.12%2B-yellow)
![platform](https://img.shields.io/badge/export-Web%20%7C%20Windows%20%7C%20Android-lightgrey)
![license](https://img.shields.io/badge/license-MIT-green)

---

## What is Nativize?

Nativize is a desktop editor focused on **real code and real packaging** — not a PowerPoint-style canvas.

| You write | You export |
|-----------|------------|
| HTML, CSS, JS, JSON, … | **Web** folder for hosting |
| Multi-file project tree | **Windows `.exe`** (desktop window) |
| Optional other sources in the tree | **Setup installer** for your domain |
| | **Android** WebView project → APK in Android Studio |

Ideal when you already think in the web stack and want a simple path to a downloadable Windows app or a mobile shell.

---

## Features

- Multi-file code editor with folders (`css/`, `js/`, `assets/`, …)
- Project save/load (`.miapp` + `project.json`)
- Browser **Preview**
- Full **export dialog**: app name, exe name, window title, version, author, company, description, license, copyright, icon, package ID
- **Web** export + `package.json`
- **EXE** export with `run_app.py`, `COMPILAR.bat`, `www/` bundle
- **Setup** scripts for [Inno Setup](https://jrsoftware.org/isinfo.php) (`setup.iss`, `CREAR_SETUP.bat`)
- **Android** Gradle/WebView project export
- Basic syntax highlighting by file type

---

## Quick start

### Requirements

- Python **3.12+**
- [PySide6](https://pypi.org/project/PySide6/)

### Run the editor

```bash
pip install PySide6
python AppMaker.py
```

> Use the actual entry script name from this repo if it differs (`nativize.py`, `main.py`, …).

### Optional (for packaging your apps)

```bash
pip install pywebview pyinstaller
```

- **Windows installer:** install [Inno Setup](https://jrsoftware.org/isinfo.php)  
- **Android APK:** install [Android Studio](https://developer.android.com/studio)

---

## Workflow

```text
1. New project
2. Edit index.html / css / js (add folders as needed)
3. Preview in the browser
4. Export → fill name, author, license, icon…
5. Choose target:
   • Web      → upload folder to hosting
   • EXE      → COMPILAR.bat → dist\App.exe
   • Setup    → compile setup.iss → Output\App_Setup.exe
   • Android  → open in Android Studio → Build APK
```

---

## Export targets

### Web

Static site ready for Netlify, Vercel, GitHub Pages, or any host.

```bash
cd export/web
npm start   # optional local server
```

### Windows EXE

Your UI runs inside a desktop window (pywebview + local server).

```bash
cd export/exe
pip install -r requirements.txt
python run_app.py          # test without compiling
# then run COMPILAR.bat  →  dist\YourApp.exe
```

Build tip (no black console window):

```bash
pyinstaller --onefile --windowed --name "YourApp" --icon=Icon.ico --add-data "www;www" run_app.py
```

### Setup (installer for your website)

1. Build the EXE first.  
2. Open `setup.iss` in **Inno Setup Compiler** (or run `CREAR_SETUP.bat`).  
3. Get `Output\YourApp_Setup.exe`.  
4. Upload that file to your domain / GitHub Releases.

If Windows says “install Inno Setup” but you already have it, `ISCC.exe` may not be on PATH — open the `.iss` in the Inno GUI and compile, or call:

```bat
"C:\Program Files (x86)\Inno Setup 6\ISCC.exe" setup.iss
```

### Android

Export generates a WebView project. Open it in Android Studio and build a signed APK for distribution.

---

## Project layout

```text
MyApp.miapp/
  project.json
  src/
    index.html
    css/style.css
    js/app.js
    package.json
    assets/
```

---

## Documentation

Full user manual (**30 pages**):

**[docs/HELP.md](docs/HELP.md)**

Includes install, UI, export tutorials (Web / EXE / Setup / Android), troubleshooting, FAQ, and roadmap.

---

## Build Nativize itself as an EXE

```bash
pyinstaller --noconfirm --onefile --windowed --name "Nativize" --icon=Icon.ico AppMaker.py
```

Output: `dist/Nativize.exe`

---

## Roadmap (short)

| Version | Focus |
|---------|--------|
| **0.1** | Editor, save/load, preview, Web + EXE scripts |
| **0.2** | Metadata dialog, Setup, Android project, docs |
| **Later** | Templates, CI examples, more polish |

See [docs/HELP.md](docs/HELP.md) for the full roadmap and FAQ.

---

## Contributing

Issues and pull requests are welcome.

When reporting a bug, include:

- OS version  
- Nativize / script version  
- Steps to reproduce  
- Logs if packaging failed (`build.log`, terminal output)

Please do **not** commit secrets, keystores, or personal absolute paths.

---

## License

This project is released under the **MIT License** (unless otherwise stated in `LICENSE`).

You are responsible for the license of **your own** exported apps and any third-party assets you bundle.

---

## Links

- Help guide: [docs/HELP.md](docs/HELP.md)  
- Inno Setup: https://jrsoftware.org/isinfo.php  
- PyInstaller: https://pyinstaller.org/  
- Android Studio: https://developer.android.com/studio  

---

<p align="center">
  <b>Nativize</b> — from code to Web, Windows, and Android
</p>
