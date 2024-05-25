# Fix Sonoff with Hue disconnecting
A simple docker file that requests a rescan of the lights in the HUE Bridge API from time to time.
This avoid the issue where the sonoff lights are disconnected and unreachable. 
Quite a dumb way to do it but works.
For it to work you need the API Key of your hue bridge and it's IP adress.
Works on Synology Container manager as well.
https://developers.meethue.com/develop/get-started-2/


**You need to modify the schedule file with your api key and IP**

If needed a python script created by our good old friend ChatGPT


### URL to Request
```
http://<bridge_ip_address>/api/<username>/lights
```

- `<bridge_ip_address>`: The IP address of your Philips Hue Bridge.
- `<username>`: The username you use to authenticate with the Hue Bridge API.

### Type of Request
- **POST**

### Example URL
If your bridge IP address is `192.168.1.2` and your username is `your-username`, the URL would look like this:
```
http://192.168.1.2/api/your-username/lights
```

### How to Make the Request
You can use various tools to make this POST request, such as `curl` in the command line, Postman for a GUI approach, or within a script or program using an HTTP client.

#### Using `curl`
Here is an example of how you can do it using `curl`:

```sh
curl -X POST http://192.168.1.2/api/your-username/lights
```

#### Using Python
If you prefer using Python, you can make this POST request using the `requests` library:

```python
import requests

bridge_ip = '192.168.1.2'
username = 'your-username'
url = f'http://{bridge_ip}/api/{username}/lights'

response = requests.post(url)

print(response.json())
```

### Response
The response from the bridge will include a status indicating whether the scan for new lights was started successfully.

### Example Response
A typical response might look like this:
```json
[{"success":{"/lights": "Searching for new devices"}}]
```

This indicates that the bridge has started scanning for new lights.