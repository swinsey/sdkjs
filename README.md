### Description
 Javascript SDK for Snowem service. For more detail, please check [here](https://docs.snowem.io).

### SDK Loading and Initialization
The following snippet will load SnowSDK javascript. If you host your snowsdk.js yourself, change the path to it accordingly.  

```
(function(d){
  var js, id = 'snowsdk', ref = d.getElementsByTagName('script')[0];
  if (d.getElementById(id)) {return;}
  js = d.createElement('script'); js.id = id; js.async = true;
  js.src = "<path-to>/snowsdk.js";
  ref.parentNode.insertBefore(js, ref);
}(document));

window.snowAsyncInit = function() {
   var config = { 
      'ip': "your-wss-ip",
      'port': 443 
   };  
   SnowSDK.init(config);

   //start your code here
   console.log("start your app here");
   start_app();
}
```

When SnowSDK is loaded, it invokes _snowAsyncInit_ if it is defined. Once it is called, you can initlialize SnowSDK with _init_ function. The _init_ function requires domain name or ip address of Snowem Websocket Service.

### Example Usage

**Create Peer Agent**
```
var config = {
   'wss_ip': "snowem.example.com",
   'wss_port': 443,
}
var peer = new SnowSDK.PeerAgent(config);
```

**Publish A Stream**
```
var settings = { 
   'channelid': peer.channelId, 
   'local_video_elm': document.getElementById('localVideo')
};  
peer.onAddPeerStream = function(info) {
  console.log("peerid: ", info.peerid);
  //make use of remote stream
  //remote_video_elm.srcObject = info.stream;
}
peer.onRemovePeerStream = function(info) {
  console.log("removing stream from peerid: " + info.peerid);
}
peer.publish(settings);
```
**Play A Stream**
```
var config = { 
   'channelid': peer.channelId,
   'remote_video_elm': document.getElementById('remoteVideo')
};  
peer.onAddPeerStream = function(info) {
  console.log("peerid: ", info.peerid);
  //make use of remote stream
  //remote_video_elm.srcObject = info.stream;
}
peer.onRemovePeerStream = function(info) {
  console.log("removing stream from peerid: " + info.peerid);
}
peer.play(config);
```


