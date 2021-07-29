A batch file that installs Chocolatey and uses it to install packages from Cholocatey repository.

Usage:

1. Go to https://community.chocolatey.org/packages and find your desired package (i.e. "google-chrome" from "choco install google-chrome")
2. Put in packages.txt the name of the package (i.e. "google-chrome")
3. Run the batch file. It is configured to check for admin privileges and ask for them if required (required by Chocolatey to function properly)