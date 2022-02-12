### Array Update Pending

#### Problem
- create a collection of posts
- it should have title, comments, author details, tags
- comments should be an array of objects with, body, author of the comment etc., comment id
- tags should be array of strings
1. push a new tag into a post
2. push multiple tags into a post
3. pull and remove a particular tag
4. pull and remove an array of values use $in
5. use $pop to remove first and last tag
6. use addToSet to add.5 tags
#### Part II
7. create a collection of users with high scores
8. each user can have 3 high scores
9. it should be always in descending order
10. add 5 new high scores, and maintain the order, and keep the limit of 3 scores
11. remove multiple scores which are greater than x value

1. 
```js
    db.posts.update({id:1},{$push:{tags:"nature2"}})
```

2. 
```js
    db.posts.updateOne({id : 1},{$push : {tags : {$each : ["comedy","drama"]}}})
```

3. 
```js
db.posts.updateOne({id : 1},{$pull : {tags : "nature2"}})
```

4. 
```js
    db.posts.updateOne({id : 1},{$pull : {tags : {$in: ['nature','passion']}}})
```

5. 1. Last tag of the array pop
```js
     db.posts.updateOne({id : 1},{$pop : {tags : 1}})
```

5. 1. First tag of the array pop
```js
     db.posts.updateOne({id : 1},{$pop : {tags : -1}})
```

6. 
```js
     db.posts.updateOne({id : 1},{$addToSet : {tags :{$each:[ 'logical', 'money', 'physical', 'furious', 'nature2', 'comedy','comedy with drama' ]}}})
```

10. 
```js
     db.users.updateOne({ _id: ObjectId("6207aaafc8532bcd1eb953ff")},{$push :{scores :{$each : [100,99,96,93,91],$sort : {scores : -1},$slice : 3} }})
```

11. 
```js
    db.users.updateOne({id :1},{$pull : {scores : {$gt : 70}}})
```