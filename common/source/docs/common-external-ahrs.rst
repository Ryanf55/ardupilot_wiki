.. _common-external-ahrs:

=====================
External AHRS Systems
=====================

Rather than using ArduPilot's internal Attitude Heading Reference System (AHRS) for attitude, heading and position, it is possible to use several external systems.

Supported Systems
=================

Currently, ArduPilot supports these systems:

- `MicroStrain 3DM® Series <https://www.microstrain.com/inertial-sensors/all-sensors>`_
- `VectorNav VN-300 AHRS <https://www.vectornav.com/products>`__
- `VectorNav VN-100AHRS <https://www.vectornav.com/products>`__
- `Inertialabs INS-P <https://inertiallabs.com/wp-content/uploads/2023/09/INS-B-P-D-DL_Datasheet_rev-6.27_August_2023.pdf>`__

Setup
=====

Start with the common instructions, then follow the hardware-specific information.

Common
------

:ref:`EAHRS_SENSORS<EAHRS_SENSORS>` defaults to the recommended value for each driver.
This parameter configures which sensor data is exposed to ArduPilot EKF.

If bit 0 (GPS) is set, ensure that at least one of the following is true.
- :ref:`GPS_TYPE<GPS_TYPE>` = 21
- :ref:`GPS_TYPE2<GPS_TYPE2>` = 21

Set the SERIALx_PROTOCOL to “36” (AHRS) and SERIALx_BAUD to “115” (unless you have changed the external unit’s baud rate from its default value) for the port which is connected to the external AHRS unit.

When :ref:`AHRS_EKF_TYPE<AHRS_EKF_TYPE>` is set to 11 (ExternalAHRS), this will replace ArduPilot’s internally generated INS/AHRS subsystems with the external system.
In addition, instead of replacing ArduPilot's INS/AHRS systems, it is possible to use an external AHRS system's sensors (IMU,GPS, Compass, and Barometer) as additional sensors for use with ArduPilot's internal INS/AHRS systems.
Simply set the :ref:`AHRS_EKF_TYPE<AHRS_EKF_TYPE>` from "3" (EKF3).

Switching from the internal to external AHRS in flight
------------------------------------------------------

https://ardupilot.org/copter/docs/common-auxiliary-functions.html#supported-features
See ``SwitchExternalAHRS``


VectorNav300 or MicroStrain
---------------------------

    - :ref:`AHRS_EKF_TYPE<AHRS_EKF_TYPE>` = 11 (External AHRS)

    - :ref:`EAHRS_TYPE<EAHRS_TYPE>` = 1 (VectorNAV), 2 (MicroStrain5), 5(InertialLabs), or 7(MicroStrain7)

This will replace ArduPilot’s internally generated INS/AHRS subsystems with the external system.
The MicroStrain system must be configured via `Sensor Connect <https://www.microstrain.com/software/sensorconnect>`__ before use.

VN-300 Specific setup
~~~~~~~~~~~~~~~~~~~~~
When setting up the VN-300, it will be necessary to set :ref:`GPS_TYPE<GPS_TYPE>` = 21 and :ref:`GPS_TYPE2<GPS_TYPE2>` = 21. 

VN-300 data is expected at two different update rates, 50Hz and 5Hz. This is autoconfigured. See the `USER MANAUAL <https://www.vectornav.com/products/detail/vn-300>`__ for more details.


VectorNav100
------------

    - :ref:`AHRS_EKF_TYPE<AHRS_EKF_TYPE>` = 3 (ArduPilot's EKF3)

    - :ref:`EAHRS_TYPE<EAHRS_TYPE>` = 1 (VectorNAV)

    - :ref:`EAHRS_OPTIONS<EAHRS_OPTIONS>` bit 0 set to 1 ("1" value) to disable its compensation of the sensor biases, letting EKF3 do that (since there is no internal GPS to provide the best estimates)



