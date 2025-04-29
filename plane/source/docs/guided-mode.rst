.. _guided-mode:

===========
GUIDED Mode
===========

GUIDED mode can be used when you want the aircraft to fly to a specific
point on the map without setting up a mission. Most ground control
stations support a "click to fly to" feature where you can click a point
on the map and the aircraft will fly to that location then loiter.

.. note::

   ArduPlane does not yet guarantee the safety of guided "fly-to" commands in steep terrain, even if :ref:`TERRAIN_FOLLOW<TERRAIN_FOLLOW>` is enabled.
   See `ardupilot/#29914 <https://github.com/ArduPilot/ardupilot/issues/29914>`__ for details.

The other major use for GUIDED mode is in :ref:`geo-fencing <geofencing>`.
When the geo-fence is breached the aircraft will enter GUIDED mode, and
head to the predefined geo-fence return point, where it will loiter
until the operator takes over.

Finally, guided mode can be used with a companion computer or scripting for lower level commands.
See :ref:`here <plane-commands-in-guided-mode>` for details.
