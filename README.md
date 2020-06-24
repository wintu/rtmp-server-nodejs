# RTMP-Server

[![npm](https://img.shields.io/npm/v/rtmp-server.svg)](https://npmjs.org/package/rtmp-server)
[![npm](https://img.shields.io/npm/dm/rtmp-server.svg)](https://npmjs.org/package/rtmp-server)
[![npm](https://img.shields.io/npm/l/rtmp-server.svg)](LICENSE)

A Node.js implementation of RTMP Server 
 - Supports only RTMP protocol.
 - Supports only H.264 video and AAC audio.
 
# Install

```bash
npm install --save rtmp-server
```
 
# Usage 
```js
const RtmpServer = require('rtmp-server');
const rtmpServer = new RtmpServer();

rtmpServer.on('error', err => {
  throw err;
});

rtmpServer.on('client', client => {
  //client.on('command', command => {
  //  console.log(command.cmd, command);
  //});

  client.on('connect', () => {
     console.log('connect', client.app);
  });
  
  client.on('play', ({ streamName }) => {
    console.log('PLAY', streamName);
  });
  
  client.on('publish', ({ streamName }) => {
    console.log('PUBLISH', streamName);
  });
  
  client.on('endPublish', () => {
    console.log('publish client disconnected');
  });

  client.on('endPlay', () => {
    console.log('play client disconnected');
  });
});

rtmpServer.listen(1935);
```

You can now publish streams to `rtmp://localhost:1935/live` and use any unique stream key.

The stream will then be available at `rtmp://localhost:1935/<your stream key>`.


# License

[GPL-2.0](LICENSE)
