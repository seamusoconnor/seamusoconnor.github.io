---
title: Building my first IOS app with Swift and Xcode
date: 2020-06-27 08:00:00 +0100
categories: [IOS]
tags: [swift, coding, app, development]
---



![hello](/assets/images/2020-06-27-IOS-Swift_app/card1.png)

## Why ?

I’ve started using the <a href="https://francescocirillo.com/products/the-pomodoro-technique#" target="_blank">Pomodoro technique</a>  to keep track of projects that I’m working on. It’s early days with it but I’ve found it helps me keep track of the various professional and non-professional tasks I have ongoing. I took a look on the Apple Store for apps and although there are some, I have a few ideas that would be really useful in a cross-platform app. Initially I wanted the app built on macos but most of the tutorials with Swift i found are focused on IOS. I thought it would be a good idea to learn a bit of Swift, build an IOS App, and then port it to macos. Therefore the first thing I need to do is to learn to develop a generic IOS app to understand what’s involved, kind of like “Hello World”.


I used this excellent <a href="https://www.youtube.com/playlist?list=PLMRqhzcHGw1ZkH8RuznGMS0NZs0jWQQ5a" target="_blank">youtube</a> tutorial from <a href="https://www.youtube.com/channel/UC2D6eRvCeMtcF5OGHf1-trw" target="_blank">CodeWithChris</a>. It focuses on building a card game, where you deal the cards and either the player or the dealer wins. used xcode 11.2 as the IDE and tested the app on an iPhone 7, running IOS13. The finished product looks like this:

## Swift

Swift is a programming language developed by Apple and is the “offical” language for development of IOS, iPadOs and macos apps. It appears to be a replacement for Objective C. My only experience with coding (outside of College) has been python so it as nice to delve into something different and approach similar ideas from a different perspective.

Here’s a small example of Swift code:

```swift
// Declare a variable
var str = "Hello, playground"

// Declare a constant - variable that doesn't change
let number = 33

if number == 33 {
    print("This number is as expected: \(number)")
}
```

The first portions of the tutorial are based around building the GUI elements that are used to interact with the apps. Xcode allows this to be built through code or by manipulating the elements in a GUI like environment called a storyboard. Each of the elements has properties that can be modified, like creating a text label and modifying the colour/font/size etc.. I found the experience to be ok, although it gives Xcode a kind-of photoshop-like behaviour that I’m not familiar with. I’d imagine that doing this through code would be pretty painful, so in time clicking through all the non-obvious icons would make a bit more sense. XCode itself probably has some in depth tutorials to understand what’s going on (again like photoshop) and warrants further study.

Once the GUI elements are built, it’s time to write the code. The entirety of the code is as below
<br><br><br>
![hello2](/assets/images/2020-06-27-IOS-Swift_app/code1.png)
<br><br><br>
@IBOutlet lines 5-11 are used to link elements in the GUI to code labels – For instance, the left card UIImageView shown is assigned the name LeftImageView

The bottom-left element to track the player score is assigned the name LeftScoreLabel.

Lines 13-14 are used to initialise the scores at the start of the game to Zero.

The @IBAction function DealTapped links back to the “Deal” button. Once tapped by the user, it runs the code below.

The LeftNumber and RightNumber generate a random integer between 2 and 14 (the card numbers, which correspond to different picture assets in the Assets.xassets folder

Lines 25-26 assign the image (card) displayed for each left and right card to one of the asset, eg. if 9 is the random integer then “card\(LeftNumber)” becomes “card9” which corresponds to an image file stored.

lines 28-37 are used to deal with the logic of updating the score displayed, depending on if the Left (player) or right (CPU) gets a higher random integer drawn.


## Testing

One thing that’s really nice about XCode is that it allows you to simulate your app across multiple virtual devices or to push the app to your physical device. You can do this as you’re developing so it gives some nice feedback and allows you to see if some of your elements look cramped or unwieldy in different IOS devices – I tested from iphone 7 to iPad Pro 12.9.

## Conclusion

For me this seems a world away from when writing python scripts to interact with networking devices as this allows a more pleasing feedback, dare I say child-like way of developing applications. Pushing the app to my iPhone lets me “amaze” my friends with something I spent a few hours on, as opposed to writing a script to pull some configuration from a device and them being non-plussed while I run some bash command to execute the script. I found another course to develop a note-taking app so I’ll complete that and I believe both of these should give me some of the elements I need to develop my own Pomodoro app.
