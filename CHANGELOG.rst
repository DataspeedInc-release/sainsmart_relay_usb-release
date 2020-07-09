^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Changelog for package sainsmart_relay_usb
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

0.0.3 (2020-07-09)
------------------
* Increase CMake minimum version to 3.0.2 to avoid warning about CMP0048
  http://wiki.ros.org/noetic/Migration#Increase_required_CMake_version_to_avoid_author_warning
* Remove check for ROS distributions less than Kinetic
* Use the simple filename 'udev' when installing rules, instead of the debian package name
* Contributors: Kevin Hallenbeck

0.0.2 (2017-12-02)
------------------
* Added build dependency on roslib, needed for the ROS_DISTRO environment variable
* Contributors: Kevin Hallenbeck

0.0.1 (2017-11-30)
------------------
* Initial release
* Contributors: Kevin Hallenbeck
