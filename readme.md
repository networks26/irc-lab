# Lab: Talking to an IRC Server Using Only netcat

Welcome to the quiet underlayer of IRC — the part usually hidden behind shiny clients.
In this lab you will connect to a real IRC network using raw TCP and speak the protocol manually, keystroke by keystroke.

Your job is to demonstrate that you understand the structure of IRC messages, can keep a connection alive, and can perform basic channel/user operations without any client help.

Everything must be done using netcat.

However, so that you will see how it looks, the Vachagan will open an IRC client on the Screen so that you all can see yourself in the room on the big screen.

# Big screen time!

If you want, you also can connect both via IRC client and netcat.
For the lab machine you can try to download portable versions of [pidgin](https://portableapps.com/apps/internet/pidgin_portable) or [mirc](https://portapps.io/app/mirc-portable/) or [kvirc](https://portableapps.com/apps/internet/kvirc_portable).

But the purpose of the lab is to talk to IRC via netcat to learn the protocol.



---

## 1. Preparation

You will connect to:
```
the.hell.am
```
and from there to an IRC server.

Use your system’s netcat (either BSD nc or GNU netcat).
The command looks like:
```
nc the.hell.am 6667
```
If your operating system requires a different syntax, adjust accordingly.

You may want to connect by using:
```
nc the.hell.am 6667 | tee irc-session.txt
```

in order to save the output also to that file, so in the end it'll be easier to submit that file.

Before beginning, study this reference carefully — you will need it to craft your own IRC messages:

Manual IRC protocol introduction:
[https://github.com/networks26/BBS/blob/main/irc/irc.md](https://github.com/networks26/BBS/blob/main/irc/irc.md)

(You may want to keep it open while you work.)

---

## 2. Connect & Identify Yourself

Once you’re connected with nc, the server will greet you with numerics and sometimes a PING.
You must speak the minimal mandatory lines:
```
NICK your_nick
USER your_nick 0 * :Your Real Name
```
After this, PING/PONG will begin.
When you receive something like:
```
PING :some_token
```
you must answer immediately:
```
PONG :some_token
```
Failing to do so disconnects you.

---

## 3. Your Tasks

Perform all operations manually, by typing IRC commands directly into netcat.

Work inside the channel:
```
#auanet26
```
### Required actions

1. Join the room:
```
JOIN #auanet26
```
2. Say hello & identify yourself.
   Send a message that includes your GitHub username:
```
PRIVMSG #auanet26 :hello there, I am <your github username>
```
3. Respond to PING messages from the server with PONG.

4. Kick someone from the room (requires operator privileges or coordination with classmates):
```
KICK #auanet26 <nick> :optional reason
```
5. Send someone a private message:
```
PRIVMSG <nick> :hello from netcat
```
6. Change the channel topic (if you have permission):
```
TOPIC #auanet26 :New topic text
```
7. Perform WHOIS on any user:
```
WHOIS <nick>
```
Read and understand the returned numerics such as 311, 312, 318.

---

## 4. Save Everything You Receive

You must log every line you and the server exchange.

The easiest way is to redirect netcat’s output:
```
nc irc.libera.chat 6667 | tee irc-session.txt
```
Or run netcat normally and later copy/paste the full transcript into a file named:

irc-session.txt

---

## 5. Submission

Place your transcript file into your repository:

git add irc-session.txt
git commit -m "IRC lab session"
git push

Your submission must include all raw communication:
• your commands
• server numerics
• channel messages
• PING/PONG
• WHOIS output
• topic changes
• private messages
• the KICK command you issued

Do not clean or edit anything.
We want to see the full wire conversation exactly as it happened.

---

## 6. Goal of the Lab

By the end of this exercise, you will have:

• spoken IRC manually
• understood numerics and prefixes
• survived server heartbeats
• manipulated a channel
• used WHOIS and private messages

How cool is that?

You will also have a complete transcript — a small fossil of your raw IRC session.

