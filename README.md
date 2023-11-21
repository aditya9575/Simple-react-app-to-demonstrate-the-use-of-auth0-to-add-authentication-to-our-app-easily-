# Simple-react-app-to-demonstrate-the-use-of-auth0-to-add-authentication-to-our-app-easily-
This is a simple react app that demonstrates and guides the developer to add authentication via AUTH0

                                                           *FOLLOW THESE STEPS WITH PRECISION*
                       ADDING AUTHENTICATION (LOGIN/LOGOUT)FUNCTIONALITY TO A REACT APPLICATION STEP BY STEP



npx create-react-app appname 

delete unnecessary files and set up the application and test command -> npm run start 

after a successful test run of our react app we now start building a registration , login , authentication functionality 


****************************************************************************************************************************
start by log in on auth 0 site using google account 
then after  go  to applications -> applications 

then select create applications -> name your app -> select react (or single page application option)

NOW in quickstart option select -> REACT 

Then now go to settings and copy the domain and client id and paste it safe somewhere for further use 
DOMAIN:- dev-207zvpre5hjuxtpi.us.auth0.com
CLIENT ID:- EubsY780OxXGGMQkZgkxTogPIuJ4PCAh

Now copy your home page url whatever it is -> http://localhost:3000 
and now paste the copied url in these three options :- Allowed Callback Urls , Allowed Logout Urls , Allowed Web Origins 
and after pasting the url in these three options we now go to the settings page bottom and hit save changes and then go back to the 
previous applications page where we will find out that there has been a new application created as we named it previously 



Now after we see that our application has been created we now tap onto it then select -> quickstart and react option again 



Now we just have to start copy pasting things -> 

start by running the below given installation command for Auth0 SDK -> npm install @auth0/auth0-react

Now we need to wrap our app component with <Auth0Provider/> component so now copy the below component as it is along with its import
statement and then after wrap the app component with it in the index.js file -> 

import { Auth0Provider } from '@auth0/auth0-react';

<Auth0Provider
    domain="dev-207zvpre5hjuxtpi.us.auth0.com"
    clientId="EubsY780OxXGGMQkZgkxTogPIuJ4PCAh"
    authorizationParams={{
      redirect_uri: window.location.origin
    }}
  >
    <App />
    </Auth0Provider>,



=======>NOW SIMPLY WE HAVE TO ADD THE LOGIN FUNCTIONALITY WHICH IS GIVEN IN FORM OF AUTH0 BUTTON IN OUR QUICKSTART DOCUMENTAION PAGE     
YOU CAN ALSO ADJUST THIS BUTTON ACCORDING TO YOURSELF BUT IF WE JUST COPY PAST THE BUTTON CODE ALSO WE WILL GET A LOGIN BUTTON WHICH 
WHEN USED WILL REDIRECT THE USER TO AN CUSTOM DESIGNED AUTH0 LOGIN FORM BY WHICH USER CAN REGISTER AND LOGIN 


******************************************************************************************************************************
we can also setup some authentication rules like minimum and maximum characters required from going onto these options :--> 
authentication -> then database -> then settings 
******************************************************************************************************************************

*============================*
NOW AS WE ONLY WANT  to show the login button once and if the user has login / authenticated successfully then we need to show our 
LOGOUT BUTTON 

So Even this thing is being handled by our auth0 

so if you just simply add your logout button by copy pasting the code from auth0 the logout button will start appearing simultaneously 
with the login button but as we need it only after the authentication and login so we will 

we are sample signing up with this -> 
email-> adityamehto19@gmail.com
password-> Rks-1421



The base page designing used here is that we created an homepage which on render will show a login button with some text and 
as a user logs-in and gets authenticated the text will change as we are using the conditional rendering provided by the auth0 to 
render a logout button on being logged in.


*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=
WE START INSIDE A DIV BY USING CURLY BRACES AND USING THE  isAuthenticated ?  (display this ) : (else display this) conditional render
i.e-> 
      {isAuthenticated ? (
        <div>
          <h1>Welcome {user.name}! Use the button below to logout.</h1>
          <button
            onClick={() =>
              logout({ logoutParams: { returnTo: window.location.origin } })
            }
          >
            Log Out
          </button>
        </div>
      )                       :                     (
        <div>
          <h1>Hello USER, this is our LOGIN PAGE!</h1>
          <button onClick={() => loginWithRedirect()}>Log In</button>
        </div>
      )}

also remember to add the import statement as given in the auth0 docs -> import { useAuth0 } from "@auth0/auth0-react";

and also to remember to destructure these methods from the auth0 component-> 
const { loginWithRedirect, logout, isAuthenticated, user } = useAuth0();

*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=
Finally 
i.e -> 

--------------------------------------------------------------------------------------------------------------------------------------
homepage.jsx code -> 

import React from "react";
import { useAuth0 } from "@auth0/auth0-react";

const HomePage = () => {
  const { loginWithRedirect, logout, isAuthenticated, user } = useAuth0();

  return (
    <div>
      {isAuthenticated ? (
        <div>
          <h1>Welcome {user.name}! Use the button below to logout.</h1>
          <button
            onClick={() =>
              logout({ logoutParams: { returnTo: window.location.origin } })
            }
          >
            Log Out
          </button>
        </div>
      ) : (
        <div>
          <h1>Hello USER, this is our LOGIN PAGE!</h1>
          <button onClick={() => loginWithRedirect()}>Log In</button>
        </div>
      )}
    </div>
  );
};

export default HomePage;

--------------------------------------------------------------------------------------------------------------------------------------
                                                           
