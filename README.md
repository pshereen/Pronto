# Pronto

Programming Challenge: 'Loons Tower Defense
---
Expected time frame: 1 week

Server URL: `wss://pronto-challenge.ngrok.app/{YOUR_EMAIL_HERE}/ws`
Replace `{YOUR_EMAIL_HERE}` with your email address in the URL. The URL may change occasionally so reach out to kemal@pronto.ai if it's not working for you.

The programming challenge should take no more than 1 week. If selected to continue on the next stages, we will be discussing your solution and implementation at the end of the challenge; even if all the steps have not been completed. 

The submission should be in a github repo and a URL for your deployed app, with instructions on how to deploy your implementation locally.

Feel free to reach out to kemal@pronto.ai at any time if you'd like to discuss parts of the challenge or have any questions! Happy Hacking! 

### Problem statement
You've been assigned a project where you implement a single player tower defense game (**NOT** similar to [Bloons Tower Defense](https://en.wikipedia.org/wiki/Bloons_Tower_Defense). The player can place turrets on the map/canvas to pop 'Loons (**NOT** Bloons), which are gas-filled sacs that seem to move of their own accord. The problem is split up into 4 stages:

 1. Implement a user interface for the game. It doesn't have to be feature-complete or pretty. A websockets server running a basic reference implementation of the backend engine & RPC has been provided.
    - The initial frontend should interface with the provided server
    - Players should be able to drag and drop turrets to a location on the canvas
    - Players should be able see the location and trajectory of the 'Loons
    - Turrets should be able to pop the nearest 'Loon at 1 Hz.
    - Loons will expire & disappear when they reach the end of the map.

 2. Implement the backend server for the game. Feel free to change the structure of the RPC if you don't like certain aspects of the reference implementation. Bonus points if you can improve the backend logic.

 3. Extend the RPC interface & frontend to introduce the following mechanics:
    - add a `Level` attribute to both loons & turrets. 
    - Turrets start at level 1. Players should be able to upgrade turrets
    - Level 2 'loons should spawn 10% of the time. 
    - Loon's that are level 2 can only be popped by turrets that have been upgraded to level 2

 4. Discuss potential bugs or exploits with either the game mechanics or the RPC interface. How can we make it more robust? How would you improve the overall architecture?


Basic RPC spec
---
Very basic pub-sub mechanism.

### Subscribing

Client Request:
```
    {'subscribe': 'topicA'}
    {'subscribe': 'topicB'}
```

Server Response: 
```
    {'topicA': <payload>} 
    {'topicB': <payload>} 
    {'topicA': <payload>} 
```

### Subscription topics
 - `msg`: event messages displaying the state of the game
 - `loonState`: the state of all loons in the current wave.

### Publishing

Client Request: 

```
{'publish': {'topicA': <payload>}}
```

### Popping Loons
Client Request:
```
{
  "publish": {
    "popLoon": {
      "loonId": <loonId>
    }
  }
}
```

