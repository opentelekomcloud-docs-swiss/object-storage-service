:original_name: obs_03_0347.html

.. _obs_03_0347:

Time Difference Is Longer Than 15 Minutes Between the Client and Server
=======================================================================

**Symptom**

Error message "Time difference is longer than 15 minutes between the client and server" or "The difference between the request time and the current time is too large" is displayed during the use of OBS.

**Cause**

For security purposes, OBS verifies the time offset between the client and server. If the offset is longer than 15 minutes, the OBS server will reject your requests and this error message is reported.

**Solution**

To resolve this problem, adjust your local time (UTC) and try again.
