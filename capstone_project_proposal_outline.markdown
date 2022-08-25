# Capstone project proposal outline

Welcome in my capstone project proposal. After more than a year studying web-development, I am proud to present the project I will support to get my diploma. This project is a web-application in Ruby on Rails and I will develop the back and the front end. 

## Project overview

Travel Tips brings together travels enthusiasts to keep and share their travel memories by listing the places they have visited. 
* You want to keep a beautiful memory of the places you have visited? 
* You look for inspiration to select the places you will visit during your next travel?
* Or you simply want to share the beautiful places you have found?
Travel Tips will be your next best travel buddy just like Google Maps or TripAdvisor with a social dimension. The app is focused on Switzerland. 

## Application purpose

### Never forget a travel you have made 

>*"I sometimes look at pictures from my previous trips without being able to name the restaurant or the place I were. I found it really sad and I hope that I would have one place where I could find the addresses I visited"*
>Dorine, 26 years old, travels more than 5 times per year for her summer vacations and romantic week-end
Keep memories of the places you have visited during your travel. Look for the places and add some personal information like a description, the travel style and information about price range. 
You will be happy to retrieve the details of your travel a few months later. 

### Find the travel inspiration from people like you 

>*"When I organized my city break to Wallis, I remember struggling between the many recommandations from the different ranking websites, blog posts,... I just wished I had a friend that could shared me his best kids friendly addresses"*
>Ilona, 39 years old, travels 2 times per year for her summer vacations and a family week-end

Families with little kids, sportsmen and women, loving couples, we all want to have happy vacations in places that suit us. Find the people that share the same interests and pick their addresses to organize your own best travel. 
Personalize your travel with the places visited by people like you. 

### Share your passion for travelling with a community 

>*"My last trip was amazing. I had found the best addresses to visit in Lucern. I wish I could share all of my addresses with my friends. For the time being I just putted it on a permanent story on Instagram. But that is not the easiest medium to share."*
>Anas, 29 years old, travels more than 10 times per year for city breaks and vacations abroad

Sharing your best recommendations has never been so easy with Travel Tips. Just send the URL of your travel and your friend and your community will be able to retrieve the places you want to share with them. 
No notepad to keep on the phone and to retrieve each time, no time to spend writing the same email again. 

### Help Swiss residents rediscover their country 

