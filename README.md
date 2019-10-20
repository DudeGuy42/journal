# JOURNAL

## 10-19-2019
This is my first entry. I am currently designing a project. I am experimenting with a lot of different technologies and a consequence of this is that I am constantly spinning up different README.md files, and literring hard-drives and repositories with my thoughts. This acts to union those disparate pieces in to a consistent thread. Hopefully this will make me a bit more coherent as well. 

I am generally lead towards different technologies by necessity, suitability, ease-of-use, and interest (I'd like to think in that order, however sometimes I may become interested in a thing and throw everything else away and find an excuse to use that interesting thing; i.e. shiny objects are pretty). I want to move in to the VR world. I suspect that while it is great to do a lot of things on the client device locally, I am a Carmack at heart, and I am curious about the benefits allotted by doing work in remote locations and having it streamed to the device. This is the source of my current inspiration. Building massive, scalable services to host systems for VR applications. I am most interested in the Actor Model of programming for this reason, though after researching and experimenting with it a bit, I am curious to see what the throughput of it is like. A lot of different and even some of the more interesting usecases require a high throughput. That is my current mission: Build a distributed, actor-based system, and test its throughput.

I have experimented with Microsoft's Service Fabric only so far, but have looked at other producers like Akka.net, and I am now looking at Thespian (a python implementation) as well as CAF (a C++ implementation in its early days). 

Service Fabric is a great idea, and I suspect I will keep migrating back to that framework, but in the meantime it is a headache to work with while C# 8, and .Net Core 3 are coming up (or rather, now that they appear to be out, waiting for the Fabric team to catch up to the current state). 

Since these technologies are relatively new, and my exposure to them is definitely new a lot of my writing is probably going to be exploratory and rife with errors. I do not mind, and if a reader happens upon these words: I hope they will be forgiving.

### Experiments with Thespian
Today I spent several hours ramping up and studying Thespian, an actor based implementation for Python. I like it a lot. My first implementation consisted of 
two actors. One is the "parent" and the other are "children." The Server creates a RegionActor and then subsequently tells it to spawn three GuyActors. Then the server begins pumping "tick" messages in to the RegionActor, which upon receipt, inform the RegionActor to produce Tick messages to each Guy. Each actor is also equipped with the ability to log content. Because I created a UDP-based ActorSystem, each Actor type is launched as its own process. Because Python is single-threaded at process level, I found this abstraction to be pleasant to think about. 

The server kicked on and everything (eventually) started filling the logs. I used `procexplorer` to confirm that traffic was occurring in sync with the tick messages the server output. It's a very nifty abstraction. I am going to spend one more day learning how multiple actor systems can be spun up (i.e. on different machines entirely) and then I think I will resume laying the ground work for an architecture for a service that aims to be massively scalable.

My lab work is here: https://github.com/DudeGuy42/python-lab
Thespian is located here: https://thespianpy.com/