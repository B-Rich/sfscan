
# Net scan

* scan port
* scan ip

## Installation

```shell
npm install -g sfscan
```

## CLI

```shell
npm test
```

```shell
sfscan -h andmeics.com -r 1~65535
```

Output:

```shell
scan host: andmeics.com ports 1~65535
port 80 is open
scanning [                    ] 0% 1/65535  port 443 is open
scanning [                    ] 1% 812/65535
scanning [==                  ] 12% 7803/65535
scanning [====================] 100% 65535/65535  
ports scan: 331442.883ms
open ports: [ 80, 443 ]
```

## Example

### Range scan
```javascript
var scan = require('sfscan');

console.time('ports scan');
scan.port({
	host: 'andmeics.com',
	start: 1,
	end: 65535,
	timeout: 2000,
	queue: 1000
}, function(err, result) {    
	console.timeEnd('ports scan');
	console.log('open ports:', result);
});
```

Output

```shell
port 80 is open
scanning [                    ] 0% 1/65535  port 443 is open
scanning [                    ] 1% 812/65535
scanning [==                  ] 12% 7803/65535
scanning [====================] 100% 65535/65535
ports scan: 331442.883ms
open ports: [ 80, 443 ]
```

### Ports scan
```javascript
var scan = require('sfscan');

console.time('ports scan');
scan.port({
	host: 'github.com',
	ports: [20, 21, 22, 80, 443, 3306, 8580, 27017],
	timeout: 2000
}, function(err, result) {    
	console.timeEnd('ports scan');
	console.log('open ports:', result);
});

```

Output

```shell
ports scan: 121442.983mss
open ports: [ 80, 443, ]
```

### Listener
```javascript
console.time('ports scan');
scan.port({
		host: 'andmeics.com',
		start: 1,
		end: 65535,
		timeout: 2000,
		queue: 1000
	})
	.on('open', function(port) {
		console.log('found port open', port);
	})
	.on('end', function(port) {
		console.timeEnd('ports scan');
		console.log('scan port over');
	});

```

Output

```shell
found port open 80
found port open 443
ports scan: 2243ms
scan port over
```
