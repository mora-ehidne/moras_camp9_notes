# Cache

Cache stores resources fetched via the HTTP GET method (images, HTML, CSS, etc).
The cache can store files of any type or size.

The goal of caching is to make subsequent visits to the website faster, as some data is already in local memory and doesn't have to be downloaded again. (improves website performance)

Disk caching stores data in the hard drive, memory caching stores data in the RAM.

# Cookies

Cookie is a format for storing small bits of information from the backend in the frontend - in the client's browser.


It is used to store information (often stateful information) such as:
 - Personalisation/User preferences (color scheme, preferred language etc.)
 - Information for page navigation (settings, favorites etc)
 - Contents of an online shop cart
 - Session management
 - Tracking

On subsequent page visits, cookies are sent back from the frontend to the server in order to update some user information.

Cookies are stored in the `Cookies` browser object. Cookies are also objects, with several properties, most importantly the name (string) and the value (also string).
Other properties are: domain, path, expiration date etc.
As cookies only store string values, JSON data can be stringified and saved in a cookie.


# Local Storage

Local storage is used for storing temporary data from the frontend, such as the current contents of a form etc. 
Local storage cannot be accessed from the backend.

Local storage is an object whose key-value pairs can be set (both strings).

Local Storage can be directly and simply accessed via JS:
`localStorage.setItem(key, value)`
`localStorage.getItem(key)`
`localStorage.removeItem(key)`


Local storage persists between browser sessions.
Local storage items can be deleted either from the frontend (the website deleted it itself) or by the user, from the browser settings.

Sensitive data, such as user data should not be saved in local storage as it is not very safe.

# Session Storage

Works similiarly to Local Storage, except that it gets cleared when the user closes the tab or browser.

It can also be accessed by JS:
`sessionStorage.setItem(key, value)`
`sessionStorage.getItem(key)`
`sessionStorage.removeItem(key)`

