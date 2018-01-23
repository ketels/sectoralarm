# Sector Alarm Node.js Library

## Information
A simple Node.js library to check the status and history of Swedish Sector Alarm sites. Library also includes a notify functionality that executes a callback as the alarm status changes. This library uses https://minasidor.sectoralarm.se, and is intended for Swedish Sector Alarm customers.

This library also supports multiple sites connected to the same customer account

You can visit the Sector Alarm at http://www.sectoralarm.se

## Installation
```bash
npm install sectoralarm
```

## Usage example

```js
const sectoralarm = require('sectoralarm');

const email = '<Your account email>',
      password = '<Your account password>',
      siteId = '<Your Panel/Site ID>';

sectoralarm.connect(email,password,siteId)
    .then(async (site) => {
        
        await site.status()
            .then((status) => {
                console.log(status);
            });

        await site.history()
            .then((history) => {
                console.log(history);
            });
    });
```
## Output

**Example output from calling status**

```js
{ siteId: '38728342',
  name: 'Home',
  armedStatus: 'armed',
  partialArmingAvailabile: true,
  user: 'Code' }
```

**NOTE:** armedStatus can either be armed, partialarmed or disarmed. user can be either state the user, be empty or state Code (Kod) if a code was used to arm/disarm.

**Example output from calling history**

```js
[ { time: '2018-01-23 07:48:19', action: 'armed', user: 'Code' },
  { time: '2018-01-22 16:45:52', action: 'disarmed', user: 'Code' },
  { time: '2018-01-22 07:46:23', action: 'armed', user: 'Code' },
  { time: '2018-01-20 15:14:18', action: 'disarmed', user: 'Code' },
  { time: '2018-01-19 15:51:05', action: 'armed', user: '' },
  { time: '2018-01-19 15:50:46', action: 'disarmed', user: 'Code' },
  { time: '2018-01-19 15:50:11', action: 'partialarmed', user: '' },
  { time: '2018-01-19 15:49:30', action: 'disarmed', user: 'Code' },
  { time: '2018-01-13 11:45:57', action: 'armed', user: 'Code' },
  { time: '2018-01-13 11:44:53', action: 'disarmed', user: 'Code' } ]
```