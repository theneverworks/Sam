Based on the [mattmakai](https://github.com/mattmakai "mattmakai")/[slack-starterbot](https://github.com/mattmakai/slack-starterbot "slack-starterbot")
author: Matt Makai (matthew.makai@gmail.com) web: http://www.mattmakai.com/
https://www.fullstackpython.com/blog/build-first-slack-bot-python.html

Based on the Py-AIML or PyAIML or pyAIML or Program-Y interpreter currently cloned by [creatorrr](https://github.com/creatorrr "creatorrr")/[pyAIML](https://github.com/creatorrr/pyAIML "pyAIML")
author: Cort Stratton (cort@users.sourceforge.net) web: http://pyaiml.sourceforge.net/

# What is Slack?

[Slack.com](https://slack.com/ "Slack.com") has a video explaining all you need to know on YouTube [What is Slack?](https://youtu.be/9RJZMSsH7-g "What is Slack?")

# What or who, is Sam?

Sam is a new twist on an old favorite. The use of the [creatorrr](https://github.com/creatorrr "creatorrr")/[pyAIML](https://github.com/creatorrr/pyAIML "pyAIML") interpreter to add personality to a command capable Slackbot using Matt Makai’s [mattmakai](https://github.com/mattmakai "mattmakai")/[slack-starterbot](https://github.com/mattmakai/slack-starterbot "slack-starterbot"). Sounds simple, but the extendibility of Python and the availability of Slack means from you browser, phone, or desktop app, you can control, check and execute anything. Share the output of commands, directly with your team or family. The AIML-Slackbot is intended to leverage the power of Slack as a delivery medium for teams, personal and professional.

Sam also utilizes Twilio to add text capability to your home or office AI. I'm currently working on his Outlook client to add direct email capability will relying on Outlook to manage security and interfacing with Exchange.

He or she has the ability to;

  * Execute builds from Microsoft Team Foundation Server utilizing the [Microsoft](https://github.com/Microsoft "Microsoft")/[tfs-cli](https://github.com/Microsoft/tfs-cli "tfs-cli") tool
  * Locate my bus is utilizing the GTFS feed from my local city
  * Perform health checks on ArcGIS Server
  * Call a web service or URL to GET or POST data
  * Look up a song
  * Find a movie playing nearby
  * Ask the Wolfram|Alpha Super Computer Cluster a question
  * Pull a random gif from GIPHY using [shaunduncan](https://github.com/shaunduncan "shaunduncan")/[giphypop](https://github.com/shaunduncan/giphypop "giphypop")
  * Start/Stop/Restart services on another machine
  * Check the status of a service on another machine
  * List open files on your web server
  * List logins on your servers
  * Query your help desk(s)
  * Query your monitoring solution(s)
  * Query data from a database
  * Query data from Elasticsearch
  * Control or query your IoT devices
  * Interface with an alarm system

Anything you can script, you can enable for yourself, your team or your family and friends.

# Screenshots

![Alarm interface](http://theneverworks.com/images/github/alarm.jpg "Alarm interface")

![Temperature](http://theneverworks.com/images/github/temp.jpg "Temperature")

![Temperature in time](http://theneverworks.com/images/github/tempintime.jpg "Temperature in time")

![Bus locator](http://theneverworks.com/images/github/locatebus.jpg "Bus locator")

![Find movies](http://theneverworks.com/images/github/findmovies.jpg "Find movies")

![Who sings](http://theneverworks.com/images/github/whosings.jpg "Who sings")

![Pick a movie](http://theneverworks.com/images/github/pickamovie.jpg "Pick a movie")

![Look up bacon](http://theneverworks.com/images/github/lookupbacon.jpg "Look up bacon")

# History

The definition of artificial intelligence (AI) currently refers to intelligent agents that perceive their environment and act upon that to achieve some task. What we call chat-bots, once were called stimulated response artificial intelligence. They are either weak forms of AI with some randomness overlaid a on rule based set of actions or they employ machine learning to analyze a body of conversation to attempt to learn the appropriate conversational response to a given input. As I want Sam to perform as I expect, every time, I have over fit his actionable commands. Over fitting makes the commands less adapted in dynamic situations but ensures reliability of actions taken.

I have been a fan of the simplicity of AIML for many years. No web services to call or rely on, small, light, portable, predictable, personality! Where you want it. Sam is based on the ALICE bot of old. Here is some info on the ALICE bot (AIML) http://www.alicebot.org/about.html. It’s what the PyAIML interpreter is for. The full sets of AIML can be found here, http://www.alicebot.org/downloads/sets.html. You can always create your own custom sets or there are a few floating around the web. Some with encyclopedia like pools of facts and such.

I had the idea of wiring the two together after reading a great article on Full Stack Python by Mr. Matt Makai https://www.fullstackpython.com/blog/build-first-slack-bot-python.html.  He has provided an excellent write up of how to add your bot account to Slack and how to retrieve your token and bot ID.  The framework code is entirely from mattmakai/slack-starterbot.  

# Installation and Dependencies

Before you begin, you’ll need to install some required modules. I recommend utilizing PIP especially if you have Python 2.7.9 or greater. At that release, PIP is installed by default. You can find it separately here, https://pip.pypa.io/en/stable/. Depending on what you intend to use Sam for and how you deploy him, will affect the dependencies naturally.

I am or have successfully deployed Sam on Windows Server 2012, Windows 10, Windows 8.1, Windows 7, Raspbian Jessie, Raspbian Wheezy, Ubuntu 14.04 LTS, and Ubuntu 16.04 LTS. Using Python 2.7.8 through 2.7.13.

I have not tested on Python 3.x.

I am utilizing Advanced Message Queuing Protocol (AMQP) https://www.amqp.org/ exchanges to route messages from various sources. Utilizing them for asynchronous messages “FROM” the bot give you a means to thread heavy processes and return results later and gives the illusion that the bot is actively performing human work. In reality, the threaded process is doing what it needs and returns the response later. We are able to feed alerts to or through the bot. Alerts can be reported to the team as though they came directly from the bot.

I prefer RabbitMQ, the open source messaging queue https://www.rabbitmq.com/. The deployment, configuration, and administration of Rabbit are not part of this documentation but their website has excellent step by step examples in Python. RabbitMQ runs great on a RaspberryPi too.

I also purchased an awesome and affordable voice model with its own engine from a company called Cepstral, http://www.cepstral.com/. With their speech engine, you can have the same voice on Windows and Linux (even the Pi). This is the engine I use in the announcement service and in any other speech synthesis components.

NOTE: Installations should be performed "as administrator" in Windows or using "sudo" in Linux.

NOTE: You may have to include the full path to python if you didn't include Python in your PATH environment variables.

## Windows Only Items and IronPython

The intended design is to make a cross platform solution. That being said, each operating system offers different capabilities that we wish to capitalize on. Some components, such as SamSpeak.py, only run on Windows as they utilize the Windows speech recognition engine. Further, SamSpeak.py requires IronPython 2.7.x http://ironpython.net/.

## Installing the required Py-AIML

Linux:
```
sudo python /PATH/setup.py install
```

Windows:
```
python /PATH/setup.py install
```

## Installing the Required Slack Client

Linux:
```
sudo pip install SlackClient
```

Windows:
```
python -m pip install SlackClient
```

## Installing the Optional Pika Client (to use AMPQ messaging queues)

Linux:
```
sudo pip install pika
```

Windows:
```
python -m pip install pika
```

# Running Sam

Before Sam will run, it will need to have a few edits made.

## Required edits

Edit slacksam.py and update the Slack bot ID to your Slackbot's name

```python
AT_BOT = "<@BOT_ID>"
```

Edit slacksam.py and update the Slack token to your Slack team's token

```python
slack_client = SlackClient("SLACK_TOKEN")
```

Edit slacksam.py and update the path to your AIML files and or compiled brain

Linux:
```python
saiml = "/PATH/sam/aiml/"
```

Windows:
```python
saiml = "C:\\PATH\\sam\\aiml\\"
```

## Starting Sam up

Running only the Slackbot fairly straightforward. You execute python and pass slacksam.py as an argument.

```cmd
python slacksam.py
```

You may have to include the full path to python if you didn't include Python in your PATH environment variables.

Linux:
```sh
sudo /usr/bin/python slacksam.py
```

Windows:
```cmd
C:\PATH\python slacksam.py
```

## Adding new commands

Edit slacksam.py;

Using the starterbot framework we first add a command phrase constant

```python
YOUR_COMMAND = "make me a sandwich"
```

Locate the handle_command function definition. Add your command handler by appending to the handle_command.

```python
elif command.startswith(YOUR_COMMAND):
```

Locate the Help handler "elif command.startswith(HELP_COMMAND):" and add a line to explain how to use your new command.

```python
response += "*look up* <KEYWORDS> - _Experimental_ _command_ to look up a topic. \n" 
```

## Conversation bot

Any text sent to the bot requires "@" in Slack. You could also add support for direct messenging if you wished. Any text that is not determined to be a command is sent on to the AIML interpreter. This is the blending of both works.

```python
else:
        response = k.respond(command, "sam")
```

# Editing AIML

You can edit the AIML files or predicate file to suite your bot requirements. The bot start up is designed to detect when Sam's files have been edited or added to and recompile the brain automatically. Note, this will impact the next start up as the bot must relearn its personality.

# Brain file

The brain file sam.brn is a compiled and optimized binary version of the AIML files themselves. It is compiled at start up and requires shutting down Sam to update it with changes.

# What is the Message Handler?

The Message Handler is ran as a service in Linux or Windows and feeds AMPQ messages from one or many exchanges into Slack as the bot. Useful for adding intelligence to other processes. There is also a Web Message Handler where we wrap the same idea in a Flask web wrapper and connect to it via GET/POST. This expands your integration capabilities to anything that can call cURL. 

Imagine a scheduled task that you have running on a machine somewhere, either as a batch, CMD, or bash script. Adding a single line to your script to pass a URL to cURL sends a message to the Message Handler and is sent as a message in Slack or spoken out loud via the Announcement Service.

# What is the Announcement Service?

The Announcement Service watches for messages sent to a single or multiple AMPQ message queues and passes them to the Cepstral Swift speech engine to be spoken out loud in Linux or Windows, and even the Raspberry Pi.

# How are you making services out of Python files?

## Linux Service

Linux is largely a matter of determining the init system used by the flavor of Linux you're using. I've had the most success with systemd services and will elaborate on those up. I have had success with Upstart as well, but will not explain those steps. Likewise, cron jobs work though not quite as reliably as I'd like.

Note:  I prefer nano as my Linux terminal text file editor. There are many others and you may use the one that you love. Just replace `nano` with the editor of your choice.

To create a systemd service, create a file (or copy one from the source code and edit it) in the systemd directory.  Replace `NAME` with the service name you'd like to use. In this example below, calling the editor with the filename of a file that does not exist, creates a new unsaved file with that name.

```bash
sudo nano NAME.service
```

Example: `sudo nano sam.service`

Add a unit description, that's our service name.  Set the working directory to the path of your Python file.  Set the path of the Python file that is to run as your service.  Setting `Restart=always` assures that the service will auto start and auto restart after failure.  Set the system log identifier to a name that is unique.  Take the other values as provided. Without going into great detail, they establish permissions, logging, and our installation.

```bash
[Unit]
Description=Slack Client
[Service]
WorkingDirectory=/path
ExecStart=/usr/bin/python /path/slacksam.py
Restart=always
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=slackclient
User=root
Group=root
[Install]
WantedBy=multi-user.target
```

It may be necessary to set or update permissions on your new service file. I have read where some flavors of Linux require it. With Raspbian I did not have to. 

Example: `sudo chmod u+rwx /etc/systemd/system/NAME.service`

Next you'll need to enable the service, which is where the `WantedBy=` line came in earlier. To enable the newly defined service use  system control enable.

```bash
sudo systemctl enable NAME.service
```

Once your service has been enabled, it's ready to be started.

```bash
sudo systemctl start NAME.service
```

Use the stop parameter to stop the service.

```bash
sudo systemctl stop NAME.service
```

## Windows Service

Windows services can be wired a few different ways. You can create a simple scheduled task but I have found a service wrapper that does everything you could want already. It's called [kohsuke](https://github.com/kohsuke "kohsuke")/[winsw](https://github.com/kohsuke/winsw "winsw") and it handles installation of the service, logging, both error and output, and gives you the ability to set recovery options. Even Slack loses connection sometimes.

To be continued... steps to follow.

# Design changes planned

I'd like to connect the Slack Sam client to the separate socketed Sam Brain making them independent. Then the other clients, SMS, email, etc. can reuse the Brain process.
