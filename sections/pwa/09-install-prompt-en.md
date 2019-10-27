# app installation

## app installation

Browsers may offer the ability to add entries to the device's start menu / to the homescreen

## app installation on Chrome and iOS

In iOS users can add any website to the phone's menu. The mechanism for PWAs is the same.

On Chrome PWAs may prompt the user to be installed. Installed PWAs will behave differently from websites - e.g. they will be displayed in a standalone window.

## app install prompt

App install prompt on Chrome:

https://developers.google.com/web/fundamentals/app-install-banners/

## app install prompt

requirements to show the prompt:

- manifest file includes:
  - _short_name_ or _name_
  - 192px and 512px icons
  - _start_url_
  - _display_ must be one of _fullscreen_, _standalone_, _minimal-ui_
- served via HTTPS
- has a service worker (with a fetch event handler)
- user has interacted with the domain for at least 30 seconds

## app install prompt

once all the requirements are met, a `beforeinstallprompt` event will fire; we can listen for this event and store it for later use

```js
let installPromptEvent;

window.addEventListener('beforeinstallprompt', event => {
  // the browser is ready to show the install prompt
  event.preventDefault();
  installPromptEvent = event;
  showInstallBtn();
});
```

## app install prompt

Once the user wants to install the app, we can use the stored event:

```js
installBtn.addEventListener('click', () => {
  hideInstallBtn();
  // Show the prompt
  installPromptEvent.prompt();
});
```

## deployment

We can test a deployment on https://app.netlify.com/drop

important: Switch to HTTPS in the Browser