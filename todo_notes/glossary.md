# Glossary

* Bootloader: A general term for a link in the boot-chain that has a specific job that is run each cold-boot
* cold-boot: Fresh boot from powered off state
* QFUSE: Microscopic hardware fuse that is integrated into the SoC - Once physically blown, impossible to reset or replace
* SoC: System-on-chip (your phone’s “motherboard” of sorts)
* EFUSE: Software based fuse whose data is stored in QFPROM
* QFPROM: Qualcomm’s fuse region
* TrustZone: Qualcomm ARM chipset’s “Secure World” implementation
* QSEECOM: A linux kernel driver that lets us communicate with TrustZone, and issue an SCM call to TrustZone to do things like blow fuses. It only will allow signed applets and approved calls to be made
* SCM: Secure Channel Manager (note: not related to Linux’s SMC calls)
* DTB: Device Tree Blob. Its purpose is to “provide a way to describe non-discoverable hardware” to Linux, read more [here](https://elinux.org/Device_Tree_Reference)
* Android Verified Boot (AVB): A strict set of checks implemented at the aboot/ABL level to verify the integrity of various parts of the operating system, read more [here](https://source.android.com/security/verifiedboot/)
* DM-Verity: A component of Android Verified Boot that checks partitions to see if they have beeen mounted read/write before, read more [here](https://source.android.com/security/verifiedboot/dm-verity)
* system_as_root: A new mount setup logic for android that mounts the system partition as ‘/’ as opposed to ‘/system’. This means that system files now live at ‘/system/system’. This is a way for Qualcomm to check whether ‘/’ has ever been remounted read/write under Verified Boot. It also introduces the new standard that the Android ramdisk be stored on the system partition, as opposed to being stored in the boot image

Telephony :
* Command: A request from frameworks to modem to perform a task, or return data required by userspace
* Request: See Command
* Response: Information from the modem to frameworks in response to a request being sent
* Indication: Information from the modem to the frameworks as a result of an event occurring
* Solicited Response: Legacy name for Response
* Unsolicited Response: Legacy name for Indication
* Unsol: Short for unsolicited response
* DSDA: Short for Dual SIM Dual Active, a type of Multi-SIM device in which two discrete modems are present, and two subscriptions can be active at the same time
* DSDS: Short for Dual SIM Dual Standby, a type of Multi-SIM device in which one modem handles two SIM slots, and only one subscription can be active at any given time
* IMS: Short for IP Multimedia Subsystem, used as an umbrella term for features such as VoLTE and WFC (VoWiFi) in Android
* VoLTE: Short for Voice over LTE, standard for transmitting phone calls over LTE networks
* VoWiFi: Short for Voice over WiFi, alternate name for WFC
* WFC: Short for WiFi Calling
* RIL: Short for Radio Interface Layer, generally used to refer to the modem interface library or libril, sometimes used to refer to any part or the whole of the Telephony stack

* Android Compatibility Definition Document (CDD) : This document enumerates the requirements that must be met in order for devices to be compatible with the latest version of Android. (pdf)

* HAL stands for hardware abstraction layer. Generally it's a piece of software that interacts with a specific piece of hardware and exposes a generic application programming interface for that hardware. That way, any software that wants to use the hardware doesn't have to implement all of the hardware specific features, just utilize the API. For example, Qualcomm's Vulkan drivers act as a HAL upon the Adreno GPU. The programmer doesn't care how the Adreno works, but instead only cares that the HAL and the hardware correctly implement whatever is specified in the API.

* A "blob" in the android context, is just some binary. Often these blobs will interface with some hardware or will implement crucial features that enable some other feature on the phone. The "blobs" we talk about are generally from OEMs and manufacturers that users don't know or care about. One such blob (which you probably don't even know exists!) is the Trustzone blob. Without it, your phone wouldn't boot up, show the display, anything really. What does it do? A ton of stuff, though nothing that the user needs to worry or care about.
