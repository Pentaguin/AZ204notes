# Configure App Settings
- In App Service, app settings are passed as environment variables to the app code.
- For Linux and custom containers, App Services passes app settings to container user `--env` flag to set environment variables in container.

# Configure path mappings
- Linux and containerized apps
  - Add custom storage for your app
  - Containerized apps include all Linux apps and Windows and Linux custom containers running on App Service
- Windows apps (uncontainerized)
  - Customize IIS handler mappings and virtual apps and directories
  - Handler mappings enable adding custom script processors to handle requests for specific file extensions.

# Logging:
https://learn.microsoft.com/en-us/training/modules/configure-web-app-settings/5-enable-diagnostic-logging
![img.png](../../images/img2.png)

`Security`:
Options for adding certificate to app service:
![img.png](../../images/img3.png)

- Private certificate requirements:
  - Exported as a password-protected PFX file, encrypted using triple DES.
  - Contains private key at least 2048 bits long.
  - Contains all intermediate certificates and the root certificate in the certificate chain.

![img.png](../../images/img4.png)
![img.png](../../images/img5.png)