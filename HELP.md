# Nativize — Complete Help Guide

**Documented versions:** 0.1 · 0.2  
**Repository docs:** place this file as [`docs/HELP.md`](docs/HELP.md) or link it from the main [README](../README.md).

Welcome to the official **Nativize** help manual. Content is split into numbered pages for easy reading on GitHub.

---

## Table of contents

### Part A — Getting started
- [Page 1 — What is Nativize](#page-1--what-is-nativize)
- [Page 2 — Installation](#page-2--installation)
- [Page 3 — First run](#page-3--first-run)
- [Page 4 — Interface overview](#page-4--interface-overview)
- [Page 5 — Projects and file structure](#page-5--projects-and-file-structure)

### Part B — Working with code
- [Page 6 — Creating and editing files](#page-6--creating-and-editing-files)
- [Page 7 — Supported languages](#page-7--supported-languages)
- [Page 8 — Preview](#page-8--preview)
- [Page 9 — Saving and opening projects](#page-9--saving-and-opening-projects)
- [Page 10 — Best practices for code](#page-10--best-practices-for-code)

### Part C — Export system
- [Page 11 — Export dialog (metadata)](#page-11--export-dialog-metadata)
- [Page 12 — Export overview](#page-12--export-overview)
- [Page 13 — Web export tutorial](#page-13--web-export-tutorial)
- [Page 14 — EXE export tutorial](#page-14--exe-export-tutorial)
- [Page 15 — Setup / installer tutorial](#page-15--setup--installer-tutorial)
- [Page 16 — Android export tutorial](#page-16--android-export-tutorial)
- [Page 17 — Full pipeline (zero to public download)](#page-17--full-pipeline-zero-to-public-download)
- [Page 18 — Icons, names, and branding](#page-18--icons-names-and-branding)

### Part D — Troubleshooting & advanced
- [Page 19 — Common EXE problems](#page-19--common-exe-problems)
- [Page 20 — Inno Setup and PATH issues](#page-20--inno-setup-and-path-issues)
- [Page 21 — PyInstaller tips](#page-21--pyinstaller-tips)
- [Page 22 — Offline vs online apps](#page-22--offline-vs-online-apps)
- [Page 23 — Security and licenses](#page-23--security-and-licenses)
- [Page 24 — Performance tips](#page-24--performance-tips)

### Part E — Project life & community
- [Page 25 — Versioning (0.1 / 0.2 / 1.0)](#page-25--versioning-01--02--10)
- [Page 26 — Roadmap](#page-26--roadmap)
- [Page 27 — FAQ](#page-27--faq)
- [Page 28 — Glossary](#page-28--glossary)
- [Page 29 — Contributing on GitHub](#page-29--contributing-on-github)
- [Page 30 — One-page summary](#page-30--one-page-summary)

---

# Part A — Getting started

# Page 1 — What is Nativize

## 1.1 Core idea

**Nativize** is a desktop tool that lets you write application code (especially **HTML, CSS, and JavaScript**) in a multi-file project and **package** it for:

| Target | Output | Typical use |
|--------|--------|-------------|
| **Web** | Static site + `package.json` | Hosting / your domain |
| **Windows EXE** | Desktop executable | App without a manual browser step |
| **Setup** | `*_Setup.exe` installer | Public download page |
| **Android** | WebView project | Build APK in Android Studio |

The main workflow is **code → files/folders → export**. It is not a PowerPoint-style visual slide designer.

## 1.2 Who it is for

- Developers shipping HTML/JS tools as Windows apps  
- Indie makers who need a simple installer for their website  
- Students learning how web UIs become desktop packages  
- Teams that want one project tree for web + desktop shell  

## 1.3 Design principles

1. **Code first** — the source of truth is your files.  
2. **Honest packaging** — Web, EXE, and Android paths are explicit.  
3. **Metadata matters** — name, license, icon, and copyright are part of export.  
4. **Scripts over magic** — when tools are missing, Nativize generates clear `.bat` / project files.

---

# Page 2 — Installation

## 2.1 Requirements

| Component | Required for |
|-----------|----------------|
| Python 3.12+ | Running the editor |
| PySide6 | Editor UI |
| pywebview | Running exported desktop apps |
| PyInstaller | Building `.exe` |
| Inno Setup | Building Windows installers |
| Android Studio | Building APK from export |

## 2.2 Install the editor

```bash
pip install PySide6
python AppMaker.py
```

Use the actual entry script name from this repository if it differs (`nativize.py`, `main.py`, …).

## 2.3 Optional tools for export

```bash
pip install pywebview pyinstaller
```

Install [Inno Setup](https://jrsoftware.org/isinfo.php) for Setup generation.

## 2.4 Packaging Nativize itself as EXE

```bash
pyinstaller --noconfirm --onefile --windowed --name "Nativize" --icon=Icon.ico your_script.py
```

Always use **`--windowed`** so users do not see a black console window.

---

# Page 3 — First run

1. Launch Nativize.  
2. Choose **New project** and enter an application name.  
3. A starter tree is created, for example:

```text
index.html
css/style.css
js/app.js
package.json
```

4. Edit `index.html` and styles/scripts.  
5. Press **Preview** to open the app in a browser.  
6. When ready, press **EXPORT** (`Ctrl+E`).

---

# Page 4 — Interface overview

## 4.1 Start screen

- **New project**  
- **Open project** (folder containing `project.json`)  
- **Recent projects**  

## 4.2 Main window

| UI region | Purpose |
|-----------|---------|
| Left tree | Project files and folders |
| Center editor | Code editing with basic highlighting |
| Toolbar | Save, Preview, **EXPORT**, add file/folder, delete |
| Menus | File / Edit / View / Export / Help |
| Status bar | Short hints and save/export messages |

## 4.3 Keyboard shortcuts (typical)

| Shortcut | Action |
|----------|--------|
| `Ctrl+S` | Save |
| `Ctrl+E` | Export dialog |
| `Ctrl+N` | New file |
| `F5` | Preview |
| `Delete` | Delete selected file/folder |

---

# Page 5 — Projects and file structure

## 5.1 Project format

A Nativize project is a folder (often ending in `.miapp`) with:

```text
MyApp.miapp/
  project.json    ← metadata
  src/            ← your source files
    index.html
    css/
    js/
```

## 5.2 Recommended layout

```text
src/
  index.html
  css/
    style.css
  js/
    app.js
  assets/
    img/
    fonts/
  data/
    config.json
  package.json
```

## 5.3 Rules of thumb

- One clear entry: `index.html`  
- Relative paths only (`js/app.js`, not `C:\...`)  
- Keep secrets out of the repo (API keys, keystores)

---

# Part B — Working with code

# Page 6 — Creating and editing files

## 6.1 New file

Toolbar **+ Archivo** / **+ File** or `Ctrl+N`.  
Enter a path such as:

- `js/player.js`  
- `data/settings.json`  
- `src/main.cpp`  

Folders in the path are created as needed.

## 6.2 New folder

Use **+ Carpeta** / **+ Folder** (e.g. `assets/icons`).

## 6.3 Delete

Select an item in the tree and press **Delete** or the delete toolbar button.

## 6.4 Editing

Click a file in the tree. Changes are kept in memory; **Save** writes the project to disk.

---

# Page 7 — Supported languages

Files are identified mainly by extension:

| Extension | Language / role |
|-----------|------------------|
| `.html` / `.htm` | Markup entry |
| `.css` | Styles |
| `.js` / `.ts` | Scripts |
| `.json` | Config / data |
| `.py` | Python sources in the project |
| `.cpp` / `.c` / `.h` | C/C++ sources |
| `.cs` | C# sources |
| `.md` | Notes / docs |
| `.svg` | Vector assets |

> **Note:** Storing C++/C# in the tree does not automatically compile them into the Windows EXE. The default desktop package runs the **web frontend** inside a native window.

---

# Page 8 — Preview

## 8.1 What Preview does

Preview writes the current files to a temporary folder and opens `index.html` in your default browser.

## 8.2 When to use it

- Layout and CSS checks  
- Quick JS debugging with browser DevTools  
- Before every export  

## 8.3 Limitations

- Browser preview is not identical to the EXE WebView in every edge case.  
- Always do a final test with `python run_app.py` or the built `.exe` after EXE export.

---

# Page 9 — Saving and opening projects

## 9.1 Save

- **Save** → writes to the current project path  
- **Save as…** → choose a parent folder; Nativize creates `Name.miapp`

## 9.2 Open

Choose the **folder** that contains `project.json` (the `.miapp` directory).

## 9.3 Recent list

The start screen lists recent project paths for faster reopening.

---

# Page 10 — Best practices for code

1. Keep UI logic in small JS modules when the app grows.  
2. Prefer relative asset paths.  
3. Test with empty cache after large CSS changes.  
4. Do not rely on `file://` quirks; the EXE runtime uses a tiny local HTTP server.  
5. Document your app’s version in both `package.json` and the export dialog.

---

# Part C — Export system

# Page 11 — Export dialog (metadata)

Open with **EXPORT** or `Ctrl+E`. Sections include:

### 11.1 Identity

- Application name  
- `.exe` file name (no spaces recommended)  
- Window title  
- Version  
- Author  
- Company  
- Short description  

### 11.2 License and copyright

- License (MIT, Apache-2.0, GPL-3.0, BSD, Proprietary, …)  
- Copyright line  

### 11.3 Icon and destination

- Icon file (`.ico` preferred on Windows)  
- Output folder  
- Android Package ID (`com.example.app`)  

### 11.4 Format

- Web  
- EXE + Setup  
- Android APK project  

### 11.5 Options

- Generate Setup scripts (`setup.iss`, `CREAR_SETUP.bat`)  
- Try to compile EXE immediately with PyInstaller  

---

# Page 12 — Export overview

| Format | Needs extra tools? | End result |
|--------|--------------------|------------|
| Web | Optional Node for `npm start` | Folder for hosting |
| EXE | PyInstaller + pywebview | `dist\App.exe` |
| Setup | Inno Setup + existing EXE | `Output\App_Setup.exe` |
| Android | Android Studio | Project → APK |

Export never deletes your original `.miapp` project; it writes a **copy** into the destination folder.

---

# Page 13 — Web export tutorial

## 13.1 Steps

1. Export dialog → **Web**  
2. Confirm metadata  
3. Choose output folder  
4. Export  

## 13.2 Output

```text
export/web/
  index.html
  css/
  js/
  package.json
  README.md
  …
```

## 13.3 Local test

```bash
cd export/web
npm start
```

## 13.4 Deploy

Upload the folder contents to your host. Point the domain (or subfolder) to `index.html`.

---

# Page 14 — EXE export tutorial

## 14.1 Steps in Nativize

1. Export → **EXE + Setup**  
2. Set `.exe` name and icon  
3. Export (with or without “compile now”)  

## 14.2 Generated files

```text
export/exe/
  www/               ← your site
  run_app.py
  requirements.txt
  COMPILAR.bat
  setup.iss
  CREAR_SETUP.bat
  LICENSE
  README.md
```

## 14.3 Test without building

```bash
cd export/exe
pip install -r requirements.txt
python run_app.py
```

## 14.4 Build the executable

Double-click `COMPILAR.bat` or run PyInstaller with `--onefile --windowed` and `--add-data` for the `www` folder.

Result: `dist\YourApp.exe`.

---

# Page 15 — Setup / installer tutorial

## 15.1 Why Setup

Installers create shortcuts, install directories, and uninstall entries—ideal for a **Download** button on your website.

## 15.2 Prerequisites

- `dist\YourApp.exe` already built  
- Inno Setup installed  
- `setup.iss` present  

## 15.3 Compile the installer

**Option A — GUI**

1. Open **Inno Setup Compiler**  
2. Open `setup.iss`  
3. Build → Compile  

**Option B — Command line**

```bat
"C:\Program Files (x86)\Inno Setup 6\ISCC.exe" setup.iss
```

## 15.4 Output

```text
Output\YourApp_Setup.exe
```

Upload that file to your domain.

## 15.5 Minimal install link

```html
<a href="/downloads/YourApp_Setup.exe" download>Download for Windows</a>
```

---

# Page 16 — Android export tutorial

## 16.1 What you get

A Gradle Android project embedding your web files under:

```text
app/src/main/assets/www/
```

## 16.2 Steps

1. Export → Android  
2. Set Package ID (`com.company.app`)  
3. Open the folder in Android Studio  
4. Build → Build APK(s)  

## 16.3 Signing

For store or production installs, use **Generate Signed Bundle / APK** with your keystore. Never commit keystores to GitHub.

---

# Page 17 — Full pipeline (zero to public download)

```text
1. New project in Nativize
2. Edit HTML / CSS / JS
3. Preview in browser
4. Export → EXE + Setup (fill metadata + icon)
5. Run COMPILAR.bat → dist\App.exe
6. Test App.exe
7. Compile setup.iss → Output\App_Setup.exe
8. Upload App_Setup.exe to your website
9. Optional: Web export for online demo
10. Optional: Android export → APK
```

---

# Page 18 — Icons, names, and branding

## 18.1 Names

| Field | Example | Tips |
|-------|---------|------|
| App name | `My Shop` | Shown to users |
| EXE name | `MyShop` | No spaces or special chars |
| Window title | `My Shop` | Title bar text |

## 18.2 Icons

- Prefer **`.ico`** for Windows taskbar/title bar  
- Provide at least 256×256 source art when possible  
- Set the icon in the export dialog and again in Inno Setup (`SetupIconFile`)

## 18.3 Branding checklist

- [ ] Consistent name across EXE, Setup, and website  
- [ ] License and copyright filled  
- [ ] Icon on EXE and installer  
- [ ] Version number bumped before each public build  

---

# Part D — Troubleshooting & advanced

# Page 19 — Common EXE problems

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| Black console window | Built without `--windowed` | Rebuild with `--windowed` |
| Empty white/black window | Missing `www/index.html` or `file://` issues | Use generated `run_app.py` runtime |
| “pywebview not found” | Dependency missing on build machine | `pip install pywebview` before PyInstaller |
| Huge EXE size | Onefile + heavy deps | Expected; or use onedir mode |
| Antivirus alert | New unsigned binary | Sign code or whitelist during testing |

---

# Page 20 — Inno Setup and PATH issues

If a batch file says **install Inno Setup** but you already installed it:

1. `ISCC.exe` is probably not on PATH.  
2. Open the `.iss` file in Inno Setup Compiler and compile from the GUI.  
3. Or call the full path to `ISCC.exe`.  

Common locations:

```text
C:\Program Files (x86)\Inno Setup 6\ISCC.exe
C:\Program Files\Inno Setup 6\ISCC.exe
```

Updated Nativize scripts also search these folders automatically.

---

# Page 21 — PyInstaller tips

```bash
# Recommended pattern for a Nativize-exported app
pyinstaller --noconfirm --onefile --windowed ^
  --name "MyApp" ^
  --icon=Icon.ico ^
  --add-data "www;www" ^
  run_app.py
```

- Use `;` on Windows and `:` on Linux/macOS for `--add-data`.  
- Keep `console=False` in `.spec` files.  
- Read `build.log` when builds fail.  
- Clean `build/` and `dist/` before release builds.

---

# Page 22 — Offline vs online apps

## Offline-friendly

- Local HTML/CSS/JS  
- Assets embedded under `www/`  
- No required API calls  

## Needs network

- CDN libraries without a local fallback  
- Auth or cloud APIs  
- Analytics endpoints  

Document network needs on your download page.

---

# Page 23 — Security and licenses

- Fill **license** and **copyright** on every public export.  
- Do not ship proprietary third-party assets without permission.  
- Do not commit API keys, keystores, or `.env` secrets.  
- Treat user data carefully if your HTML app stores anything locally.

---

# Page 24 — Performance tips

- Compress PNG/JPEG/WebP assets.  
- Avoid unused JS libraries.  
- Lazy-load heavy screens if you build multi-page UIs.  
- Test EXE startup time on a low-end PC.  
- Prefer CSS animations over heavy JS loops.

---

# Part E — Project life & community

# Page 25 — Versioning (0.1 / 0.2 / 1.0)

| Version | Meaning |
|---------|---------|
| **0.1.x** | Editor + basic export works |
| **0.2.x** | Setup, metadata dialog, Android project path |
| **1.0.0** | Stable public workflow and docs |

Bump the version in the export dialog **and** in `package.json` when you ship.

---

# Page 26 — Roadmap

## Done / in 0.1–0.2 focus

- Multi-file code editor  
- Project save/load  
- Web export  
- EXE runtime + scripts  
- Setup (Inno Setup)  
- Android WebView export  
- Metadata: name, author, license, icon, copyright  

## Possible later ideas

- Official English/Spanish UI toggle  
- Project templates  
- CI examples for GitHub Actions  
- Code signing docs  
- Plugin hooks  

---

# Page 27 — FAQ

**Q: Can pure HTML become an EXE?**  
A: Yes. That is the primary desktop path.

**Q: Do end users need Python?**  
A: No. Only the builder machine needs Python/PyInstaller.

**Q: Why does a console open with my EXE?**  
A: Rebuild with `--windowed`.

**Q: Inno Setup is installed but scripts fail?**  
A: Compile `setup.iss` from the Inno GUI or use the full path to `ISCC.exe`.

**Q: Can I host the Setup on GitHub Releases?**  
A: Yes. Attach `*_Setup.exe` to a Release and link it from your README.

**Q: Does Android export produce a Play Store bundle automatically?**  
A: No. It produces a project; you build/sign in Android Studio.

---

# Page 28 — Glossary

| Term | Definition |
|------|------------|
| **Nativize** | This editor and packaging toolchain |
| **`.miapp`** | Project folder with `project.json` + `src/` |
| **Runtime** | Host process that shows your HTML in a desktop window |
| **PyInstaller** | Freezes Python apps into Windows executables |
| **Inno Setup** | Builds Windows installers from a `.iss` script |
| **WebView** | Native control that renders HTML/CSS/JS |
| **Package ID** | Android application id (`com.company.app`) |
| **Setup** | Installer executable for distribution |

---

# Page 29 — Contributing on GitHub

## 29.1 Issues

When filing an issue, include:

- OS version  
- Nativize version  
- Steps to reproduce  
- Relevant logs (`build.log`, terminal output)  

## 29.2 Pull requests

- Keep changes focused  
- Update docs if behavior changes  
- Do not commit binaries, secrets, or personal paths  

## 29.3 Suggested repo layout

```text
README.md
LICENSE
docs/
  HELP.md          ← this file
  screenshots/
assets/
  Icon.ico
```

## 29.4 README badge ideas

```markdown
![version](https://img.shields.io/badge/version-0.2-blue)
![platform](https://img.shields.io/badge/platform-Windows%20%7C%20Web%20%7C%20Android-lightgrey)
```

---

# Page 30 — One-page summary

1. Install Python + PySide6 and run Nativize.  
2. Create a project; edit `index.html`, CSS, and JS.  
3. Preview until it looks right.  
4. Open **EXPORT** and set name, author, license, copyright, icon.  
5. Choose a target:
   - **Web** → upload folder to hosting  
   - **EXE** → build with PyInstaller (`--windowed`)  
   - **Setup** → compile `setup.iss` with Inno Setup → put `*_Setup.exe` on your domain  
   - **Android** → open project in Android Studio → build APK  
6. Test on a clean machine before announcing the release.

---

## Document info

- **Product:** Nativize  
- **Help revision:** 0.2-docs  
- **Pages:** 30  
- **Format:** GitHub-flavored Markdown  

*End of help guide.*
