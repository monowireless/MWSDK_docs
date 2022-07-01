---
title: TwePacketPAL
author: "Mono Wireless Inc."
---

# TwePacketPAL

The `TwePacketPal` class interprets TWELITE PAL packet data. This class handles TWELITE PAL (sensor data and other upstream data) commonly.

```cpp
class TwePacketPal : public TwePacket, public DataPal { ... };
```



PAL common data is defined in `DataPal`.

Generator functions are provided to retrieve data specific to each PAL sensor board.



### DataPal structure

Although the packet data structure of PAL differs depending on the connected sensors, etc., `DataPal` holds the data structure of the common part.

```cpp
struct DataPal {
	uint8_t u8lqi; // LQI value

	uint32_t u32addr_rpt; // address of the relay

	uint32_t u32addr_src; // source address
	uint8_t u8addr_src; // source logical address

	uint16_t u16seq; // sequence number

	E_PAL_PCB u8palpcb; // PAL board type
	uint8_t u8palpcb_rev; // Revision of PAL board
	uint8_t u8sensors; // Number of sensor data in the data (MSB=1 is an error)
	uint8_t u8snsdatalen; // sensor data length (in bytes)

	union {
		const uint8_t *au8snsdata; // reference to sensor data part
		uint8_t _pobj[MWX_PARSER_PKT_APPPAL_FIXED_BUF]; // each sensor object
	};
};
```

The PAL packet data structure consists of two blocks: the common part for all PALs and the individual data part. The individual data part does not interpret the packet, but stores it as is. To simplify handling, data exceeding 32 bytes is stored in dynamically allocated `uptr_snsdata`.

The individual data parts are stored in a structure whose base class is `PalBase`. This structure is generated by the generator function defined in `TwePacketPal`.

If the size fits in `MWX_PARSER_PKT_APPPAL_FIXED_BUF` when `parse<TwePacketPAL>()` is executed, a separate sensor object is generated.

If it does not fit, a reference to the byte sequence used for analysis is stored in `au8snsdata`. In this case, if the data in the byte string used for analysis is rewritten, sensor-specific objects cannot be generated.



### PalBase

All data structures for each sensor in PAL inherit from `PalBase`. The sensor data storage status `u32StoredMask` is included.

```cpp
	struct PalBase {
		uint32_t u32StoredMask; // Data acquisition flags used internally
	};
```

### PalEvent

PAL events are information that is sent when certain conditions are met by processing sensor information, rather than directly from sensors. For example, when an acceleration sensor detects a certain level of acceleration from a stationary state.

```cpp
	struct PalEvent {
		uint8_t b_stored; // true if stored
		uint8_t u8event_source; // spare
		uint8_t u8event_id; // event ID
		uint32_t u32event_param;// event parameter
	};
```

If event data exists, it can be determined by `.is_PalEvent()` of `TwePacketPal` being `true`, and `.get_PalEvent()` will yield a `PalEvent` data structure.



## Generator functions

Generator functions are used to extract various types of data from sensor PAL.

```cpp
void print_pal(pktparser& pkt) {
	auto&& pal = pkt.use<TwePacketPal>();
	if (pal.is_PalEvent()) {
		PalEvent obj = pal.get_PalEvent();
	} else
	switch(pal.u8palpcb) {
	case E_PAL_PCB::MAG:
	  {
		  // generate pal board specific data structure.
		  PalMag obj = pal.get_PalMag();
	  } break;
  case E_PAL_PCB::AMB:
	  {
		  // generate pal board specific data structure.
		  PalAmb obj = pal.get_PalAmb();
	  } break;
	  ...
	default: ;
	}
}
```

To use the generator function, first determine if `pkt` is an event (`.is_PalEvent()`). If it is an event, it has `get_PalEvent()`. Otherwise, it creates an object according to `u8palpcb`.



### get\_PalMag()

```cpp
PalMag get_PalMag()

// MAG
struct PalMag : public PalBase {
    uint16_t u16Volt; // module voltage [mV]
    uint8_t u8MagStat; // state of magnetic switch [0:no magnet,1,2].
    uint8_t bRegularTransmit; // MSB flag of u8MagStat
};
```

If `.u8palpcb==E_PAL_PCB::MAG`, the data `PalMag` of the open/close sensor pal is taken.



### get\_PalAmb()

```cpp
PalAmb get_PalAmb()

// AMB
struct PalAmb : public PalBase {
    uint16_t u16Volt; // module voltage [mV]
    int16_t i16Temp; // temperature (100x value)
    uint16_t u16Humd; // humidity (100x value)
    uint32_t u32Lumi; // illuminance (equivalent to Lux)
};
```

If `.u8palpcb==E_PAL_PCB::AMB`, the data `PalAmb` of the environmental sensor pal is taken.



### get\_PalMot()

```cpp
PalMot get_PalMot()

// MOT
struct PalMot : public PalBase {
    uint16_t u16Volt; // module voltage [mV]
    uint8_t u8samples; // number of samples
    uint8_t u8sample_rate_code; // sample rate (0: 25Hz, 4:100Hz)
    int16_t i16X[16]; // X axis
    int16_t i16Y[16]; // Y axis
    int16_t i16Z[16]; // Z axis
};
```

If `.u8palpcb==E_PAL_PCB::MOT`, the data `PalMot` of the operating sensor pal is taken.



### get\_PalEvent()

```cpp
PalEvent get_PalEvent()

// PAL event
struct PalEvent {
    uint8_t b_stored; // if true, event information is available
    uint8_t u8event_source; // event source
    uint8_t u8event_id; // event ID
    uint32_t u32event_param; // 24bit, event parameter
};
```

Extracts a `PalEvent` (PAL event) if `.is_PalEvent()` is `true`.
