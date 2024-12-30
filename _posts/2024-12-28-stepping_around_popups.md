---
layout: post
title: Stepping Around popups
subtitle: Fun with Userscripts
cover-img: /assets/img/greasemonkey_logo.jpeg
thumbnail: /assets/img/greasemonkey_logo.jpeg
tags: [userscripts, frontend, javascript]
author: Alex Follette
---

## Stepping Around Popups

### Introduction
Websites that heavily use popups are often best avoided. They are dark patterns designed to manipulate the user, and they may even carry malicious JavaScript payloads—malware. However, some websites may contain valuable information despite these annoyances.

In this case, I want to copy a hash from a webpage. But the JavaScript on the page creates an overlay `<div>` block, meaning any click will redirect me to a spam site instead of interacting with the content I need.

Fortunately, we can combat JavaScript with JavaScript using **userscripts**!

### What Are Userscripts?

Userscripts are browser extensions that allow you to run custom JavaScript on specific domains. This gives you the power to modify the behavior of websites according to your needs. In this case, I'll demonstrate how to automatically copy a hash from a webpage to my clipboard—bypassing unwanted popups and spammy redirects.

### Getting Started

#### Step 1: Install GreaseMonkey or TamperMonkey
First, download and install the **GreaseMonkey** or **TamperMonkey** extension for your browser. I'll be using GreaseMonkey in this example:

- [GreaseMonkey for Firefox](https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/)
- [TamperMonkey](https://www.tampermonkey.net/)

#### Step 2: Create the Userscript

Click on the GreaseMonkey extension icon, and select **Create a New Script**.

Now, we'll write a script to extract the hash from the link and copy it to the clipboard. The website I’m working with contains a link with the hash I need, but JavaScript overlays a popup that redirects me to a spam site when clicked.

Here's the script:

```javascript
// ==UserScript==
// @name     MyHash
// @version  1
// ==/UserScript==
(function() {
    'use strict';

    const link = document.querySelector('a[href*="myhash.com/hash/"]');
    
    if (link) {
        const url = new URL(link.href);
        const hash = url.pathname.split('/')[2];
        
        navigator.clipboard.writeText(hash);
    }
})();
```

### Step 3: define the domain. 

In GreaseMonkey go to the Userscripts options. Ine the include put the domain pattern of your choice. The script will run on every page you open in that domain. Of course, you can disable this by clicking disable on the GreaseMonkey menu. In this example I'll use

```
myhash.com/hash/*

```

which will activate on every webpage that contains a hash I might want to extract!

### Conclusion

Userscripts will allow us to keep on fighting the good fight against dark patterns. This also exemplifies the nature of front end systems. Any information you put on the front end is available to be manipulated and parsed. So, if you have any critical information that you are hiding, hide it in the backend and only give it up when the user provides the appropriate action or credentials... but also don't manipulate the user...
