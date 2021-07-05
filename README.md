
# TheClockTwister's Template: `deb`
This template can be useful t ocopy when creating a distribution package for Debian-based OS like Debian itself, Ubuntu, Kali and any other Debian derivates.

----------

## Pre-requisites
Since you will probably run this on a Debian derivate, there are no additional packages that need to be installed or configured, since this is the most basic magic Debian does, when it comes to package management. 

_You just need to have apt and dpkg with their utilities installed, but as I said, this is most-likely the case._


## Building a `.deb` file
- When copying this template, the fodler hierarchy should look like this **(files/folders marked with `*` are mandatory):**
    ```
    mypackage_1.0_all   * (name_version_architecture)
    |- DEBIAN           * (Configuration fodler)
    |  |- control       * (Holds package information)
    |  |- preinst         (executed before installation)
    |  |- postinst        (executed after installation)
    |  |- prerm           (executed before removal)
    |  |- postrm          (executed after removal)
    ```

- Create the desired folder structure inside your package folder. Your package fodler will be treated as `/` on the installing system, meaning that `mypackage_1.0_all/bin/1337.txt` will end up in `/bin/1337.txt` on the target system. (missing directories will be created automatically)

- Make sure the install and uninstall scripts have executable permissions (755 or similar)!
    ```bash
    cd mypackage_1.0_all
    chmod 755 DEBIAN/pre* DEBIAN/post*
    cd ..
    ```

- Supply your package information in the `mypackage_1.0_all/DEBIAN/control` file

- Build the package into a the current directory
    ```bash
    dpkg-deb --build mypackage_1.0_all ./
    ```

