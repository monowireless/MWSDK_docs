# Table of contents

* [TWELITE SDK (MWSDK) manual](README.md)
* [Introduction](overview/README.md)
  * [TWELITE SDK Terms of Use](overview/policy.md)
  * [Support and response](overview/support.md)
  * [Mono Wireless Software License Agreement](overview/mwsla.md)
  * [Structure of TWELITE SDK](overview/sdk_structure.md)
* [Get the latest version](latest/README.md)
  * [TWELITE SDK revision history](latest/sdk_changes.md)
* [How to use TWELITE SDK](twelite-sdk-howto/README.md)
  * [Install TWELITE SDK (MWSDK)](twelite-sdk-howto/twelite-sdk-howtoinsutru.md)
  * [Use with VSCode](twelite-sdk-howto/vscode-deno.md)
  * [folder structure](twelite-sdk-howto/derekutori.md)
  * [How to build from the command line](twelite-sdk-howto/komandoraindenobirudo.md)
  * [About build definitions](twelite-sdk-howto/birudonitsuite/README.md)
    * [About Makefile](twelite-sdk-howto/birudonitsuite/makefile-nitsuite.md)
    * [about Version.mk](twelite-sdk-howto/birudonitsuite/versionmk-nitsuite.md)
    * [bin file naming conventions](twelite-sdk-howto/birudonitsuite/binfuiru.md)
  * [program firmware](twelite-sdk-howto/fumuua/README.md)
    * [Wiring for firmware programming](twelite-sdk-howto/fumuua/fumuua.md)
    * [tweterm.py](twelite-sdk-howto/fumuua/tweterm.py.md)
* [TWELIET NET API overview](twelite-net-api-expl/README.md)
  * [Terms](twelite-net-api-expl/yong-yu.md)
  * [TWELITE NET  library structure](twelite-net-api-expl/twelite-net-raiburari.md)
  * [TWENET working flow](twelite-net-api-expl/twenet-fur/README.md)
    * [flow: System start-up](twelite-net-api-expl/twenet-fur/fur.md)
    * [flow: Main loop](twelite-net-api-expl/twenet-fur/meinrpufur.md)
    * [flow: Wireless events](twelite-net-api-expl/twenet-fur/fur-1.md)
    * [flow: Hardware interrupts/events](twelite-net-api-expl/twenet-fur/hdouafur.md)
    * [flow: User-defined event processing function](twelite-net-api-expl/twenet-fur/yzaibentofur.md)
  * [Structure of the source code](twelite-net-api-expl/ssukdono.md)
  * [Modules](twelite-net-api-expl/mojru.md)
  * [Wireless packets](twelite-net-api-expl/paketto/README.md)
    * [Maximum packet length](twelite-net-api-expl/paketto/pakettono.md)
    * [Addressing conventions](twelite-net-api-expl/paketto/adoresuno.md)
    * [Application ID](twelite-net-api-expl/paketto/apurikshonid.md)
  * [About the network](twelite-net-api-expl/nettowkunitsuite/README.md)
    * [SimpleNet](twelite-net-api-expl/nettowkunitsuite/netto/README.md)
      * [Transmit](twelite-net-api-expl/nettowkunitsuite/netto/song-xin.md)
      * [Receive](twelite-net-api-expl/nettowkunitsuite/netto/shou-xin.md)
    * [RelayNet](twelite-net-api-expl/nettowkunitsuite/netto-1/README.md)
      * [Implementation of the parent  device](twelite-net-api-expl/nettowkunitsuite/netto-1/no.md)
      * [Implementation of repeaters](twelite-net-api-expl/nettowkunitsuite/netto-1/no-1.md)
      * [Implementing a child device (MININODES)](twelite-net-api-expl/nettowkunitsuite/netto-1/no-mininodes.md)
      * [NB beacon system connection](twelite-net-api-expl/nettowkunitsuite/netto-1/nbbkonno.md)
      * [Address of the relay network](twelite-net-api-expl/nettowkunitsuite/netto-1/nettonoadoresu.md)
      * [Static relay with fixed host address](twelite-net-api-expl/nettowkunitsuite/netto-1/adoresuwoshita.md)
