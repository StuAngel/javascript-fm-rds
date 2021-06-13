# FM-RDS
a simple implementation of FM RDS in Javascript, 

I am currently working with a USB FM tuner and required the use of the "Radio Data System", this is what displays the current station and misc text they broadcast, I also see timestamp and application data but have not implemented those interfaces

usage

var rdsObject = new rds();\
/*\
&nbsp;&nbsp;Sender is the RDS object itself\
&nbsp;&nbsp;Text is the text that has just been modified\
&nbsp;&nbsp;Target:\
&nbsp;&nbsp;&nbsp;&nbsp;text - text sent by the station, may include weather reports etc.\
&nbsp;&nbsp;&nbsp;&nbsp;station - normally the name of the radio station\
*/

/* Update function will only be called on an actual change to the text */\
rdsObject.onUpdate(function(sender, text, target){ console.log(target+": "+text); });

in the callback of the RDS request on the USB device

in my case

setInterval(function()\
{\
&nbsp;&nbsp;usbdevice.put(this.put([0x03, tuner_band.FM, 0x82, 0x01, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00], function()\
&nbsp;&nbsp;{\
&nbsp;&nbsp;&nbsp;&nbsp;/* arguments[1] being an array of uShort representing Group A, Group B, Group C, Group D */\
&nbsp;&nbsp;&nbsp;&nbsp;rdsObject._rds.analyseframes(arguments[1]);\
&nbsp;&nbsp;});\
}, 50);
