
CAN or Control Area Network is a wired noise resistant bus type connection similar to wifi in it's message to all node design. The AGX jetson orin has two CAN lines 'can0' and 'can1'.

See
https://docs.nvidia.com/jetson/archives/r35.3.1/DeveloperGuide/text/HR/ControllerAreaNetworkCan.html?

**Startup**
1.  sudo ip link set can0 up type can bitrate 500000 dbitrate 1000000 berr-reporting on fd on
		iplink set can0 up : start can0 line
		type can : use CAN message
		bitrate 500000 : Classical CAN bitrate  to 500,000 bps (500 kbps)
		dbitrate 1000000 : CAN FD (flex data rate) 1Mbps
		berr-reporting on : report errors to user space
		fd on : enable CAN FD mode 





**Command Line**

Send on canline 0 to ID 123 message "abcabc"
	cansend can0 123#abcabc


dump all received CAN messages
	candump -x any & 

dump all received CAN messages with TX RX and timestamp
candump -ta -x -c -c can0 can1


dump all received CAN messages with TX RX and timestamp, filter out "002"
candump -ta -x -c -c can0 can1 | grep -v  "002"


Check bus status
ip link show dev can0
ip link show dev can1


mamamamamamamamamap

I have a Jetson Orin Dev and I have successfully run CAN sends via command line and I have used python socketCAN to communicate with my CAN interfaces on my MIT mini cheeta style motors. When I attempt to use the cantransmit.c example with socketcan on C my frame reads incorrectly on my scope and my motors cannot read the message as they do not send back their return state frame. It appears the flag bits are being attached to the message rotating it by 3 bits. 

My CAN setup file is as follows. 

# Close any CAN buses that are up
sudo ip link set down can0
sudo ip link set down can1

# set pins for CAN
sudo busybox devmem 0x0c303000 32 0x0000C400
sudo busybox devmem 0x0c303008 32 0x0000C454
sudo busybox devmem 0x0c303010 32 0x0000C400
sudo busybox devmem 0x0c303018 32 0x0000C454

sudo modprobe can
sudo modprobe can_raw
sudo modprobe mttcan
sudo ip link set can0 type can bitrate 1000000 sjw 4 dbitrate 1000000 berr-reporting on fd on
sudo ip link set can1 type can bitrate 1000000 sjw 4 dbitrate 1000000 berr-reporting on fd on
sudo ip link set up can0
sudo ip link set up can1

#show bus status
ip link show dev can0
ip link show dev can1

# open terminal and show CAN messages
candump -ta -x -c -c can0 can1
exec bash

I have physically connected my can0 and can1 buses to act as a loopback.

When I run cansend can0 00B#FFFFFFFFFFFFFD
I receive
 (1738264828.757803)  can0  TX - -  00B   [7]  FF FF FF FF FF FF FD
 (1738264828.757834)  can1  RX - -  00B   [7]  FF FF FF FF FF FF FD
 (1738264828.757938)  can0  RX - -  00B   [6]  0B 7F B2 80 27 FF
 (1738264828.757921)  can1  RX - -  00B   [6]  0B 7F B2 80 27 FF

Good message. Scope is clean and matches the message.

I have modified the address and message in the cantransmit.c to the following

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>

#include <net/if.h>
#include <sys/ioctl.h>
#include <sys/socket.h>

#include <linux/can.h>
#include <linux/can/raw.h>

int main(int argc, char **argv)
{
    int s; 
    struct sockaddr_can addr;
    struct ifreq ifr;
    struct can_frame frame;

    printf("CAN Sockets Demo\r\n");

    if ((s = socket(PF_CAN, SOCK_RAW, CAN_RAW)) < 0) {
        perror("Socket");
        return 1;
    }

    strcpy(ifr.ifr_name, "can0" );
    ioctl(s, SIOCGIFINDEX, &ifr);

    memset(&addr, 0, sizeof(addr));
    addr.can_family = AF_CAN;
    addr.can_ifindex = ifr.ifr_ifindex;

    if (bind(s, (struct sockaddr *)&addr, sizeof(addr)) < 0) {
        perror("Bind");
        return 1;
    }

    frame.can_id = 0x00B ; 
    frame.can_dlc = 8;

    unsigned char message[8] = {0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFD};

    memcpy(frame.data, message, sizeof(message));

    if (write(s, &frame, sizeof(struct can_frame)) != sizeof(struct can_frame)) {
        perror("Write");
        return 1;
    }

    if (close(s) < 0) {
        perror("Close");
        return 1;
    }
    return 0;
}

The Command line returns 

(1738265246.860569)  can0  TX B E  00B   [8]  FF FF FF FF FF FF FF FD
 (1738265246.860597)  can1  RX B E  00B  [08]  FF FF FF FF FF FF FF FD

There are B and E flags which I believe to be Base and Extended CAN ID flags which I believe to be conflicting. 

The Scope reads


Note the DLC is 7 not 8 and the first nibble in the message is 1 not F, the last byte has been pushed out of the dlc length.
It is my current theory that the motor is reading the same as the scope as the motor does not send back an acknowledgement. 

Has anyone successfully verified socketcan on the jetson orin? What setup code has worked? I have followed the available Nvidia setup guide to my knowlege. 


