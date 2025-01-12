---
Category: Building
order: 4
title: How to check for electrical compatibility?
id: compatibleElectrically
answer: >-
  We're lucky that a lot of the stuff out there is compatible and standardized,
  but there are also some exceptions and weird off-spec things. As long as you
  read carefully, you should be fine. As compatibility is hard to get in a
  single answer, they have been split


  ##### Electronic compatibility:


  * There are mainly two things you should look out for. Accepted voltage/current levels, and signal communication

  * ##### Voltage and Current:

    * Most electronic parts used have a rated minimal and maximal accepted voltage. This can be as simple as a camera taking in 5V or a VTX having an accepted voltage range of 7-36V, or on flight controllers/ESCs where it's often listed as a cell count. Small AIOs might take 1s only, 1-2s, or 2s up to 6s, which is also the most common rating for 5" quad parts. Overvolting can at best result in something failing in a non-damaging way, **at worst it'll cause a fire**
    * Current ratings come into play with both FCs and ESCs for the max current. In ESCs, this is the max current the FETs will let through, on FCs it's how much current each voltage regulator can handle: 
    * Your ESC's current rating is measured for **each motor**, so a 40A 4in1 ESC has 4x 40A outputs. Motor manufacturers should list the max current draw for the motors, and it's usually not hard to find. It's always good to have some overhead allowed current on the ESC: For a tinywhoop, this can be as low as an extra 1A, for other micro quads it's about 3-10A, and on a 5" you want *at least* a 10A overhead from the rated max current draw of the motor
    * All FCs should have at least a 5V regulator (sometimes an additional 4.5V output, signifying that it will output USB power), to power most peripheral devices. 3.3V for the MCU, and some lower-power devices, and usually a 9/10/12V regulator for your VTX. Each of those has its own current rating. Usually 0.3-0.5A for 3.3V, 1-2A for 5V, and 1-2A for the "VTX" output. In most cases, this should be plenty, but if you attach a lot of devices or your FC's regulators are weak enough, this can overload it and make some stages not work properly
  * ##### Signal communication:

    * All peripherals transmit and receive data in one way or another. Be that over UART (serial), I2C, SPI, or some other way of transmission. 
    * Receivers transmit and receive signals in two ways. Over the **air**, and over the **wire**. The air protocol dictates compatibility between radio and receiver, they need to match (in systems that use the same protocol over different frequencies, like ELRS 2.4GHz and 900MHz, the frequency also has to match). The wire protocol is over UART. For example, ELRS, Tracer, and Crossfire all use a pair of **RX** and **TX** pads (which should be accessible on any FC) and the CRSF protocol, which is supported by all modern systems

      ![connection diagram for an ELRS receiver](/uploads/flywoo_elrs_rx.png)
    * A GPS will also use a UART, also needing a free set of RX+TX pads. Some GPS units also have an integrated compass (you can also get them standalone) that will need I2C communication. This uses two pads, **Data**, and **Clock,** usually labeled **SDA** and **SCL** on the FC

      ![connection diagram for a gps unit](/uploads/flywoo_gps_compass.png)
---
