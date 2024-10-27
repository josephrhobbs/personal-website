# Proton

~

During the summer following my junior year, I was offered an internship at Adom Industries, a small start-up based in the Dallas-Fort Worth Metroplex in Texas.  As of the time of writing, Adom is in stealth mode right now, so I'll refrain from sharing the details of my work.  However, it involved a lot of wireless computer networking, and in the course of my project I began developing a Rust package for wireless access point management for Linux machines. 

I love giving back to the greater software development community, and so I obtained permission from the company to release the code as open-source.  Adom graciously agreed, and so I released the Proton Access Point Management Library under the MIT License.

## Vision

The vision of the Proton Access Point Library was quite simple.  I needed a way to control the functionality of a Wi-Fi access point in an asynchronous, type-safe, and simple manner.  I planned to use the NetworkManager system daemon for my project, but the Rust API bindings available can be difficult to use and lack certain features, such as IPv4 address discovery.

### Asynchronous Design

Asynchronous programming enables computers to execute multiple tasks concurrently, but not necessarily simultaneously.  This is analogous to one chef having multiple pots on the stove... he can only stir one pot at a time, but he doesn't have to finish one dish before starting the next.

The asynchronous programming paradigm is critical for Proton (and many other networking packages) because networking is time-sensitive by its nature.  Data is transmitted over time, and if the receiver doesn't receive it in time, it's gone.  Asynchronous programming allows Proton to focus on what's most important \it{right now} and then turn to less important tasks while it's waiting.

### Type Safety

In a nutshell, a program is type-safe when it "can't go wrong."  More specifically, it's important that I can't apply a method to a data structure that doesn't have that method or otherwise process a data structure incorrectly.  Rust's zero-cost abstraction makes it an excellent choice for a complex program such as Proton.  The Rust compiler can optimize away all of the object-oriented complexity that I create, and yet it will still prevent me (and others) from making silly mistakes.

### Simplicity

Software should always be as simple as possible, but no simpler.  I didn't want to tie together a dozen APIs in the frontend or deal with a number of complex data structures... I wanted an interface that "just worked."

As explained in the below section on the structure of the Proton library, I have a very minimal outward-facing API, because I wanted the code to be self-documenting and not require significant mental effort to understand.

## Structure

The Proton library is likely the most complex software package I've ever developed, and it contains a number of interconnected and interdependent elements.

## Access Point Management

The top level of the Proton software stack contains the access point manager.  This is an API structure that is exposed to the end user for manipulation.

The user may create a hotspot connection with a given SSID, password, and security protocol.  The user may then activate, deactivate, or delete that hotspot connection.  The user also can scan the access point's wireless network to obtain a list of connected network devices.

## Device Management

One level below access point management is device management.  This layer of the software stack is responsible for discovering connected network devices.

Network device discovery is performed using two methods in tandem.  The first involves direct communication with the Linux kernel via Generic Netlink.  The device manager opens a communication channel with the Linux kernel and requests a list of devices connected to the hotspot.  This method is capable of obtaining the hardware (MAC) address, signal strength, and connection time of the device.  It is not, however, capable of determining the IPv4 address of each connected device.

Enter the second method of network device discovery: Address Resolution Protocol (ARP).  ARP is compartmentalized away from device management and is conducted by a separate collection of methods.  This keeps device management code from becoming too complex.  The ARP manager provides a list of devices by their IPv4 addresses and their corresponding MAC addresses.  The device manager uses this information to complete its own device list, which it may return to the end user via the access point manager.

## ARP Management

Address Resolution Protocol (ARP) behaviors are managed by this software stack layer.  The ARP manager interfaces with Layer 2 (Data Link Layer) of the Open Systems Interconnection (OSI) model via the network interface manager, and it sends ARP frames across the network requesting the hardware (MAC) address for each IPv4 address in the network range.

The ARP manager requires a significant number of asynchronous programming structures.  This is because it must simultaneously send ARP requests and listen for their responses.  The Tokio package for Rust asynchronous programming provides all asynchronous functionality to the ARP manager. 

## Network Interface Management

The network interface manager provides direct interface to the Wi-Fi card of the access point.  It constructs individual ARP Request frames for the ARP manager, and it parses ARP Reply frames to be registered by the ARP manager.

## Hotspot Configuration

The Proton library requires a hotspot configuration data structure, exposed to the end user, that contains a full characterization of the hotspot on the access point.  Hotspot configuration structures contain: SSID, password, security type, frequency band, network gateway IPv4 address, and network range in IPv4 CIDR notation.

## Hardware Addressing

The Proton library additionally requires abstractions over and methods on hardware (MAC) addresses.  The library implements these natively in a separate crate.

## Error Handling

Finally, the Proton library requires a shared error handling methodology, to streamline spftware development as well as debugging and the experience of library users.  The Proton implements a robust error handling system natively in order to facilitate safe error handling across the rest of the library.

## Features

Currently, the Proton access point management library can create, activate, deactivate, and delete hotspots on the device upon which they are installed.  Proton is also capable of scanning its hotspot's network and reporting MAC address, IPv4 address, signal strength, and connection time of every network device.

## Improvements

Adom Industries is the licensor of Proton, and as of this writing, I have completed my internship at their company; therefore, I am no longer the primary developer of the library.  I may fork the library to my personal GitHub account and continue development out of personal interest, though I don't have any pressing need to do so and therefore this is low on my priority list.

## Source Code

As mentioned above, the source code for the Proton access point management library has been released open-source under the MIT License by Adom Industries.  It may be found on the Adom Industries GitHub.

[https://github.com/adom-inc/proton](https://github.com/adom-inc/proton)

## Credits

Thanks to John Lauer, CEO of Adom Industries, for the opportunity to work at his company, as well as for the permission to release this project open-source.  Working at Adom was a pleasure and I learned far more about this field than I ever thought I could in twelve weeks.

Thanks to Adrian Wowk, software developer at Adom Industries, for help in debugging many aspects of my internship's project, including the source code of Proton.