# Programming Languages and Techniques-CIS120 #
Repository for Programming Languages and Techniques (CIS 120, Fall 2018 Upenn)  

As a part of the CIS 120 Programming Languages Course, Java code for the following projects was written:
- Server Model
- Spelllchecker
- Game

## Server Model ##
A internet chat server was designed using Java. A modele of the internal state of the server was developed to handler communicaiton with users of the chat system.

For the Server Model, a `User()` class to store the `nickname` and `userID` of each user; and a `Channel()` class to store the nickname of the owner of each channel, the channel name, and a group of users, which is a map data structure with the key being the nickname of the user (type string) and each user profile (type user). The User class has a constructor that sets the userID and nickname via setter methods, along with getter methods for the nickname and userID. Each class implements the `Comparable <T>` interface and I have overridden both the `compareTo` and `equals` methods with my own implementations. Also, in Channel, I have methods that return collection views of all users in a channel and just return the nickname of all users in a channel.

In `ServerModel`, I am instantiating private two maps, one to hold a map of registered users with the key being the user nickname, and the value the actual user of type `User` of which each is a User object created earlier. The other map is a map of registered channels with the key being the name of the channel, and value being the Channel object created earlier.

I keep track of whih user has which user ID by instantiating another map in server model that will associate each user nickname to an ID. To store which users are in the channel, there are getter methods that I have implemented that when called, retrieve the list of users in a channel. This is done by calling my instantiated map of registered users, using `.contains` method of TreeMap. The input variable is the channel name which checks first that the channel exists. If it does I then call my `getUserGroup` method in channel that returns a list of user nicknames in a channel. I do this with the `.get` method of TreeMap of which the input variable is the channel of interest.

To track which user is the owner of each channel, I instantiate private fields in my Channel class that stores the owner, which is passed in as an argument each time a new Channel class is instantiated. There are also getter methods that retrieve the current owner nickname and setter methods that enable one to change the current owner.

The most practical collection for this project is `TreeMap<>` in that it enables me to store the required associations that this project requires, e.g. nickname to ID, nickname to user, channel to user-group, and channel name to channel.

In the proces of developing this project, I removed the nickname to id my in servermodel to streamline my code. The associations between nickname and userId are already store in my User Class. There is no need for an additional map to store that information. I also updated methods in channel class that return collection views of the current group of users in a channel and the user nicknames in a channel to return copies instead of the collections themselves to preserve encapsulation. I did this my instantiating new maps in these methods to copy over the relevant data and then returned those new maps. I also modified other methods in my code e.g. getUsersInChannel() in the same way to further preserve encapsulation. I had to add more methods that would enable me to update the usergroup in a specific channel and use map .remove methods inside my Channel class , again to help preserve encapsulation.

To keep track of which channels are invite-only, I added a private Boolean field in my Channel class that holds the invite-only state of a specific Channel.

Throughout my design itereation, I made quite a few changes. I went through code in servermodel and removed for each loops where a TreeMap method would save, which removed quite a bit of code from methods like createChannel() and addUserToChannel(). I also removed redundant state variables in my Channel class, one being a variable that held the current owner, of type User. This was not needed and I instead directly placed that owner in the userGroup upon instantiating the Channel class. This corrected errors where I was comparing a given nickname to an owner name that was not of type string, but was of type User. I utilized my getOwnerNickname() method that returned the String version of the owner nickname. I noticed this as a warning but caused me to fail certain test cases where an owner that was kicked out of channel did not result in deleting that channel.  I also went through and corrected ConcurrentModificatonExceptions which arose from deleting channels that I was currently iterating through. I first became aware of this problem after my first submission attempt and wrote comprehensive test cases to isolate the issue. I addressed this issue by saving the specific channel to delete to a set of channels deleting only after exiting the loop. I also fixed a case where I was inviting a user to a non-existent channel. A second submission attempt revealed this error so I created a test to test what happens when I invite a user to a non-existent. It resulted in a null-pointer exception. I realized that I was checking if a channel existed after checking if the channel was public, which would result in a null pointer exception if the channel did not exist. So I moved the error checking case for channel existence to be above the case for checking if the channel was public and that solved the issue.

## Spelllchecker ##
```
// TODO Code
```

## Game ##

```
// TODO Code
```
