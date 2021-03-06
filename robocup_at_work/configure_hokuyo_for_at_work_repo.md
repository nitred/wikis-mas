Hokuyo at_work configuration
============================

This tutorial describes how to configure hokuyo laser scanner for usage with the BRSU robocup at work team 

in the youbot robot from scratch.

NOTE : If you are working in the youbot computer's most probably this was already done by the staff members.

documentation available at:

		http://wiki.ros.org/youbot_driver
		http://www.reactivated.net/writing_udev_rules.html

creating a udev rule
====================

go to rules.d directory:

		cd /etc/udev/rules.d

create a file (on the previous location) with the name "47-hokuyo.rules" with the following data on it:

		SUBSYSTEMS=="usb", KERNEL=="ttyACM0", ATTRS{manufacturer}=="Hokuyo Data Flex for USB", ATTRS{product}=="URG-Series USB Driver", MODE="0666", SYMLINK+="youbot/hokuyo_front"

		SUBSYSTEMS=="usb", KERNEL=="ttyACM1", ATTRS{manufacturer}=="Hokuyo Data Flex for USB", ATTRS{product}=="URG-Series USB Driver", MODE="0666", SYMLINK+="youbot/hokuyo_rear"

confirm that the rules are working:

		ls /dev/youbot

you should see:

		hokuyo_front hokuyo_rear

check if the proper permissions were given:

		cd /dev/youbot
		ls -lha

you should see something like this:

		lrwxrwxrwx  1 root root   10 Dec  7 13:57 hokuyo_front -> ../ttyACM0
		lrwxrwxrwx  1 root root   10 Dec  7 14:01 hokuyo_rear -> ../ttyACM1

as you can see output now reflects the fact that the port has been given read and write access and also that a symbolic link in /dev/youbot/hokuyo_front as well as /dev/youbot/hokuyo_rear was created

Now hokuyo front and rear sensors are properly configured to run with the HBRS @work team code.

NOTE: In this case the first connected hokuyo will recive the "hokuyo_front" tag and the next one the "hokuyo_rear" tag.