# Collaborative filtering for Node.js

> This API is a lightweight implementation of collaborative filtering for Node.js. The only dependency is Math.js. Currently it supports generating recommendations with Jaccard similarity.

## Features

- Generate recommendations for a user based on users with a similar taste.
- No popularity bias (normalization based on popularity).
- Currently only supports likes (no dislikes).
- Database agnostic. As long as you are running Node.js, you can use this API.

## Requirements

- Node.js

## Install

```
npm install collaborative-filter
```

## Usage

In your project, simply include the module.

```javascript
const rec = require('collaborative-filter')
```


## Example
To run the provided example.

```bash
node examples/demo.js
```

### How-to
The input for the engine is an array matrix which defines the ratings of the users in the database. It should be a matrix containing of 0:s (not rated) and 1:s (liked the item) and follow this format.

```
     I0 I1 I2 . . .
    [
U0  [1  1  1  .  .  .],
U1  [1  0  1  .  .  .],
U2  [1  0  0  .  .  .],
.   [.  .  .  .  .  .],
.   [.  .  .  .  .  .],
.   [.  .  .  .  .  .],
    ]
 ```
 In javascript, this could look something like this
 ```javascript
 const ratings = [
  [1, 1, 1],
  [1, 0, 1],
  [1, 0, 0],
];
 ```
 If you want to run the whole collaborative filter, you would do this:
 ```javascript
 const recommendations = require('../lib/cf_api.js');

 const result = recommendations.filter(ratings, 2);
 ```
where 2 is the user index. The output of this with ratings matrix as above, would be an array `[2, 1]`. This tells us that item 2 is the most appropriate recommendation followed by item 2.

You could also run the filtering process by calling the global API functions individually.

```javascript
const recommendations = require('../lib/cf_api.js');

const coMatrix = createCoMatrix(ratings, numUsers, numItems);
const result = getRecommendations(ratings, coMatrix, userIndex);
```
which results in the same array as before. This could be useful when you do not need to generate the co-occurrence matrix multiple times. For instance, if you want recommendations for multiple users, you do not need to generate the co-occurrence matrix multiple times, saving you processing time.


## Contributing

This API is far from done. It currently lacks support for dislikes and other rating scales. The plan is to improve it in the future. You can also submit a pull request if you want to contribute! We follow the Airbnb JavaScript Style Guide.

## License

MIT