# Alexa Develop Skill Set Documentation  
This documentation defines how to create an Alexa Skill on Amazon's Developer site, and how to test/use your skill on a particular computer whether it is connected to an Amazon Echo or not.


## Starting Up

#### Setting Up a Development Account with Amazon  
If you want your own account with Amazon where you can link and test your skill, you can set up an Amazon Developer account [here](https://developer.amazon.com).  

This step is only necessary if you want to develop a skill linked to an account specific to you.

#### Installing Flask-Ask  
Assuming Python is installed, you can run the command:
	
	$pip install flask-ask

If you are using a Mac and Python isn't installed follow the instructions [here](https://docs.python.org/3/using/mac.html), if you are using Windows follow the instructions linked [here](http://docs.python-guide.org/en/latest/starting/install/win/).

In your Python file where you develop your skill you must import Flask-Ask like this:
```
from flask import Flask, render_template
from flask_ask import Ask, statement, question, session
```
For more detailed information on using Python's Flask-Ask library, a link to documentation can be found [here](https://developer.amazon.com/blogs/post/Tx14R0IYYGH3SKT/flask-ask-a-new-python-framework-for-rapid-alexa-skills-kit-development).

#### Installing Ngrok  
Instructions to download and use Ngrok can be found on their website linked [here](https://ngrok.com).

## Developing Your Skill  

### Defining a Skill on Amazon Developer  
Log into [Amazon Developer](https://developer.amazon.com), click on the "Alexa" tab, then under Alexa Skills Kit click "Get Started."

In the top right click the "Add a New Skill" button, from here you can start creating your skill.

#### Skill Information  
For "Skill Type" choose "Custom Interaction Model," from here put your skill's name under "Name" and "Invocation Name," these two fields can be the same.
You do not need to change anything in the section labeled "Global Fields," from here Save your skill and then hit the Next button.

#### Interaction Model  
The Intent Schema must be in JSON format.  Your skills intents--the things that your skill does--are defined under a header titled "intents," you should have a section for each intent you create.  Each intent should have a name, defined under "intent."  If your intent takes input, such as a location or a person's name, in a section titled "slots," located on the same level as the name of your intent in the JSON. 

If you're intent using a data type not already defined by Alexa (such as a patient's name), you can define that data type by clicking "Add Slot Type" under the Custom Slot Type section. 
From here you can define the name of your slot type, make sure it is the same name as what you said your slot's type was in your Intent Schema, from here you can define valid values for your slot type under "Enter Values."

Under Sample Utterances you can define the questions that you plan on asking Alexa in order to activate your skill.  Sample Utterances consist of the name of the intent you want to use followed by the question you would ask Alexa.  When you actually ask Alexa these Sample Utterances you will say her name in place of the name of your the intent, so do not write the Sample Utterances with the plan of speaking the intent's name in the question.  If the Sample Utterance you are writing requires slot input, you define this by putting the slot's name that you defined in the Intent Schema (different than the slot's type), in squiggly brackets ({}) for each required Sample Utterance.

Examples of intent schemas, custom data types, and sample utterances for the skills Caregiver and Memory Game can be found in their respective folders in the GitHub respository. 

After all of this, Save your skill and hit the Next button.

#### Configuration  
Under "Endpoint" choose HTTPS as your "Service Endpoint Type" and for your geographical location choose North America.

If you are on the Machine you are choosing to host your skill on, you can define where that skill is hosted using `ngrok`.  If you don't have `ngrok` you can get it [here](https://ngrok.com/download).

In the Terminal, navigate to the directory where you created the Python file that uses `Flask-Ask` to develop your skill.  In this directory, run `ngrok` in the Terminal with the command

Mac/Linux:
	
	./ngrok http 5000

Windows:
    
    ngrok.exe http 5000

Copy the URL corresponding to the second `Forwarding` field under `Session Status`.  From here return to Amazon's Developer into the field underneath "North America" on Amazon's Developer site.

Keep the "Account Linking" section as is, from here Save and hit "Next."

#### SSL Certificate  
Under "Certificate for NA Endpoint" click the bubble next to *"My development endpoint is a sub-domain of a domain that has a wildcard certificate from a certificate authority."*  After this, Save your progress and hit "Next."

#### Test  
If you defined a valid endpoint in the "Configuration" section, you are able to click the "Enable" button that allows you to enable the skill for testing on your account.

After this, save your progress.  Assuming your skill was developed with Flask-Ask, your work on Amazon's Developer site is complete.  From here you can move forward and try out your new skill.

## **Testing & Running The Alexa Skill**  

To try out your skill, first make sure Ngrok is running from the skill's directory in the Terminal. 
Next create a new tab in the Terminal, here you can start your Flask-Ask Python program that defines the skill. 
You can test out your newly created skill by interacting with the Amazon Echo connected to the computer running these programs. 
If there is no Amazon Echo available, you can still test your skill using a virtual Amazon Echo located [here](https://echosim.io/welcome?next=%2F).

You can start your skill by asking the Amazon Echo: 
***"Alexa, start \<skill name\>."***

From here you can use your skill by getting Alexa to respond to the Sample Utterances you defined when creating the skill.