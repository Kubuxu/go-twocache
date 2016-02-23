# go-twocache

Two stage caching for Golang.

#### What is two stage caching?

It is cache which doesn't suffer from flaw of normal caches. When entry in cache expires user is left out waiting for new entry to be found.
Two stage caching solves that problem by using two expiration times, first defines after what time entry should be deemed _dirty_, second time works like in normal cache, when
exceeded it renders entry unusable.

Dirty entries will still be returned on cache get request but will cause a background resolution to run. When this resolution finished entry is updated and its timers reset.

#### What is the benefit?
Imagine that we want cache to expire quickly, let's say 1 minute. If user uses the cache every 15 seconds, one in four requests he will have to wait for the cache to be refilled.
This can be solved with two stage cache having first time equal to 30 seconds and second to one minute.

This way when user uses cache every 15 seconds, after second use the background resolution will run. If it takes less than 30 seconds there won't be any cache miss.

### License
The MIT License 
Copyright (c) 2016 Jakub Sztandera
Full text in LICENSE file.





