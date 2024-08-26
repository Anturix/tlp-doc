openSUSE
===============================
.. rubric:: Scope:

* Officially supported openSUSE Leap releases and Tumbleweed

.. note::

    Execute the commands below in a root shell or with with a preceding :command:`sudo`.

Package Installation
--------------------
Packages are available from the official repositories:

* **tlp** – Power saving
* **tlp-rdw** – optional - :doc:`/settings/rdw`

Install them either with your favorite package manager or the command: ::

    zypper install tlp tlp-rdw

*openSUSE Leap 15.4 and newer as well as Tumbleweed*

Uninstall the conflicting `power-profiles-daemon` package: ::

   zypper remove power-profiles-daemon

Service Units
-------------
To complete the installation you must enable TLP's service: ::

   systemctl enable tlp.service

You should also mask the following services to avoid conflicts and assure proper
operation of TLP's :doc:`/settings/radio` options: ::

   systemctl mask systemd-rfkill.service systemd-rfkill.socket

.. seealso::

    * FAQ: :ref:`Service units <faq-service-units>`
    * FAQ: :ref:`faq-ppd-conflict`

Legacy ThinkPads only: External Kernel Module for Battery Care
--------------------------------------------------------------
.. important::

    OpenSUSE Tumbleweed (at the time of writing) provides Linux kernel 6.10.
    In combination with TLP 1.5 or newer it offers full battery care support
    (i.e. charge thresholds and recalibration) for ThinkPads from model
    year 2011 onwards.

    **An external kernel module (also referred to as "out-of-tree" module)
    is not required in this case, and the following steps are not necessary.
    However, if your model is from 2011 or older, read on.**

Only if the bottom of the output of :command:`tlp-stat -b`, section 'Recommendations',
shows the line

.. code-block:: none

    Install tp-smapi kernel modules for ThinkPad battery thresholds and recalibration

then install the required package as follows.

**openSUSE Tumbleweed:** install from the official repository with your favorite
package manager or the command ::

    zypper install tp_smapi

**openSUSE Leap:** browse for `community packages of tp_smapi <https://software.opensuse.org/package/tp_smapi-kmp-default>`_
or build the required module from source. Your mileage may vary.