* [TWELITE NET API references](twelite-net-api-ref/README.md)
  * [The callback functions](twelite-net-api-ref/krubakku/README.md)
    * [cbAppColdStart()](twelite-net-api-ref/krubakku/cbappcoldstart.md)
    * [cbAppWarmStart()](twelite-net-api-ref/krubakku/cbappwarmstart.md)
    * [cbToCoNet_vMain()](twelite-net-api-ref/krubakku/cbtoconet_vmain.md)
    * [cbToCoNet_vRxEvent()](twelite-net-api-ref/krubakku/cbtoconet_vrxevent.md)
    * [cbToCoNet_vTxEvent()](twelite-net-api-ref/krubakku/cbtoconet_vtxevent.md)
    * [cbToCoNet_vNwkEvent()](twelite-net-api-ref/krubakku/cbtoconet_vnwkevent.md)
    * [cbToCoNet_vHwEvent()](twelite-net-api-ref/krubakku/cbtoconet_vhwevent.md)
    * [cbToCoNet_u8HwInt()](twelite-net-api-ref/krubakku/cbtoconet_u8hwint.md)
  * [TWELITE NET functions](twelite-net-api-ref/twelite-net-guan-shu/README.md)
    * [ToCoNet_vMacStart()](twelite-net-api-ref/twelite-net-guan-shu/toconet_vmacstart.md)
    * [ToCoNet_bMacTxReq()](twelite-net-api-ref/twelite-net-guan-shu/toconet_bmactxreq.md)
    * [ToCoNet_u32GetSerial()](twelite-net-api-ref/twelite-net-guan-shu/toconet_u32getserial.md)
    * [ToCoNet_u32GetRand()](twelite-net-api-ref/twelite-net-guan-shu/toconet_u32getrand.md)
    * [ToCoNet_vSleep()](twelite-net-api-ref/twelite-net-guan-shu/toconet_vsleep.md)
    * [ToCoNet_vDebugInit()](twelite-net-api-ref/twelite-net-guan-shu/toconet_vdebuginit.md)
    * [ToCoNet_vDebugLevel()](twelite-net-api-ref/twelite-net-guan-shu/toconet_vdebuglevel.md)
    * [ToCoNet_u32GetVersion()](twelite-net-api-ref/twelite-net-guan-shu/toconet_u32getversion.md)
    * [ToCoNet_bRegisterAesKey()](twelite-net-api-ref/twelite-net-guan-shu/toconet_bregisteraeskey.md)
    * [ToCoNet_vRfConfig()](twelite-net-api-ref/twelite-net-guan-shu/toconet_vrfconfig.md)
    * [ToCoNet_vChConfig()](twelite-net-api-ref/twelite-net-guan-shu/toconet_vchconfig.md)
    * [ToCoNet_Tx_vProcessEventQueue()](twelite-net-api-ref/twelite-net-guan-shu/toconet_tx_vprocesseventqueue.md)
    * [ToCoNet_u16RcCalib()](twelite-net-api-ref/twelite-net-guan-shu/toconet_u16rccalib.md)
  * [RelayNet API](twelite-net-api-ref/netto-api/README.md)
    * [functions](twelite-net-api-ref/netto-api/sys_callbacks/README.md)
      * [ToCoNet_Nwk_bInit()](twelite-net-api-ref/netto-api/sys_callbacks/toconet_nwk_binit.md)
      * [ToCoNet_Nwk_bStart()](twelite-net-api-ref/netto-api/sys_callbacks/toconet_nwk_bstart.md)
      * [ToCoNet_Nwk_bPause()](twelite-net-api-ref/netto-api/sys_callbacks/toconet_nwk_bpause.md)
      * [ToCoNet_Nwk_bResume()](twelite-net-api-ref/netto-api/sys_callbacks/toconet_nwk_bresume.md)
      * [ToCoNet_Nwk_bTx()](twelite-net-api-ref/netto-api/sys_callbacks/toconet_nwk_btx.md)
    * [Structure](twelite-net-api-ref/netto-api/structure/README.md)
      * [tsTxDataApp (relay net)](twelite-net-api-ref/netto-api/structure/tstxdataapp-netto.md)
      * [tsRxDataApp (relay net)](twelite-net-api-ref/netto-api/structure/tsrxdataapp-netto.md)
      * [tsToCoNet_Nwk_Context](twelite-net-api-ref/netto-api/structure/tstoconet_nwk_context.md)
    * [LayerTree net](twelite-net-api-ref/netto-api/layertree-netto/README.md)
      * [ToCoNet_NwkLyTr_psConfig()](twelite-net-api-ref/netto-api/layertree-netto/toconet_nwklytr_psconfig.md)
      * [ToCoNet_NwkLyTr_psConfig_MiniNodes()](twelite-net-api-ref/netto-api/layertree-netto/toconet_nwklytr_psconfig_mininodes.md)
      * [tsToCoNet_NwkLyTr_Context](twelite-net-api-ref/netto-api/layertree-netto/tstoconet_nwklytr_context.md)
  * [typedef, frequently used macros](twelite-net-api-ref/typedef-yokuumakuro.md)
  * [Structures](twelite-net-api-ref/gou-zao-ti/README.md)
    * [sToCoNet_AppContext](twelite-net-api-ref/gou-zao-ti/stoconet_appcontext.md)
    * [tsRxDataApp](twelite-net-api-ref/gou-zao-ti/tsrxdataapp.md)
    * [tsTxDataApp](twelite-net-api-ref/gou-zao-ti/tstxdataapp.md)
  * [TWELITE NET macros](twelite-net-api-ref/twelite-net-makuro/README.md)
    * [ToCoNet_REG_MOD_ALL()](twelite-net-api-ref/twelite-net-makuro/toconet_reg_mod_all.md)
    * [utils.h](twelite-net-api-ref/twelite-net-makuro/utils.h.md)
  * [User defined event handling functions](twelite-net-api-ref/yzaibento/README.md)
    * [State](twelite-net-api-ref/yzaibento/sutto.md)
    * [Events](twelite-net-api-ref/yzaibento/ibento.md)
    * [ToCoNet_Event API](twelite-net-api-ref/yzaibento/toconet_event-api/README.md)
      * [ToCoNet_Event_Register_State_Machine()](twelite-net-api-ref/yzaibento/toconet_event-api/toconet_event_register_state_machine.md)
      * [ToCoNet_Event_Process()](twelite-net-api-ref/yzaibento/toconet_event-api/toconet_event_process.md)
      * [ToCoNet_Event_SetState()](twelite-net-api-ref/yzaibento/toconet_event-api/toconet_event_setstate.md)
      * [ToCoNet_Event_vKeepStateOnRamHoldSleep()](twelite-net-api-ref/yzaibento/toconet_event-api/toconet_event_vkeepstateonramholdsleep.md)
      * [ToCoNet_Event_u32TickFrNewState()](twelite-net-api-ref/yzaibento/toconet_event-api/toconet_event_u32tickfrnewstate.md)
  * [Module library](twelite-net-api-ref/mojru-raiburari/README.md)
    * [ENERGY SCAN](twelite-net-api-ref/mojru-raiburari/energy-scan.md)
    * [NB SCAN](twelite-net-api-ref/mojru-raiburari/nb-scan.md)
  * [PRSEV library](twelite-net-api-ref/prsev-raiburari.md)
  * [global variables](twelite-net-api-ref/gurbaru/README.md)
    * [uint32 u32TickCount_ms](twelite-net-api-ref/gurbaru/uint32-u32tickcount_ms.md)
    * [sToCoNet_AppContext (static variable)](twelite-net-api-ref/gurbaru/stoconetappcontext-jing-de-bian-shu.md)
  * [PANIC](twelite-net-api-ref/panic.md)
