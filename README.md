# Hello World Deployment – Task 1.1  

This repository contains the solution for **Task 1.1 (Walkthrough Packaging)** of the Deployment Portfolio.  
The aim was to create a simple **Windows Forms “Hello World” application** and package it using:  
- A **WiX MSI installer**  
- A **UWP/MSIX sideloading package**  

This task formed the foundation for later deployment exercises.

---

## 📌 Environment Setup  

Before starting the project, the environment was configured with the following tools:  

- **Visual Studio Community 2022**  
  - Installed with the **.NET Desktop Development** workload.  
  - Included **.NET Framework SDKs and Targeting Packs** (4.7.2, 4.8, 4.8.1).  
  - Installed **Visual Studio Build Tools** (C++ + .NET build support).  
  - Enabled **MSIX Packaging Tools** for UWP package creation.  

- **WiX Toolset v3.11.2**  
  - Installed from the [official GitHub release](https://github.com/wixtoolset/wix3/releases/tag/wix3112rtm).  
  - Configured `WIX` environment variable pointing to installation directory.  
  - Verified installation by running `candle.exe` in Command Prompt.  
  - Installed **WiX v3 Visual Studio 2022 Extension** from Marketplace for direct integration[marketplace](https://marketplace.visualstudio.com/items?itemName=WixToolset.WixToolsetVisualStudio2022Extension).  

This setup ensured that both **MSI installers** and **UWP MSIX packages** could be created.

---
## 📂 Repository Structure  

The solution explorer for this repository consists of three main parts:  

```text
HelloWorldSolution/                 # Main Visual Studio solution folder
│
├── EshitaDesktopTutorial1/         # Main Windows Forms "Hello World" application
│   ├── Program.cs                  # Entry point for the application
│   ├── Form1.cs                    # Contains code to display "Hello World" message
│   ├── Form1.Designer.cs           # Auto-generated designer code for Form1 UI
│   ├── App.config                  # App configuration file
│   └── bin/Release/                # Compiled output (.exe, .dll, .pdb)
│       └── EshitaDesktopTutorial1.exe
│
├── SetupProject1/                  # WiX Setup project for MSI packaging
│   ├── Product.wxs                 # Installer configuration (GUIDs, components, directories)
│   ├── SetupProject1.wixproj       # WiX project file
│   └── bin/Release/                # Output MSI installer
│       └── SetupProject1.msi
│
└── HelloWorldPackage/              # UWP Packaging project for MSIX sideloading
    ├── Package.appxmanifest        # Defines app identity, visual assets, certificate info
    ├── HelloWorldPackage.wapproj   # Windows Application Packaging project file
    └── AppPackages/                # Generated MSIX bundle + certificate
        └── HelloWorldPackage_1.0.0.0_Test/
            ├── HelloWorldPackage_1.0.0.0_x64.msixbundle
            └── HelloWorldPackage_1.0.0.0_x64.cer


```
## ▶️ How to Build and Run  

### 1. Build the Hello World Application  
1. Open the solution in **Visual Studio 2022**.  
2. In the **Solution Explorer**, right-click `EshitaDesktopTutorial1` → **Set as Startup Project**.  
3. Select **Release mode** from the top toolbar.  
4. Build the project (**Build → Build Solution** or press `Ctrl+Shift+B`).  
5. Navigate to `bin/Release/` → run `EshitaDesktopTutorial1.exe` in file explorer.  
   - The app should launch and display a **Hello World message box**.  

---

### 2. Create and Run MSI Installer (WiX)  
1. In Solution Explorer, right-click `SetupProject1` → **Build**.  
2. Navigate to `SetupProject1/bin/Release/` → locate `SetupProject1.msi`.  
3. Double-click the `.msi` file to start installation.  
   - The installer will copy the app into **C:\Program Files (x86)\EshitaDesktopTutorial1**.  
4. After installation, open the **Start Menu** → search **EshitaDesktopTutorial1** → run.  
   - The app will launch and show the Hello World message.  

---

### 3. Create and Run MSIX Package (UWP Sideloading)  
1. In Solution Explorer, right-click `HelloWorldPackage` → **Publish → Create App Packages**.  
2. Choose **Sideloading** as the distribution method.  
3. Generate the package → Visual Studio will produce an `.msixbundle` and a `.cer` certificate inside:  HelloWorldPackage/AppPackages/HelloWorldPackage_1.0.0.0_Test/. Navigate to this section by right click 'HelloWorldPackage' -> 'Open in File explorer' -> 'AppPackages' -> 'HelloWorldPackage_1.0.0.0_Test'
4. Install the certificate:  
- Double-click the `.cer` file → Install Certificate.  
- Choose **Local Machine** → Place into **Trusted Root Certification Authorities**.  
5. Install the package:  
- Double-click the `.msixbundle` → Windows App Installer will open.  
- Click **Install** → App will be installed.  
6. Open the app via **Start Menu** → search for **HelloWorldPackage** → run.  
- The Hello World message box should appear.  

---

## ❌ Common Issues & Fixes  

- **Appx/MSIX installation blocked** → Ensure certificate is installed in **Trusted Root Certification Authorities**.  
- **WiX build fails with GUID errors** → Each `<Component>` in `Product.wxs` must have a unique GUID (use Visual Studio → Tools → Create GUID).  

---

## ✅ Outcomes  

- Built a Windows Forms Hello World app.  
- Successfully packaged into:  
- **MSI installer** (traditional desktop installer).  
- **MSIX sideloading package** (modern distribution).  
- Verified installation by running the deployed app from both Start Menu and App Installer.  

---

## 🔗 References  

- [WiX Toolset v3.11.2 GitHub Release](https://github.com/wixtoolset/wix3/releases/tag/wix3112rtm)  
- [WiX Visual Studio Extension](https://marketplace.visualstudio.com/items?itemName=WixToolset.WixToolsetVisualStudio2022Extension)  

---

## 👩‍💻 Author  

**Eshita Mahajan (104748964)**  
SWE40006 – Software Deployment and Evolution (Semester II, 2025)  

