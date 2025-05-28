
<h1>About</h1>

A batch file that uses winget to install packages from official and community winget sources.

<h1>Usage</h1>

1. Find the package ID for your desired software. You can do this by:
    - Using the command `winget search <AppName>` in your terminal (e.g., `winget search "Google Chrome"`).
    - Browsing online resources like [winget.run](https://winget.run/) or the official [microsoft/winget-pkgs GitHub repository](https://github.com/microsoft/winget-pkgs).
2. Put the exact package ID (e.g., "Google.Chrome") into `packages.txt`, one ID per line. Comments can be added using `#`.
3. Run the `freshInstall.bat` script. It is configured to check for admin privileges and ask for them if required (as some winget installations may need them).