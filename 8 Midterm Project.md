## Little fixes and cleanup
 
 - decide if the app is called CineApp or Cine-Scape, update the project accordingly
 - create the option to access the app without loggin in / signing up (log in as guest or demo user or whatever)
 - maybe make the app show up in an 375 x 667 rectangle in the middle of the screen if the screen is bigger than that (right now it gets stretched a lot if opened on desktop)
 - Account Settings:
	 - Account
		 - Change Password - throws errors, i don't think it really changes the password? either fix or hide page
	 - Customization
		 - Favourite Genres is not implemented - maybe remove it
		 - Toggle Dark/Light - not finished, maybe remove it too (Remove the entire Customization tab?)

-bug fix - ask doug about seatsContext!

## Deployment

We should be able to deploy on Vercel and use a Vercel database:
- figure out how to deploy a React app with an Express server backend
- figure out how to make server requests from our frontend to our backend