# Chocolatey Batch Installer

A batch script (`freshInstall.bat`) that automates the installation of Chocolatey (a package manager for Windows) and then uses it to install a list of specified software packages from `packages.txt`.

# About

Chocolatey is a package manager for Windows, similar to `apt-get` or `yum` on Linux, or Homebrew on macOS. It simplifies the process of installing and managing software. You can find more information on their official website: [https://chocolatey.org](https://chocolatey.org).

This script leverages Chocolatey to offer several benefits:

*   **Automating fresh Windows setups:** Quickly get your new Windows environment ready.
*   **Standardized tool installation:** Easily install a predefined set of software.
*   **Cross-machine consistency:** Ensure multiple Windows machines have the same tools.
*   **Time-saving automation:** Avoid repetitive manual installations.

# Prerequisites

-   **Operating System:** Windows.
-   **Internet Connection:** An active internet connection is required to download Chocolatey and the software packages.
-   **PowerShell:** The Chocolatey installation process uses a PowerShell script. `freshInstall.bat` attempts to set the required execution policies, but ensure PowerShell is enabled and can run scripts on your system.

# Usage

1.  **Find Packages:**
    *   Go to the [Chocolatey Community Package Repository](https://community.chocolatey.org/packages) to find your desired software.
    *   Note the package name (e.g., `google-chrome` from the command `choco install google-chrome`).

2.  **Edit `packages.txt`:**
    *   Open the `packages.txt` file in a text editor.
    *   Add each package name you want to install on a new line.
    *   To exclude a package, simply delete its line from the file or comment it out.
    *   You can add comments by starting a line with a `#` symbol. These lines will be ignored by the script.
    *   Example `packages.txt`:
        ```
        # Web Browsers
        google-chrome
        firefox

        # Development Tools
        git
        visualstudiocode
        ```

3.  **Run the Script:**
    *   Execute `freshInstall.bat`.
    *   The script will automatically check for administrator privileges and request them if necessary, as Chocolatey requires admin rights to install/manage software.

# How it Works

The `freshInstall.bat` script automates the setup process through the following steps:

1.  **Administrator Privileges Check:** The script begins by verifying if it has administrative rights. If not, it employs a VBScript method to request User Account Control (UAC) elevation. This is necessary because Chocolatey requires these permissions to manage software.
2.  **Chocolatey Installation:** Once running with sufficient privileges, the script downloads and executes the official Chocolatey installation script from the Chocolatey website using PowerShell. This installs Chocolatey on your system and adds its installation directory to your system's PATH environment variable, making `choco` commands accessible from any command prompt.
3.  **Package Processing:** After Chocolatey is set up, the script reads the `packages.txt` file line by line. For each entry (ignoring lines that start with `#`), it runs the command `choco upgrade <package_name> -y`.
    *   The `choco upgrade <package_name> -y` command will install the specified package if it's not already installed.
    *   If the package is already installed, `choco upgrade` will update it to the latest version if a newer one is available.
    *   The `-y` flag automatically confirms any prompts from Chocolatey, allowing the script to run without user intervention.

# Customizing `packages.txt`

The `packages.txt` file is designed for easy customization. You can tailor it to install exactly the software suite you need.

-   **Adding and Removing Packages:** As detailed in the 'Usage' section, simply add new package names (one per line) or delete lines for packages you no longer need.
-   **Organizing with Comments:** Use lines starting with a `#` symbol to add comments. This is a great way to categorize your packages and make `packages.txt` more readable. For example:
    ```
    # Development Tools
    git
    python3 # Installs the latest Python 3.x
    visualstudiocode

    # Utilities
    7zip
    powertoys
    ```
-   **Sharing Your Setup:** If you're using this script in a team or sharing your setup, your `packages.txt` can serve as a quick way to get everyone on the same page with a common set of tools.

# Troubleshooting

If you encounter issues while running the script, consider the following:

-   **Internet Connection:** Ensure you have a stable internet connection. Chocolatey needs to download its components and the software packages.
-   **Check `choco` Output:** Pay close attention to the messages printed in the command prompt. Chocolatey usually provides informative error messages if a package installation fails (e.g., package not found, download error, conflicts).
-   **Administrator Privileges:** The script is designed to request administrator privileges. However, if you suspect this is not working correctly, try running `freshInstall.bat` directly from a command prompt that you have manually launched with "Run as administrator" privileges.
-   **Specific Package Problems:** If a particular package fails to install, check its page on the [Chocolatey Community Package Repository](https://community.chocolatey.org/packages) for any specific troubleshooting tips, dependencies, or known issues.
-   **Log Files:** Chocolatey maintains log files, usually in `%ProgramData%\chocolatey\logs` (or `C:\ProgramData\chocolatey\logs`). These logs can provide detailed error information.

# .gitignore Suggestions

The `.gitignore` file helps prevent certain files from being accidentally committed to your Git repository.

-   **Temporary VBScript:** The `freshInstall.bat` script creates a temporary VBScript file (e.g., `OEgetPriv_freshInstall.vbs`) in the same directory to handle User Account Control (UAC) elevation for administrator privileges. It's recommended to add this to your `.gitignore` file.
-   **Other Files:** You might also consider adding other common files that don't need to be in version control, such as personal notes, local configuration overrides, or OS-specific temporary files.

A suggested line for your `.gitignore` to exclude the temporary VBScript is:
```
*getPriv_*.vbs
```