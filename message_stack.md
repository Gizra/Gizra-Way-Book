# Message stack

The message stack contains three modules: [Message](https://www.drupal.org/project/message), [Message Notify](https://www.drupal.org/project/message_notify) and [Message Subscribe](https://www.drupal.org/project/message_subscribe).

Message represents a record of event that occurred in the system. Message is an entity - `message` to `message type` is like `node` to `content type`. We can define different message types for different events, for example, one message type for message created every time node created, and another message type for message created when new user registered to the site.


The combination of these modules allow users to subscribe to content and be notified when events occur involving that content.


References:  
[Webinar with Amitai](https://vimeo.com/63919900)  
[Module documentation](https://www.drupal.org/node/2180145)  
[Gizra blog](http://www.gizra.com/tags.html#Message-ref)
