# OpenWrt Package Repository

This repository contains a collection of OpenWrt packages, automatically compiled from various third-party sources. It serves as a personal feed for centralized package management and continuous updates.

## Usage

The installation method depends on your OpenWrt version. Follow the instructions that match your system.

---

### For Stable Releases (e.g., openwrt-24.10) - Using `opkg`

1.  **Install the public signing key.**
    Connect to your device via SSH and run the following command to download the key to the trusted location:
    ```bash
    wget -O /etc/opkg/keys/ataraxiasjel.key https://openwrt.ataraxiadev.com/public.key
    ```

2.  **Add the package feed.**
    Add the following line to `/etc/opkg/customfeeds.conf`. If the file does not exist, create it.
    ```
    src/gz custom_repo_name https://openwrt.ataraxiadev.com/<version>/<architecture>
    ```
    *   **Example for `openwrt-24.10` on `aarch64_generic`:**
        ```
        src/gz ataraxiasjel_repo https://openwrt.ataraxiadev.com/openwrt-24.10/aarch64_generic
        ```

3.  **Update the package list.**
    ```bash
    opkg update
    ```

4.  **Install a package.**
    You can now securely install packages from this repository:
    ```bash
    opkg install <package_name>
    ```

---

### For SNAPSHOT Releases - Using `apk`

1.  **Install the public signing key.**
    Connect to your device via SSH. The key must be placed in `/etc/apk/keys/`.
    ```bash
    # Create the directory if it doesn't exist
    mkdir -p /etc/apk/keys/

    # Download the key
    wget -O /etc/apk/keys/ataraxiasjel-key.pem https://openwrt.ataraxiadev.com/public-key.pem
    ```

2.  **Add the package repository.**
    Add the repository URL to a new line in `/etc/apk/repositories`.
    ```
    https://openwrt.ataraxiadev.com/snapshot/<architecture>/packages.adb
    ```
    *   **Example for `SNAPSHOT` on `aarch64_generic`:**
        ```
        https://openwrt.ataraxiadev.com/snapshot/aarch64_generic/packages.adb
        ```

3.  **Update the package list.**
    ```bash
    apk update
    ```

4.  **Install a package.**
    You can now securely install packages from this repository:
    ```bash
    apk add <package_name>
    ```

---

## Repository Contents

This repository includes, but is not limited to, the following packages:

*   `zapret`
*   `zapret-tpws`
*   `zapret-mdig`
*   `zapret-ip2net`
*   `luci-app-zapret`
*   `podkop`
*   `luci-app-podkop`

A complete list of available packages can be found in the respective architecture directories.

## Automation and Source Code

Packages in this repository are compiled and updated automatically using GitHub Actions. The build process is configured to track new releases in the upstream source repositories and trigger a rebuild when they appear.

The workflow configuration are located in a [separate repository](https://github.com/AtaraxiaSjel/openwrt-repo-build).

## Disclaimer

All packages are provided "as is", without any warranty. Use of packages from this repository is at your own risk. The author is not responsible for any device failures or security issues caused by the use of these packages.
