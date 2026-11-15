# Obstacle Challenge: retuned corners, parking correction and a single parqueo5

This update replaces Obs_Chall.py with the version used on 14 November. Con_ESP32.py, Ope_Chall.py and Pro_CAM.py are unchanged from the previous upload (fifth upload), so they are copied here only to keep every upload folder complete.

Changed:

The angle corrections added to "daniel" after each corner were adjusted again from measured drift. correctionClock went from 90.40 to 90.1 and correctionCounter from 90.63 to 90.45.

Two speed constants were retuned. SPEED_400 went from 550 to 520 and SPEED_600 from 600 to 620.

parqueo6() was removed. parqueo5() now takes a parameter called condicion. With condicion equal to 1 it does the parking maneuver as before, with a short reverse before the turn. With condicion equal to 2 it reverses until the left distance has changed between 100 and 200 mm, and then continues with the same turn into the parking space. The clockwise parking lane now calls parqueo5(condicion=2) where it used to call parqueo6().

parqueo2() was retuned. The first approach distance went from 965 to 954, the turn angle from -90 to -88, the front distance stop from 640 to 645, and an extra turn was added at the end to straighten the robot.

In salida_clock(), look_for_block() now looks until the front distance is 1000 mm instead of 400 mm.

Many approach distances and turn angles in the counterclockwise and clockwise corner routines were retuned (for example rojo_ccw, verde_ccw, rojo2_ccw, verde2_ccw, curva_r_ccw, verde, rojo, verde2 and the probot branches of navegacion and navegacion_ccw). Several of these now use a single drive_with_heading_lock() call instead of sigue_pared(), for example in the clockwise verde() and in the parking lane after a green block.

In the clockwise parking lane with probot equal to 3, the camera is read again before deciding, and the red and green cases were swapped so that each one now matches the colour seen.

Unchanged:

The PD turn in giro_con_imu(), the heading lock in drive_with_heading_lock(), move_for_distance(), look_for_block(), and the hardware setup (steering motor on Port B, traction motor on Port C, PUPRemote on Port F).

Known issues carried over:

salida_bloque() is still dead code. It reads "color" without reading the camera first, and nothing in the file calls it.

curva_v_ccw() compares the colour with 12 for red, while the other routines use 15.
