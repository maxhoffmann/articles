---
date: 2013-10-20
---
# Email clients are bad designed

I’ve never met someone who loved working with emails. If “Inbox Zero” is a term there certainly has to be a design problem. Recently I’ve realized why there is so much frustration when we have to deal with our inbox. The email protocol itself is not the problem. The way email clients are designed is why we are always unsatisfied with our inbox.

## Inbox (52843 messages)

I don’t care how much emails I have received during the last couple of years. Why should this number be important, when the number of all received iMessages, facebook messages or Whatsapp messages is not? The only number I care about is the number of messages I have not yet read. Displaying the total number of emails sends multiple negative messages: “You should delete those emails.”, “You have work to do.”, “You could be running out of space.” and “You work too much.”

## No conversations

Imagine facebook displaying your messages the way email clients do. You would only get to see the very last message by someone. If you want to see what the same sender has written before, you would have to scroll down in your entire inbox, which is sorted by time, until you find the next message from the same sender. Additionally you would only find the messages you have received. To see the messages you have sent you would have to switch to another view where all your sent messages are listed. If you like to have something near to conversations you’d have to prefix all your messages with a topic, e.g. `<topic>: <your message>` or you would have to use the search. This sounds crazy, doesn’t it? This is the way every email client works.

Imagine an email client that looks like this:

[![iMessages (copyright by apple)](http://maximilianhoffmann.com/images/iMessages.png)](http://maximilianhoffmann.com/images/iMessages.png)

All emails would be displayed by sender, no matter what the subject is. If you receive a new mail it just gets added to the conversation with the same email address and jumps to the top of the list. If you receive an email from a new address the program asks you if you like to assign a name and a photo to it. It could display public profile pictures from social networks and your address book while you are typing the name, so you would only have to choose the one that’s correct or simply choose one from your disk. If someone has multiple email addresses just add it to the same name. Of course it would also strip out the conversation history at the end of a mail which some email clients include automatically.

## Newsletters and notifications

If you receive an email from facebook or a newsletter from Amazon you could flag the sender as a company and the email address as a newsletter or notification address. Future emails from this address will then be added automatically to a newsletter/notifications view. You could now enable or disable push notifications for conversations, notifications and newsletters separately.

> You would never again pull out your phone just to look at a newsletter that tells you something about a new product you don’t care about.

One could also add an option to disable push notifications for certain contacts and unknown email addresses. Additionally you could display a "unsubscribe" button beside newsletter emails that opens your browser with the url hiding behind the tiny, shallow unsubscribe link at the end of most newsletters. The mail program would pull that link out for you, so you don’t have to do it.

## Goodbye Mailboxes

Mailboxes are an anti pattern. Users don’t care which one of their mail addresses received the message. More important is who has sent it. You could add your contacts to lists like _work_, _family_ and _friends_. Whenever you receive an email it automatically gets added to that list and you could filter your inbox. If you want to read an email later just click on a button and it gets added to a “read later” list or create your own one.

## Attachments

Of course this program also would have a place where you could see all attachments you have received sorted by contact or date or whatever you want, just like Van Schneider designed it in his [DotMail app](http://dotmailapp.com/).

## Summary

Generally my message for people designing email clients is: Put users first. Current solutions emphasize the technology behind emails instead of the way people communicate. Let my contacts play the center role and display my mails as conversations — always. Give me convenience features like unsubscribe buttons for newsletters and display notifications as notifications in my email client instead of text I should read. Hide Mailboxes and let me manage contacts in lists instead. Dotmail is the first step in the right direction, but has no focus on the sender like I described above. I hope that better email clients will be released.
