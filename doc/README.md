# 【JTAG-SMT3参考手册】JTAG-SMT3-NC Reference Manual

原文网址 ： [JTAG-SMT3-NC Reference Manual - Digilent Reference](https://digilent.com/reference/programmers/jtag-smt3/reference-manual)

The Joint Test Action Group (JTAG)-SMT3-NC is a compact, complete, and fully self-contained surface-mount programming module for Xilinx field-programmable gate arrays (FPGAs). The module can be accessed directly from all Xilinx Tools, including iMPACT, ChipScope™, Vivado, and EDK. Users can load the module directly onto a target board and reflow it like any other component.

The JTAG-SMT3-NC uses a 3.3V main power supply and independent Vref supplies to drive the JTAG and UART signals. All JTAG signals use high speed 24mA three-state buffers that allow signal voltages from 1.8V to 5.5V, and bus speeds up to 30MBit/sec. All UART signals use high speed 24mA buffers that allow signal voltages from 1.8V to 5.5V and bus speeds up to 12Mbaud. The JTAG bus can be shared with other devices as the SMT3-NC signals are held at high impedance, except when actively driven during programming. The SMT3-NC module is CE certified and fully compliant with EU RoHS and REACH directives. The module routes the USB D+ (DP) and D- (DM) signals out to pads, providing the system designer with the ability to choose the type of USB connector and its location on the system board.

![img](https://digilent.com/reference/_media/reference/programmers/jtag-smt3/jtag-smt3-0.png)

![img](https://digilent.com/reference/_media/reference/programmers/jtag-smt3/jtag-smt3-1.png)

![img](https://digilent.com/reference/_media/reference/programmers/jtag-smt3/jtag-smt3-2.png)

![img](https://digilent.com/reference/_media/reference/programmers/jtag-smt3/jtag-smt3-3.png)


##### Download This Reference Manual

- [PDF](https://digilent.com/reference/_media/reference/programmers/jtag-smt3/jtag-smt3-nc-rm.pdf)

### Features

- Small, complete, all-in-one JTAG programming/debugging solution for Xilinx FPGAs with UART side channel
- Compatible with Xilinx Tools
- High-Speed USB 2.0 port that can drive JTAG bus up to 30Mbit/sec (frequency settable by user)
- Open drain buffer on PS_SRST_B pin allows debugging software to reset the processor core of Xilinx’s Zynq® platform
- Dual channel USB controller provides simultaneous access to both JTAG and UART interfaces
- Separate Vref for JTAG and UART signals allows each interface to operate at difference voltages (1.8V to 5.5V)
- Small form-factor surface-mount module can be directly loaded on target boards
- USB D+ and D- signals routed to pads, allowing USB connector to be placed anywhere on the host PCB
- VBUS_DETECT pin allows for reduced current consumption when the module isn’t connected to a PC

Users can connect JTAG signals directly to the corresponding FPGA signals, as shown in Fig. 1. For best results, mount the module over a ground plane on the host PCB. Although users may run signal traces on top of the host PCB beneath the SMT3-NC, Digilent recommends keeping the area immediately beneath the SMT3-NC clear.

*Note: Keep the impedance between the SMT3-NC and FPGA below 100 Ohms to operate the JTAG at maximum speed.* *Note: If series resistors are used, they should be placed near the transmitting end in order to minimize reflections.*

In addition to supporting JTAG, the JTAG-SMT3-NC also features a UART Interface that allows communication with UART peripherals (see Fig. 2). The UART interface is presented as a virtual com port on the host PC, supports baud rates up to 12Mbaud, and has an independent voltage reference which allows it to interface with devices operating at voltages between 1.8V and 5.5V.

![Figs. 1 & 2.](https://digilent.com/reference/_media/reference/programmers/jtag-smt3/figs-1-and-2.png?w=800&tok=b7aac8)

------

## Software Support

The JTAG-SMT3-NC has been designed to work seamlessly with Xilinx’s ISE® (iMPACT, ChipScope, EDK, and eFuse) and Vivado tool suites. The most recent versions of ISE and Vivado include all of the drivers, libraries, and plugins necessary to communicate with the JTAG-SMT3-NC. At the time of writing, the following Xilinx software included support for the SMT3: Vivado 2017.1+, Vivado 2016.1+, Vivado 2015.1+, Vivado 2014.1+, and ISE 14.1+. The SMT3-NC is also compatible with ISE 13.1 - 13.4; however, these versions of ISE do not include all of the libraries, drivers, and plugins necessary to communicate with the SMT3-NC. In order to use the JTAG-SMT3-NC with these versions of ISE, version 2.5.2 or higher of the [Digilent Plugin for Xilinx Tools](https://digilent.com/shop/software/) package must be downloaded from the Digilent website and the ISE13 plugin must be manually installed as described in the included documentation.

In addition to working seamlessly with all Xilinx tools, [Digilent’s Adept software](https://digilent.com/shop/software/digilent-adept/) and the Adept software development kit (SDK) support the SMT3-NC module. For added convenience, customers may freely download the SDK from Digilent’s website. This Adept software includes a full-featured programming environment and a set of public application programming interfaces (API) that allow user applications to directly drive the JTAG chain.

With the Adept SDK, users can create custom applications that will drive JTAG ports on virtually any device. Please see the Adept SDK reference manual for more information.

------

## PS_SRST_B Pin

When customers use the JTAG-SMT3-NC to interface the scan chain of Xilinx’s Zynq platform, they should connect the PS_SRST_B pin of the SMT3-NC to the Zynq’s PS_SRST_B pin. This connection allows the Xilinx Tools to reset the Zynq’s processor core at various times during debugging operations. The PS_SRST_B pin on the SMT3-NC is driven by an open drain buffer that is capable of sinking up to 32mA of current. Customers who connect this pin must provide an external pull-up to the appropriate supply rail. A pull-up resistor between 1K - 100K Ohms is recommended. Please see the following “Application Examples” section for more information.

------

## VBUS_DETECT Pin

The VBUS_DETECT pin is used by the USB controller to determine when VBUS is present. When a logic ‘0’ is detected on this pin, the USB controller is forced into suspend mode. This prevents the SMT3-MC from forcing current down the USB lines when the host or the hub is powered off. Additionally, it results in reduced current consumption from the module. Connect VBUS to the VBUS_DETECT pin using a resistor divider, similar to the one in Fig. 3 shown below.

![Figure 3. Connecting VBUS to the VBUS_DETECT pin.](https://digilent.com/reference/_media/reference/programmers/jtag-smt3/fig-3.png?w=400&tok=9057b6)

------

## Application Examples

### Example 1: Interfacing a Zynq-7000

Figure 4 demonstrates how to connect the JTAG-SMT3-NC to Xilinx’s Zynq-7000 silicon. Please note that VCCO_0 and VCCO_MIO1 may be powered by the same supply or by different supplies. The PS_SRST_B pin of the SMT3-NC is driven by an open drain buffer and therefore an external open drain buffer is not required to add an optional reset button.

![Figure 4. Zynq application example.](https://digilent.com/reference/_media/reference/programmers/jtag-smt3/fig-4.png?w=800&tok=145b1c)

### Example 2: Interfacing a Zynq-7000 while retaining the Xilinx JTAG Header

Figure 5 below demonstrates how to connect the JTAG-SMT3-NC to Xilinx’s Zynq-7000 silicon alongside Xilinx’s 14-pin JTAG header. In this example, an open drain buffer allows both the SMT3-NC and Xilinx JTAG Header to drive the PS_SRST_B pin, which may operate a different voltage than the Zynq’s JTAG pins.

![Figure 5. Open drain buffer allowing the SMT3-NC and JTAG Header to drive the PS_SRST_B pin.](https://digilent.com/reference/_media/reference/programmers/jtag-smt3/fig-5.png?w=800&tok=a1ed6f)

------

## Supported Target Devices

The JTAG-SMT3-NC is capable of targeting the following Xilinx devices:

- Xilinx FPGAs, including UltraScale+
- Xilinx SoCs, MPSoCs, and RFSoCs, including Xilinx Zynq-7000 and Zynq UltraScale+
- Xilinx ACAPs, including Versal
- Xilinx CoolRunner™/CoolRunner-II CPLDs
- Xilinx Platform Flash ISP configuration PROMs¹, ²
- Select third-party SPI PROMs¹, ²
- Select third-party BPI PROMs¹, ²

The following devices **cannot** be targeted by the JTAG-SMT3-NC:

- Xilinx 9500/9500XL CPLDs
- Xilinx 1700 and 18V00 ISP configuration PROMs
- Xilinx FPGA eFUSE programming

Remote device configuration is not supported for the JTAG-SMT3-NC when used with Xilinx’s iMPACT software.

¹ — *Note: Please see the “Introduction to Indirect Programming – SPI or BPI Flash Memory” help topic in iMPACT for a list of supported FPGA/PROM combinations.*
² — *Note: Please see the “Configuration Memory Support” section of Xilinx UG908 for a list of the FPGA/PROM combinations that Vivado supports.*

### Programming Solutions Comparison Chart

|                                | JTAG-SMT3-NC            | JTAG-SMT2                | JTAG-SMT2-NC             |
| :----------------------------- | :---------------------- | :----------------------- | ------------------------ |
| Max Speed                      | 30 MHz                  | 30 MHz                   | 30 MHz                   |
| Voltage Range                  | 1.8V – 5V               | 1.8V – 5V                | 1.8V – 5V                |
| Xilinx Native Support          | ISE 14.1+ Vivado 2014.1 | ISE 14.1+ Vivado 2013.1+ | ISE 14.1+ Vivado 2013.1+ |
| Xilinx Plug-in Support         | ISE 13.1+               | ISE 13.1+                | ISE 13.1+                |
| Digilent Adept Support         | YES                     | YES                      | YES                      |
| PC Interface                   | USB                     | USB                      | USB                      |
| Onboard USB Connector          | YES                     | YES                      | NO                       |
| Host Board Connector Interface | 18-pad SMT              | 11-pad SMT               | 13-pad SMT               |
| 4-Wire JTAG                    | YES                     | YES                      | YES                      |
| 2-Wire JTAG                    | NO                      | YES                      | YES                      |
| Zynq-7000 PS_SRST Support      | YES                     | YES                      | YES                      |
| SPI Support                    | NO                      | YES                      | YES                      |
| Independent UART Channel       | YES                     | NO                       | NO                       |

------

## Pinout Table

| Pin Number | Pin Name  | Pin Number |  Pin Name   |
| :--------: | :-------: | :--------: | :---------: |
|     1      |    GND    |     10     |     TCK     |
|     2      | VREF_UART |     11     |     TDO     |
|     3      |    CTS    |     12     |     TDI     |
|     4      |    RTS    |     13     |     TMS     |
|     5      |    RXD    |     14     |     GND     |
|     6      |    TXD    |     15     |     VDD     |
|     7      |    GND    |     16     |   USB_DM    |
|     8      | VREF_JTAG |     17     |   USB_DP    |
|     9      | PS_SRST_B |     18     | VBUS_DETECT |

**Note:** Pin 9 on the silkscreen of the JTAG SMT3-NC may be incorrectly labeled as GND rather than the correct label of PS_SRST_B.

------

## Mechanical Information

![Figure 6. PCB spacing diagram.](https://digilent.com/reference/_media/reference/programmers/jtag-smt3/fig-6.png?w=800&tok=0591b6)

![Figure 7. PCB pin spacing diagram.](https://digilent.com/reference/_media/reference/programmers/jtag-smt3/fig-7.png?w=800&tok=2f6676)

------

## General USB Signal Routing Guidelines

- Maintain a differential impedance of 90 Ohms between the DP and DM signals.
- Keep DP and DM trace lengths within 50 mils of each other.
- Minimize DP and DM signal trace length. Keeping the trace length below 3 inches is recommended.
- When possible, route DP and DM on the plane closest to the ground plane.
- When possible, avoid routing the DP and DM signals through vias. If vias cannot be avoided, then keep them small and place the DP and DM traces on the same layer.
- When possible, avoid routing other traces near DP and DM.
- When possible, minimize or avoid the use of bends in the DP and DM traces. If 90 degree bends are necessary, then use two 45 degree turns or an arc instead of a single 90 degree turn.
- Do NOT route DP or DM near oscillators, crystals, switching regulators, clock generators, or inductors.

### Absolute Maximum Ratings

| Symbol                          | Parameter                                                    | Condition   | Min  | Max  | Unit |
| :------------------------------ | :----------------------------------------------------------- | :---------- | :--- | :--- | :--- |
| Vdd                             | Operating supply voltage                                     |             | -0.3 | 4.0  | V    |
| Vref                            | I/O reference/supply voltage                                 |             | -0.3 | 6    | V    |
| VIO                             | Signal Voltage                                               |             | -0.3 | 6    | V    |
| IIK,IOK                         | TMS, TCK, TDI, TDO, TXD, RXD, RTS, CTS, PS_SRST_B DC Input/Output Diode Current | VIO < -0.3V |      | -50  | mA   |
| VIO > 6V                        | +20                                                          |             |      |      |      |
| IOUT                            | DC Output Current                                            |             |      | ±50  | mA   |
| TSTG                            | Storage Temperature                                          |             | -10  | +60  | ºC   |
| ESD                             | Human Body Model JESD22-A114                                 |             | 4000 | V    |      |
| Charge Device Model JESD22-C101 |                                                              | 2000        | V    |      |      |

### DC Operating Characteristics

| Symbol                  | Parameter                         | Min         | Typ         | Max   | Unit  |
| :---------------------- | :-------------------------------- | :---------- | :---------- | :---- | :---- |
| Vdd                     | Operating supply voltage          | 2.97        | 3.3         | 3.63  | Volts |
| VREF_JTAG               | JTAG I/O reference/supply voltage | 1.65        | 3.3         | 5.5   | Volts |
| VREF_UART               | UART I/O reference/supply voltage | 1.65        | 3.3         | 5.5   | Volts |
| TDO, RXD, CTS           | Input High Voltage (VIH)          | 0.75 x Vref |             | 5.5   | Volts |
| Input Low Voltage (VIL) | 0                                 |             | 0.55        | Volts |       |
| VBUS_DETECT             | Input High Voltage (VIH)          | 2.0         |             | Vdd   | Volts |
| Input Low Voltage (VIL) | 0                                 |             | 0.8         | Volts |       |
| TMS, TCK, TDI           | Output High (VOH)                 | 0.78 x Vref | 0.95 x Vref | Vref  | Volts |
| Output Low (VOL)        | 0                                 | 0.05 x Vref | 0.55        | Volts |       |
| TXD, RTS                | Output High (VOH)                 | 0.75 x Vref |             | Vref  | Volts |
| Output Low (VOL)        | 0                                 |             | 0.55        | Volts |       |
| PS_SRST_B               | Output Low (VOL)                  | 0           |             | 0.55  | Volts |
| TA                      | Operating Temperature             | -40         |             | 85    | ºC    |

------

## AC Operating Characteristics

The JTAG-SMT3-NC’s JTAG signals operate according to the timing diagram in Fig. 7. The SMT3-NC supports JTAG/TCK frequencies from 30 MHz to 8 KHz at integer divisions of 30 MHz from 1 to 3750. Common frequencies include 30 MHz, 15 MHz, 10 Mhz, 7.5 MHz, and 6 MHz (see Table 2). The JTAG/TCK operating frequency can be set within the Xilinx tools.

*Note: Please refer to Xilinx’s iMPACT documentation for more information.*

![Figure 8. Timing diagram.](https://digilent.com/reference/_media/reference/programmers/jtag-smt3/fig-8.png?w=800&tok=1b0e6c)

------

## Mounting to Host PCBs

The JTAG-SMT3-NC module has a moisture sensitivity level (MSL) of 6. Prior to reflow, the JTAG-SMT3-NC module must be dried by baking it at 70° C for 72 hours (the tray and the module itself can be baked 125° C for 24 hours, but any labels and rubber feet present on the module cannot withstand this higher temperature). Once this process has been completed, the module has a MSL of 3 and is suitable for reflow for up to 168 hours without additional drying.

The factory finishes the JTAG-SMT3-NC signal pads with the ENIG process using 2u” gold over 150u” electroless nickel. This makes the SMT3-NC compatible with most mounting and reflow processes (see Fig. 8). The binding force of the solder is sufficient to hold the SMT3-NC firmly in place, so mounting should require no additional adhesives.

![Figure 9. JTAG-SMT3-NC reflow temperature over time.](https://digilent.com/reference/_media/reference/programmers/jtag-smt3/fig-9.png?w=800&tok=8363c4)

------

## Packaging

Digilent ships quantities under 40pcs individually packaged in antistatic bags with MSL 6. Digilent will pack and ship larger quantities in groups of 40 positioned in an antistatic bake tray with MSL 3 (see Fig. 10). Trays will be packaged in an anti-static vacuum sealed bag. We also offer to bake them before shipping for an additional cost per 40pc lot.

![Figure 10. JTAG-SMT3-NC shipping arrangement.  ](https://digilent.com/reference/_media/reference/programmers/jtag-smt3/fig-10.png?w=400&tok=975039)