* [HW API reference](hw-api-ref/README.md)
  * [Peripherals](hw-api-ref/perifuraru/README.md)
    * [ADC](hw-api-ref/perifuraru/adc/README.md)
      * [adc.c](hw-api-ref/perifuraru/adc/adc.c.md)
    * [DIO](hw-api-ref/perifuraru/dio.md)
    * [TickTimer](hw-api-ref/perifuraru/ticktimer.md)
    * [UART](hw-api-ref/perifuraru/uart/README.md)
      * [SERIAL library](hw-api-ref/perifuraru/uart/serial-raiburari/README.md)
        * [SERIAL_vInit()](hw-api-ref/perifuraru/uart/serial-raiburari/serial_vinit.md)
        * [SERIAL_vInitEx()](hw-api-ref/perifuraru/uart/serial-raiburari/serial_vinitex.md)
        * [SERIAL_bRxQueueEmpty()](hw-api-ref/perifuraru/uart/serial-raiburari/serial_brxqueueempty.md)
        * [SERIAL_i16RxChar()](hw-api-ref/perifuraru/uart/serial-raiburari/serial_i16rxchar.md)
        * [SERIAL_vFlush()](hw-api-ref/perifuraru/uart/serial-raiburari/serial_vflush.md)
        * [tsSerialPortSetup](hw-api-ref/perifuraru/uart/serial-raiburari/tsserialportsetup.md)
        * [tsUartOpt](hw-api-ref/perifuraru/uart/serial-raiburari/tsuartopt.md)
      * [fprintf library](hw-api-ref/perifuraru/uart/fprintf-raiburari/README.md)
        * [vfPrintf()](hw-api-ref/perifuraru/uart/fprintf-raiburari/vfprintf.md)
        * [vPutChar()](hw-api-ref/perifuraru/uart/fprintf-raiburari/vputchar.md)
        * [tsFILE](hw-api-ref/perifuraru/uart/fprintf-raiburari/tsfile.md)
    * [Timer](hw-api-ref/perifuraru/timer/README.md)
      * [Timer library](hw-api-ref/perifuraru/timer/timerraiburari/README.md)
        * [vTimerConfig()](hw-api-ref/perifuraru/timer/timerraiburari/vtimerconfig.md)
        * [vTimerStart()](hw-api-ref/perifuraru/timer/timerraiburari/vtimerstart.md)
        * [vTimerStop()](hw-api-ref/perifuraru/timer/timerraiburari/vtimerstop.md)
        * [vTimerDisable()](hw-api-ref/perifuraru/timer/timerraiburari/vtimerdisable.md)
        * [tsTimerContext](hw-api-ref/perifuraru/timer/timerraiburari/tstimercontext.md)
    * [WakeTimer](hw-api-ref/perifuraru/waketimer.md)
    * [I2C](hw-api-ref/perifuraru/i2c.md)
    * [SPI](hw-api-ref/perifuraru/spi.md)
  * [Flash, EEPROM](hw-api-ref/flash-eeprom/README.md)
    * [EEPROM](hw-api-ref/flash-eeprom/eeprom.md)
    * [Flash](hw-api-ref/flash-eeprom/flash.md)
* [Utils references, others.](utils-ref/README.md)
  * [ByteQueue](utils-ref/bytequeue.md)
  * [u8CCITT8()](utils-ref/u8ccitt8.md)
  * [SPRINTF library](utils-ref/sprintfraiburari.md)
  * [BTM library (consecutive reading) DIO input](utils-ref/btmraiburari-dio.md)
