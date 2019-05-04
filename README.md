# signalr-client-py

Python client proxy for [SignalR](http://signalr.net/).

# Major difference with the origin signalr-client

OneBet sometimes send json object that would error out the connection. Add try out in _handle_notification


New _transport.py (Just ignore that message if it cant load it)
```
    def _handle_notification(self, message):
        if len(message) > 0:
            try:
                data = json.loads(message)
                self._connection.received.fire(**data)
            except Exception as e:
                print(str(datetime.datetime.now())+': Json decode error: ' + str(e))
        gevent.sleep()
```

Old _transport.py
```
    def _handle_notification(self, message):
        if len(message) > 0:
            data = json.loads(message)
            self._connection.received.fire(**data)
        gevent.sleep()

```