>During the pandemic, *"We had a lot more traffic to Switzerland. The articles we wrote about the country worked much better than in other years"*.
>Fabienne Lusier about her blog [Novo-monde.com](https://www.novo-monde.com/) 
>In ["Ces Suisses qui font des road trips en période de Covid", 8 November 2020, RTS](https://www.rts.ch/info/suisse/11730310-ces-suisses-qui-font-des-road-trips-en-periode-de-covid.html)

Covid 19 has changed the way of travelling by encouraging people to rediscover their own country. Between mountains and lakes, peaceful campains and electrical cities, Switzerland offers countless gems to visit. 

Travel Tips aims to highlight thoses riches to inspire every Swiss residents to complate them and live the Swiss experience. Helping people open to a new language and a new environment is the mission of Travel Tips. 

## Front end 

The front end of this web-app will be mobile first and conceived to work easily on a mobile before thinking to the desktop usage. It will be easy to use: my parents should be able to use it as simply as they use applications like Facebook.

[Please find here some mockups (9 views) of the app](https://wireframe.cc/pro/pp/fda83a806402785)

### List of views 

* Home `root_path`

Account related views: 
* Sign up `signup_path`
* Log in `login_path`
* Account `account_path`
* Account edit `edit_user_path`
* User public profile `profile_path`

Travel related views: 
* List of travels `travels_path`
* Travel details `travel_path(id)`
* Create a travel `new_travel_path`
* Edit a travel `edit_travel_path`
* Create a place `new_travel_place_path`
* Edit a place `edit_travel_place_path`

Admin related views: 
* Admin dashboard `dashboard_path`
* List of users `users_path`

Other: 
* About page `about_path`: presentation of the project

### <a name="users_types"></a>Types of users and role description 
#### The visitor 

The visitor has not signed up, he is an anonymous user. 

Main menu content: 
* Travels `travels_path`
* Sign up `signup_path`
* Log in `login_path`

Permissions: 
* Can sign up or log in 
* Consult the travel details pages `travel_path(id)`
* Consult the users public profile `profile_path`
* Use the search bar

#### The user role registered

The user has signed up or logged in. Technically, it means that his session hash is stored by the app. Registered is the default role for any user created in the app. 

Main menu content: 
* Travels `travels_path`
* Account `account_path` 
* Log out (to the controller action `sessions#delete`)

Permissions: 
* Everything that the visitor can do
* Create and edit his owned Travel and the associated Places and delete Place
* Edit his account information 
* Delete his account and all the associated Comments, Travels, Places and favorite Travels
* Log out 
* Comment any Travel and edit his Comment 
* Add and delete any Travel as favorite 

#### The admin 

The admin takes care of the community of users. He has a role that needs to be specified when its profile is created or updated.

Main menu content: 
* Travels `travels_path`
* Account `account_path` 
* Dashboard `dashboard_path`
* Log out (to the controller action `sessions#delete`)

Permissions: 
* Everything that the user can do
* Create, edit and delete any Travel and the associated Places 
* Edit and delete any account  
* Edit and delete any Comment 
* Promote and unpromote any User as admin 
* Access the dashboard `dashboard_path` and the list of Users `users_path`

### Navigation 
#### Header 

Elements: 
* Logo linked to the `root_path`
* Search bar 
* Main menu with different versions cf [Types of users section](#users_types)

#### Home page 

The visitor can access the travels available on the web-app by different filters and call to actions:
* By Swiss regions 
* Last created travels 
* By travel style
* Favorite travels of the community
* Random travel button, cf [Filters section](#filters)
* Search bar 

##### Note on the favorite travels of the community on the home page

The 10 Travels that are the most added as favorite by the Users will be returned. A Javascript feature will allow the user to swipe left or right through the different results. 

#### Footer 

* About `about_path`
* Credits 
* Logo linked to the `root_path`

#### Travel details page 

Related travels are displayed on the bottom of the page. Their are clickable and linked to the travel details page `travel_path(id)`, cf [Related travels section](#related)

### Account related features 
#### Identify 

To create an account on the `signup_path`: 
* Email 
* Password 

Session hash is stored. `User` is created. Redirected to `edit_user_path`
If errors, render the view again with error messages. 

When a User is created, a random username is generated. The User can update it at any time from his `edit_user_path` view. 

To log in on the `login_path`: 
* Email 
* Matching password 

Session hash are stored. Redirected to `account_path`
If errors, render the view again with error messages.  

After clicking on the `Log out` link in the header, Session hash is destroyed and redirect to `root_path`.  

#### Account information

On the `account_path`, the user can find the following information: 
* Avatar 
* Username 
* Email 
* Age 
* Travel Style 
* Description 
* Social media and blog links 
* His travels 
* His favorite travels 
* Button "Delete my account"

#### Account edition 

On the `edit_user_path`, the user can edit the following information: 
* Avatar
* Username
* Age 
* Travel Style
* Description 
* Social media and blog links 

#### User public profile 

The visitors of the website can access a public profile where they can find informations about the traveler `profile_path` as: 
* Username
* Avatar
* Age 
* Travel style 
* Description 
* Links (social media, blog)
* Created travels

The URI will hide the `user_id` for security reasons. 

#### Account deletion

Users can delete their own account from the `account_path` view. 
Only a User with an `admin` role can delete another user account. He can access the delete button from the `users_path`. 
When a User account is deleted, all his owned Travel, Place, Comment and Favorite are deleted too. 

### Admin related features
#### Dashboard 

On the `dashboard_path`, an `admin` role User can access: 
* Number of Travels created since the beginning the app 
* Number of Travels created during this month 
* Number of Travels created during the previous month 
* 10 last Users created 
* 5 last Travels created 
* 20 last Comments
* 5 Users who have posted the highest number of Travels 
* 5 Users who have the highest number of comments 
* 10 Travel that are most added as favorite 
* Link to `users_path`

#### Admin promotion and unpromotion 

On the `users_path`, `admin` can access a list of all the Users of the app paginated by 12 and sorted by `user_id`. For each User card, actions are available: 
* Delete button 
* Edit button 
* Promote or un-promote as `admin`: changes the User's role. After clicking, the DOM is updated with an AJAX request. 

#### Edition, deletion of Travel, Place and Comment access 

* Edit or delete Travel buttons are available on the Travel card (used for example on the `travels_path`)
* Edit or delete Place buttons are available on the `travel_path(id)` for each Place.
* Edit or delete Comment buttons are available on the `travel_path(id)` for each Comment.

*Nb: Edit button for Travel, Comment and Place and delete button for Place are available at the same places for registered users that owned the Travel, Place or Comment instances.*

### Travel related features 
#### Create a travel 

The button to create a new travel is available on `account_path` and `travels_path` (for users).
On `new_travel_path`, a user can create a Travel:
* Name - Required 
* Cover image 
* Description 
* Travel style - Required 
* Cost - Required

The user will have to save the Travel to add Places. After saving his Travel, he will be redirected to `new_travel_place_path`. 

Place is a nested resource of Travel. 

#### Create places 

After creating a travel, the user will access `new_travel_place_path`. To access this view, a travel ID should be passed in the request. If no travel is associated, the user is redirected to `root_path`

He can add as many Places as he wants. For each Place, he needs to fill: 
* Name - That field will be attached to the `Place` and `Autocomplete` object from the Google Map Platform Librairy and will return list of Places (cf [Google Maps Platform section](#gmp)). The user can select a place and alter the name.
* Description 

When selecting the Place in the Google `Autocomplete` object, two hidden field will be filled automatically: 
* Latitude 
* Longitude

After validating the Place, an AJAX request is sent and the Place is added to the DOM with a delete button. 

The form is hidden and the User has to click on an add button to display the form again. During the process of creating a Place, the user can hide of the form by clicking on a button. No data will be saved. 

A button ends the process of adding Places by redirecting to `travel_path(id)`. The button is disabled if a form is displayed. The user has to save his Place or close the form to enable the button. 

#### Edit a travel and delete place(s) 

On the `travel_path(id)`, the user can find the edit and delete button on each Place. 

When editing, the user access `edit_travel_place_path` where he can add new Places, edit or delete existing one. The view is similar to `new_travel_place_path`. 

#### Comment a travel, edit it, delete it 

Users can access a form to send a comment on `travel_path(id)`:
* Body - Required 

An AJAX request updates the DOM after posting a Comment. On each comment that belongs to the user, an edit button is displayed. 

On click on the Edit button, the DOM is modified so the comment is displayed in a form. After clicking on update, an update request is sent and the DOM is modified. 

Comment is a nested resource of Travel. 

#### Search bar 

The search bar will used the visitor's input to look for matching results in the following attributes of the Travel and Place models: 
* Travel name 
* Travel description 
* Travel style 
* Travel region 
* Place name 
* Place description 

#### <a name="filters"></a>Filters 

Here are the filters used on the app to make the navigation in the travels easy: 
* Swiss regions, based on the region attribute of the Travel model. Returns last created Travels first. 
* Last created travels
* By style, based on the `travel_style` attribute of Travel model. Returns last created Travels first. 
* Favorite travels of the community, returns the most added as favorite Travels. 

These lists are accessible behind a button on the `root_path`. The buttons are disabled if no records match the filter.

The Random travel button lets you access a random travel details page `travel_path(id)` by generating a random number. The button is available on the `root_path`.

#### List of travels 

On `travels_path`, Travels are presented by cards with the following elements: 
* Name 
* Cost 
* Travel style 
* Show more button linked to `travel_path(id)`

If the user is logged, calls to action are displayed on the card: 
* Edit button 
* Delete button (if `role` is `admin`) 
* Add as favorite button 

The instances are paginated by 12. 

Travel style filters are available on the top of the page. On click on the filter, the DOM is modified by a Javascript function and only the matching Travels are displayed. 
The buttons are disabled if no records match the filter.

#### Travels details 

On `travel_path(id)` following elements are available: 
* Travel Name (`name`)
* Travel Description (`description`)
* Travel Cover image (`cover_img`)
* Username (`username`, linked to `profile_path`)
* User avatar (`avatar`, linked to `profile_path`)
* Travel Region (`region`) 
* 1 Map from Google Map Platform with one Marker for each Place (`latitude` and `longitude`)

For each Place that `belongs_to` the Travel instance: 
* Place name (`name`) 
* Place description (`description`)

#### <a name="related"></a>Related travels

On `travel_path(id)` related travels are displayed by the region criteria and most added as favorite. 

If no Travel matches the criteria, the most added as favorite travels will be returned. 

#### Add a travel as favorite 

The button is available on the Travel card and and the `travel_path(id)`. When the Travel is added as favorite, the button is changed by an AJAX request. If the user click again the association is deleted and the DOM is updated with an AJAX request. 

### Other features
#### Locales 

The `root_path` of the website will be available on 3 languages: 
* English (default)
* French 
* German 

The user generated contents will not be translated. 

## Data structures and models

Here is a description of the different Models and the data structure of the application. 

### Travel 

* has_many Places
* has_many Comments
* belongs_to User

| Attribute | Type | Comment |
| --- | --- | --- |
| `name`| String | Required |
| `cover_img` | String | Required and managed by BCrypt Gem |
| `description` | String | Length max 300 |
| `travel_style` | String | Required, in: family, sport, couples, city break |
| `cost` | Integer | Required, in : 1, 2, 3, 4 |
| `region` | String | Required, in: Région lémanique - VD, VS, GE; Espace Mittelland - BE, FR, SO, NE, JU; Nordwestschweiz - BS, BL, AG; Zürich - ZH; Ostschweiz - GL, SH, AR, AI, SG, GR, TG; Zentralschweiz - LU, UR, SZ, OW, NW, ZG; Tessin - TI |

### Places 

* belongs_to Travel
* belongs_to User

| Attribute | Type | Comment |
| --- | --- | --- |
| `name`| String | Required |
| `latitude` | Float | Required |
| `longitude` | Float | Required |
| `description` | String | Length max 300 |

### User 

* has_many Travels 
* has_many Places
* has_many Comments

| Attribute | Type | Comment |
| --- | --- | --- |
| `email` | String | Required and unique |
| `password` | String | Required and managed by BCrypt Gem |
| `username` | String | |
| `avatar` | String | Managed by CarrierWave Gem |
| `age` | Integer | |
| `travel_style`| String | In: family, sport, couples, city break |
| `description` | String | Length max 300 |
| `insta_url` | String | |
| `fb_url` | String | |
| `tiktok_url` | String | |
| `blog_url` | String | |
| `role` | String | In: admin, registered - Default: registered |

### Favorite 

* Has_and_belongs_to_many Users and Travels

### Comments 

* Belongs_to User
* Belongs_to Travel

| Attribute | Type | Comment |
| --- | --- | --- |
| `body` | String | Required |

## Third party services

List of the third party services used for this project: 
* Google Maps Platform (GMP) the Javascript API
* Material Design Lite library
* Ruby gems: Postgres, Kaminari, Bcrypt, CarrierWave, Figaro, Fog AWS
* Heroku and AWS S3 Bucket for deployment 

### <a name="gmp"></a>Google Maps Platform (GMP)

The Google Maps API will provide us an access to a map service and a database of places. 
*"Note: As defined by the Places API, a 'place' can be an establishment, a geographic location, or a prominent point of interest."*, Google Developer Documentation

#### App functionnal requirements

* As an application, I should be able to display a map.
* As a user, I should be able to find places by typing a request (string format) in a search field. 
* As a user, I should be able to choose one place if many places are returned by the API. 
* As an application, I should be able to stock selected places in the database. 
* As an application, I should be able to access the places saved in the app to display them on the map.

#### Documentation 

Google Documentation:
* [Documentation developers](https://developers.google.com/maps/documentation/javascript/get-api-key)
* [Google Cloud page for products](https://cloud.google.com/maps-platform/products)
* [Getting started with Google Maps Platform](https://developers.google.com/maps/gmp-get-started#create-project)
* [Documentation Maps Javascript API](https://developers.google.com/maps/documentation/javascript/overview?)
* [Documentation Autocomplete](https://developers.google.com/maps/documentation/javascript/places-autocomplete)
* [Documentation Places](https://developers.google.com/maps/documentation/javascript/places)

#### Maps Javascript API

Display interactive maps. Places API and Autocomplete are loaded as libraries. Need an account on Google Maps Platform and an API key to use the services. 

Basic elements needed in the code of the app: 
* HTML: HTML5 declaration + container for the map 
        <div id='map'></div>
* CSS: set 100% height for `.map`, `html`, `body` elements
* Javascript functions are stored in `assets\javascript\places.js`
List of the output needed to generate a map and Marker: 
* Google `LatLng` object: takes a latitude and longitude as parameters
* Google `Map` object: takes `LatLng` object and `zoom` as parameters
* Google `Marker` object: takes `LatLng` and `Map` objects as parameters

Create maps in views: 
1. Store the API key in `config\secret.yml` with the key `google_maps_api_key`
2. Call the API in the `view\layouts\application.html.erb`file with the key
        <%= javascript_include_tag "https://maps.googleapis.com/maps/api/js?key=#{Rails.application.secrets.google_maps_api_key}&callback=initMap&libraries=&v=weekly", defer: true %>
3. In the `view\layouts\application.html.erb`, allow to custom the header with specifics for each view
        <%= yield(:head_tags) %>
4. In the views, call at the open a block of the file `provide :head_tags do` to pass the specific header parameters for the view. Between `script` tags, call the different functions needed with the Rails instances of Place as parameters. 

Create a map with many Markers: Push latitude and longitude of the Place instance in an array stored in an array.
Things to figure during project development:
* When many Markers, find a way to set the center and zoom based on the different place, if impossible, set the center based on the first place and the zoom with a default value. 
* Pass the name of the place to display it on the map 

##### Places Library

Access detailled information about places. 
How to use the Place object in the app: 
1. In the URL used to call the API, ensure you pass the parameter `&libraries=places` and set the Google Maps Platform account to enable the use of Places library
2. With the `Autocomplete` class (see autocomplete section for more details), `getPlace()` and get the different text inputs of your document
3. Access the info needed in the `Place` object: `place.name`, `place.geometry.location.lat()` and `place.geometry.location.lng()`
4. Alter the value of the input fields selected and set their value with the values retrieved from the `Place`object

##### Autocomplete for addresses and search terms

Suggests Places based on user input in a text field.
Extract of the documentation: 
* `Autocomplete`class: create a text input field monitored. Returns place predictions as dropdown list. Return a Place with getPlace() request.
* `Autocomplete`takes 2 arguments: HTML `input` element type text and `options`: possible to set a specific type of places or a specific area like a country - We will use this feature to focus the search on Switzerland. 

Function to create an autocomplete in the `assets\javascript\places.js`:
* Call the `Autocomplete` Google object and pass the input field as parameter
Implementation in the view: 
* Search field tag `<input id="searchTextField" type="text" size="50" placeholder="Anything you want!">`
* In the `provide :head_tags do` block, call the `autocomplete` function 
Get the `Place` object selected by the user: 
* Create an event `place_changed` 
* Add `addListener` on the `Autocomplete` object that triggers the `getPlace()` function

Things to figure during project development:
* Use of options: set the area only on Switzerland 
* Style of the field: [Style the field with CSS class](https://developers.google.com/maps/documentation/javascript/places-autocomplete#style-autocomplete)

#### Rails Gems for the GMP API

> Integration with Ruby can be made with Gems. I won't use them because:
> * The Google Documentation is clear and integration seems manageable without a Gem
> * Google can update its API and my app won't work until a new release of the Gem is made
> * Existing Gems require some settings in Javascript when the expected behavior is not the default one. 
> Since the information found about Gems can still be useful for my implementation without Gem, here are some notes. 

##### Existing Gems 

* [Google_Maps](https://github.com/9peso/google_maps)
* [GMaps4Rails](https://github.com/apneadiving/Google-Maps-for-Rails) / [tutorial](https://www.youtube.com/watch?v=R0l-7en3dUw&feature=youtu.be) / [Gmaps4Rails tutorial on a blog](https://melvinchng.github.io/rails/GoogleMap.html#65-dynamic-map-marker)
* [Google Maps](https://github.com/zilverline/google-maps)

##### Some resources

* [Store the credentials in Rails `Credentials`](https://pjbelo.medium.com/using-google-maps-api-v3-with-rails-5-2-b066a4b2cf14)
  [Encryption mechanism for Rails 5.1](https://guides.rubyonrails.org/5_1_release_notes.html#encrypted-secrets)
* [An example of the integration I want to do](https://gorails.com/episodes/google-maps-places-autocomplete-with-rails)
* [Feedback from a developer about Gems](https://www.wearefine.com/news/insights/planning-your-next-google-maps-project-part-1)

### Material Design Lite (MDL)

Why using a library for the components: 
* Training to use different front end libraries 

Why MDL: 
* Since the app is a Google Maps with social features, it makes sense to use a Google library
* Created to share the vision of a more usable web (UI and UX approches)
* Backed up by Google 
* Degradation in oldest browser
* Working on the BEM methodology 
* Optimized for cross-device usage 
* Rely on CSS, HTML and Javascript 
* Customizable 

#### Resources

* [MDL documentation](https://getmdl.io/index.html)
* [Material Icons Guide](http://google.github.io/material-design-icons/)

#### MDL usage

MDL files are stored in the assets pipeline of the app. The Material Icons need to be called in the application.html.erb file. 
Components used: 
* Buttons 
* Cards 
* Loading > while GMP API is loading
* Snackbar > when an element is deleted
* Toggle > Icon toggle when a trip is added by a user 
* Text fields 
* Tooltips > explain usage of an icon

##### Cards specific usages

Cards will be used for the display of: 
* Travel 
* User 

Some customization will be made on the Travel Cards to add: 
* Informations will be added: cost, travel style as `mdl-card__supporting-text`
* Calls to action (if the user is logged): edit, delete (`admin` roles only) and add as favorite button

Some customization will be made on the User Cards to add: 
* Add a delete button 
* Add an edit button 
* Add a promote or un-promote as `admin` button

##### Loading 

To enhance the user experience while waiting for Google Maps API calls responses, a visual indicator of loading will be used to inform the visitor or user that activity is ongoing. 
The Spinner will be used. A Javascript function will change the class of the Spinner container by adding `is-active` to make the Spinner visible. 

##### Snackbar 

When a User clicks on a button to delete an instance (like Travel or User), the Snackbar will be called to give the User confirmation about the action performed. 
The message and timeout properties will be defined in the Javascript function called. 

##### Icon toggles 

Icon toggle will be used on the Travel Card component when User has logged in to add or un-add a Travel as favorite. The icon will have the `Icon on` look when the Travel has been added by the User as favorite and the `Icon off` look when not. 

##### A flexible and adaptative layout without Material Lite Design 

Because the application needs to be adaptative to many devices sizes, Flexbox will be used to organize the different components of the application. It is also a good occasion to practice Flexbox to create quick responsive layouts.  

### Ruby Gems 

Here is a list of all Ruby Gems needed for the app: 
* Postgres > connect the database and app for production 
* Kaminari > pagination 
* Bcrypt > password encryption
* CarrierWave > images upload
* Figaro > store keys
* Fog AWS > use AWS

### Heroku and AWS S3 bucket 

The app will be deployed on Heroku because of the easy usage for Rails app. Since Heroku doesn't allow images upload by users, AWS S3 will be plugged to the app to be used as a storage solution for images. 