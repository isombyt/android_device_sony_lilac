Device configuration for Sony Xperia XZ1 Compact (lilac)
========================================================

Description
-----------

This repository is for LineageOS 18.1 on Sony Xperia XZ1 Compact (lilac).

How to build LineageOS
----------------------

* Make a workspace:

        mkdir -p ~/lineageos
        cd ~/lineageos

* Initialize the repo:

        repo init -u git://github.com/LineageOS/android.git -b lineage-18.1

* Create a local manifest:

        vim .repo/local_manifests/roomservice.xml

        <?xml version="1.0" encoding="UTF-8"?>
        <manifest>
            <!-- SONY -->
            <project name="whatawurst/android_kernel_sony_msm8998" path="kernel/sony/msm8998" remote="github" revision="lineage-18.1" />
            <project name="whatawurst/android_device_sony_yoshino-common" path="device/sony/yoshino-common" remote="github" revision="lineage-18.1" />
            <project name="whatawurst/android_device_sony_lilac" path="device/sony/lilac" remote="github" revision="lineage-18.1" />

            <!-- Pinned blobs for lilac -->
            <project name="whatawurst/android_vendor_sony_lilac" path="vendor/sony/lilac" remote="github" revision="lineage-18.1" />

            <!-- OpenGApps -->
            <remote name="opengapps" fetch="https://github.com/opengapps/"  />
            <remote name="opengapps-gitlab" fetch="https://gitlab.opengapps.org/opengapps/"  />
            <project path="vendor/opengapps/build" name="aosp_build" revision="master" remote="opengapps" />
            <project path="vendor/opengapps/sources/all" name="all" clone-depth="1" revision="master" remote="opengapps-gitlab" />
            <project path="vendor/opengapps/sources/arm" name="arm" clone-depth="1" revision="master" remote="opengapps-gitlab" />
            <project path="vendor/opengapps/sources/arm64" name="arm64" clone-depth="1" revision="master" remote="opengapps-gitlab" />
        </manifest>

* Sync the repo:

        repo sync
        repo forall -r vendor/opengapps/sources -c git lfs pull

* Extract vendor blobs

        cd device/sony/lilac
        ./extract-files.sh

* Setup the environment

        source build/envsetup.sh
        lunch lineage_lilac-userdebug

* Build LineageOS

        make -j8 bacon
