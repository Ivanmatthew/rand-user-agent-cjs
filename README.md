# rand-user-agent package

rand-user-agent is a nodejs package that provides random generation of a real user-agent string, based on the frequency the user-agents occur.

## Installation

Run the following command in the main folder of your project:

```
npm i rand-user-agent
```

## Usage Example 

```
const randUserAgent = require('rand-user-agent');
const agent = randUserAgent("desktop");

console.log(agent);

```

## How does it work

Using our own database with data about guests and their user-agent, we update a file called "user-agents.json" on a weekly basis with new information. 

This data is saved in a json under the following format:

```
{
    deviceType1: {
        userAgent1: frequencyUserAgent1,
        userAgent2: frequencyUserAgent2,
        ...
    }
    ...
}
```

Because sometimes one user-agent might occur so many times that it will end up being returned most of the times in the result, we need to normalize the frequency values to prevent that. To do so, we sort an array with all the unique values of the frequency, and replace the frequency for each user-agent with the position where the frequency is in the sorted array. We are doing this using the JSONfrequencyNormalize function from helpers.js

To make things easier for us, when somebody uses the package we are first transforming the processed json into a indexes json, such as the one below:

```
{
    deviceType1: {
        userAgent1: {
            minIndex: 0,
            maxIndex: frequencyUserAgent1 - 1,
        },
        userAgent2: {
            minIndex: frequencyUserAgent1,
            maxIndex: frequencyUserAgent2 - lastMaxIndex - 1,
        },
        ...
    }
    ...
}
```

Using the data in this format allows us to easily retrieve a random user-agent, while also taking into account how often it occured in our data.