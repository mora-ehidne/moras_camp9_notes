# Cache

Cache stores resources fetched via the HTTP GET method.
The cache can store files of any type or size.

# Cookies

Cookie is a format for storing small bits of information from the backend in the frontend - in the client's browser.

It only stores strings (so eg. JSON data can be stringified and saved in a cookie).

It is used to store information such as:
 - UI presets for a website (color scheme etc.)
 - Information for page navigation (settings, favorites etc)


# Local Storage

Local storage is used for storing temporary data from the frontend, such as the current contents of a form etc. 
Local storage cannot be accessed from the backend.

Local storage persists between browser sessions and items from it can be deleted either from the frontend or from the browser settings.

Sensitive data, such as user data should not be saved in local storage as it is not very safe.