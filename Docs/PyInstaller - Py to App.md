How to create a fully functional MacOS App from a python script and customtkinter

#### Step 1: Create a `venv`
In VS Code, open your Main Script and, in the Status Bar (at the bottom), click where it says the Python Version. Ex: `3.12.1'`. It will open a Menu that says `Select Interpreter`. Click on `Create Virtual Enviroment`and then `.venv`. Choose the version you are working with, in this example, `3.12.1`.
Wait until it creates the `venv`.

#### Step 2: Select the `venv`
Head onto the Terminal and type in (assuming the venv is in the current directory) `source .venv/bin/activate`. This will activate the venv.

#### Step 3: Create your Application!
Create your application using `customtkinter`(you can use any other but `customtkinter` is tested).

#### Step 4: Build the App
Start by creating the .spec file (`main.spec`). Type in:

```
# -*- mode: python ; coding: utf-8 -*-

a = Analysis(
    ['main.py'], # Replace with your app file
    pathex=[],
    binaries=[],
    datas=[],
    hiddenimports=[],
    hookspath=[],
    hooksconfig={},
    runtime_hooks=[],
    excludes=[],
    noarchive=False,
    optimize=0,
)
pyz = PYZ(a.pure)

exe = EXE(
    pyz,
    a.scripts,
    [],
    exclude_binaries=True,
    name='main',
    debug=False,
    bootloader_ignore_signals=False,
    strip=False,
    upx=True,
    console=False,
    disable_windowed_traceback=False,
    argv_emulation=False,
    target_arch=None,
    codesign_identity=None,
    entitlements_file=None,
)
coll = COLLECT(
    exe,
    a.binaries,
    a.datas,
    strip=False,
    upx=True,
    upx_exclude=[],
    name='main',
)
app = BUNDLE(
    coll,
    name='AppName.app', # Replace with your app name
    icon=None, # Replace with the path to the .icns (./logo.icns) or None
    bundle_identifier='com.paupalacios.AppName, # Can also be None
    info_plist={
        'CFBundleVersion': 'v1.0',
        'CFBundleShortVersionString': 'Made by Nico Palacios'
    }
)
```

If you want to add additional info (as you will to in the `.plist`), you can add them in `info_plist`. As an example I added the Bundle Version and String that show in the about section of the app.

Build the App: `pyinstaller --noconfirm main.spec`
- `--noconfirm` Prevents it from asking you to overwrite the app
- Replace `main.spec`with the name of the .spec file

#### Step 5: Test it!
Open Finder and open the App (located under the `dist`  folder)

Done!