# uio-test-system
UIO example system using AXI GPIO with connected PL to PS interrupt

An additional key-value pair needs to be added to the Linux boot arguments. This can be done by adding the kv pair to the bootargs line in the uEnv.txt file in the BOOT partition. The value will match the compatible string in the device tree node for the UIO device.

```
uio_pdrv_genirq.of_id=krtkl,generic-uio,ui_pdrv
```

The device tree node with bindings for UIO will contain one or more memory regions specified by the reg property. The interrupt associated with the device should be specified by in the interrupts property. In this example, IRQ 61 (IRQF2P[0]) is connected to the AXI GPIO interrupt. The interrupt ID is offset by 32 for the device tree bindings (29 + 32 = 61)

```
axi_gpio0: gpio@41200000 {
	reg = <0x41200000 0x10000>;
	compatible = "krtkl,generic-uio,ui_pdrv";
	interrupt-parent = <&intc>;
	interrupts = <0 29 4>;
};
```
