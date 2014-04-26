### RubyConf 2014 Lightning Talk

# How to deploy your Rails application on Windows

shesee

^ Hello everyone, this is my subject today: How to deploy your Rails application on Windows, and I'm shesee.

---

## shesee

Rails developer @ Taipei

* Ruby Taiwan Community
* Ruby Conf 2014 staff
* Rails Girls Coach
* Traffic-related engineering
* 5xRuby Inc.
* Optimis Corp.

^ I'm now a rails developer at Taipei, and join ruby taiwan community, staff of this conf, and also a rails girls coach

---


### They said

### Rails hates Windows


^ There's much people ever heard of "Rails hates Windows", actually, deployment of rails application is always a problem in Windows operation system.

---
### They said

### Rails hates Windows

# True story.


^ And I'd tell you that's true story, however I could make it easier now.

---

## True stroy


A rails application

needs to be deployed on _**Windows server 2003**_


^ Once I have a chance to deploy an application on a server with Windows server 2003 OS

---

## True stroy


A rails application

needs to be deployed on _**Windows server 2003**_

```ruby
>> 2013.years - 2003.years

=> 10 years
```

^ therefore, this server is over 10 years old.

---

# Enviroment

### 10+ years old machine


* Windows server 2003
* IIS 6

^ About this server, it's not only with Window server 2003, and has IIS 6 on that

---

# There's Plan A

### Helicon Zoo

A repository of web frameworks and applications
for Microsoft IIS

[http://www.helicontech.com/zoo/](http://www.helicontech.com/zoo/)

![original 80% inline](img/helicon_zoo.png)


^ So I decided to google the answer, and I found actually there's a service which called "Helicon Zoo", it's awesome, it seems like we can deploy multiple languages and frameworks on Microsoft IIS, such as Python Ruby Node.js etc.

---

# There's Plan A

### Helicon Zoo

A repository of web frameworks and applications
for Microsoft IIS

## But not for the 10 years old Windows system

^ Unfortunately, Helicon Zoo is only for new version Microsoft solution, it means Helicon is not support me to deploy my rails application in this 10 years old Windows server.

---

### Plan B
## Setting Rails environment

RailsInstaller(http://railsinstaller.org)

![original 80% inline](img/railsinstaller.png)

It's _**simple**_ and friendly for Microsoft users :)


^ So I turn to plan B. First step is to establish rails production environment on this windows server. We can install RailsInstaller, It's simple and friendly for Microsoft users, even in rails girls Taipei we used it to setting students' windows based notebooks.

---

### Plan B
## Setting Rails enviroment

There's a basic rails application,
you might need to be

```
$ gem install bundler
$ gem install rake
$ bundle install
$ rake assets:precompile
```

etc...

^ And there's a basic rails application, also need to install bundler and dependent gems, and do precompile for the rails application.

---

### Plan B
## gem 'thin'

This is our rails application server,
which actually response the request.

```
$ thin --prefix=/yourapp -e production
```

^ I need rails application server to give responses, so we can use default rails application server -- WEBrick, or in this case I choose to use "thin".

---

### Plan B
## Reverse proxy server

This is our plan:
Make IIS 6 been a reverse proxy server !

![original 80% inline](img/reverse_proxy_server.png)

^ to make IIS 6 been a reverse proxy server, first, the IIS server receives the request, and pass it to the rails server "thin", and "thin" give the response to IIS, and IIS feed back to user.

---

### Plan B
## Reverse proxy server - IIS6 with IIRF2.1

We need something
to turn IIS6 to be a reverse proxy server

IIRF 2.1
(http://iirf.codeplex.com/releases/view/58734)

![original 80% inline](img/iirf.png)

^ We need something to turn IIS6 to be a reverse proxy server, it's IIRF 2.1, we can install it and run on IIS server.

---

### Plan B
## East install

_**Next, next and more next**_

![original 80% inline](img/next.gif)

^ It's also easy to setup, just click next next and more next.

---

### Plan B
## Successful <3

Checkout ISAPI status

![original 200% inline](img/ISAPI.png)

^ and checkout the IIS's ISAPI status, if there are green checks, means we install IIRF 2.1 successfully.

---


### Plan B
## Put it under IIS 6

Put the "_**public**_" folder under IIS 6
[Setting its URI]

And adding an _**IIRF.ini**_ (config), it supports regex


^ And we can symbol link the rails application's public folder to IIS server, add an IIRF.ini config file, it supports regex description, to define the outsite request should get replaced inside response.

---


### Plan B
## Put it under IIS 6

Put the "_**public**_" folder under IIS 6
[Setting its URI]

And adding an _**IIRF.ini**_ (config), it suppports regex

### Example

```
RewriteLog AppPath\log\iirf.log

ProxyPass ^/(.*)$      http://localhost:3000/$1 [I]
```

^ this is example, just replace the localhost:3000 as inside responses domain.

---

### Plan B
## Review our action

1. Install _**RailsInstaller**_

^ lets review our steps, at first we have RailsInstaller

---

### Plan B
## Review our action

1. Install _**RailsInstaller**_
2. Install _**bundler**_ & _**gem**_

^ then install bundler and dependent gems

---

### Plan B
## Review our action

1. Install _**RailsInstaller**_
2. Install _**bundler**_ & _**gem**_
3. Install _**IIRF 2.1**_

^ then we install IIRF 2.1

---

### Plan B
## Review our action

1. Install _**RailsInstaller**_
2. Install _**bundler**_ & _**gem**_
3. Install _**IIRF 2.1**_
4. Put on IIS

^ then put the public folder on IIS

---

### Plan B
## Review our action

1. Install _**RailsInstaller**_
2. Install _**bundler**_ & _**gem**_
3. Install _**IIRF 2.1**_
4. Put on IIS
5. Add _**public/iirf.ini**_

^ Magically, only 5 steps we setup a rails application on windows.

---


# Thanks.

## Download this slides


Clone from Github:
_**https://github.com/CarolHsu/Rubyconf2014LT**_


Or Your can find my slideshare:
_**http://www.slideshare.net/hsuc12/how-to-deploy-your-rails-application-on-windows**_

^ And hope you guys have a great conf today. you can also download my slides if you also need to deploy your rails application on windows server one day. I hope not.
