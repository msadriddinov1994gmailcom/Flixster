# Flixster


<img src="https://github.com/msadriddinov1994gmailcom/Flixster/blob/master/Images/Cover.jpg" width=3000>


## Table of Contents
1. [Overview](#Overview)
1. [Product Spec](#Product-Spec)
1. [Wireframes](#Wireframes)
2. [Schema](#Schema)

## Overview

### Description

Flixster is a movie browsing app to see a list of trending, currently playing and upcoming movies.

### App Evaluation

- **Category:** Browsing/Entertainment
- **Mobile:** This app would be primarily developed for mobile but would perhaps be just as viable on a computer, such as AMC or other similar apps. Functionality wouldn’t be limited to mobile devices, however mobile version could potentially have more features.
- **Story:**  displays a list of trending, currently playing and upcoming movies. User can change different screens to see trending, upcoming and currently playing movies at theatre.
- **Market:** all-age group
- **Habit:** This app could be used as often or unoften as the user wanted depending on movie watching habits, and what exactly they’re looking for.
- **Scope:** First the app sends a request to MOVIE Database API and handle json response. Then app outlines list of movies. According to user's input, the user can see a list of trending, currently playing and upcoming movies.

## Product Spec

### 1. User Stories (Required and Optional)

**Required Must-have Stories**

- [x] Customers can log in their account
   - [x] create an icon for the app
   - [x] create a splash screen and wait for 20 sec each time the app starts
   - [x] create a server and user table to create an account or get access to an existing account
   - [x] create UI for login activity.
   - [x] connect the app to the server and user table
   - [x] make MainActivity persistent after user logs in.
- [x] Customers can see a list of available cloth for sale
   - [x]  create bottom menu with three fragments such as Catalog, Basket and Profile.
   - [x]  create an item layout for each item.
   - [x]  send a request to the server for posted items.
- [x] Customer can go to checkout and place an online order.
- [ ] Customer can see thier profile which includes information such as address, life-time orders and so on.

**Optional Nice-to-have Stories**

* Customers can add items to a bustket
* Customers can create an address book where they can store thier multiple addresses.
* Customers can cancel orders
* Customers can pay online for orders

### 2. Screen Archetypes

* SplashActivity screen - User signs up or logs into their account. Upon Download/Reopening of the application, the user is prompted to log in to gain access to their profile information to be properly matched with another person.
* Now_playing screen - User can see a list of items for sale and select the quantity of the item and add it to a basket.
* Trendind screen - User can see a list of items in the basket and choose address and payment methods.
* Upcoming screen  - User can see thier profile which cosists of thier basic personal information along side with thier life-time orders and address books.

### 3. Navigation

**Tab Navigation** (Tab to Screen)

* Now_playing screen
* Trending screen
* Upcoming screen

**Flow Navigation** (Screen to Screen)

* Forced SplashActivity -> Account creation if no log in is available.
* Cloth Selection (Or Queue if Optional) -> send a request to server to send back a list of items for sale along side with each item's information.
* Checkout -> show a list of items in thebasket, give user selection of addresses from thier address book, and ask user to fill payment information.
* Profile -> request to a server to send back currentuser info along with thier life-time orders

## Wireframes
<img src="https://github.com/msadriddinov1994gmailcom/Flixster/blob/master/Images/Diagram.png" width=600>

### [BONUS] Digital Wireframes & Mockups
<img src="https://github.com/msadriddinov1994gmailcom/Flixster/blob/master/Images/Screen%201%20-%20Splash.jpg" width=300>   <img src="https://github.com/msadriddinov1994gmailcom/Flixster/blob/master/Images/Screen%202%20-%20Main%20Activity.jpg" width=300>   <img src="https://github.com/msadriddinov1994gmailcom/Flixster/blob/master/Images/Screen%203%20-%20Details.jpg" width=300>


### [BONUS] Interactive Prototype
<img src="https://github.com/msadriddinov1994gmailcom/Flixster/blob/master/Images/Flixster%20Prototype.gif" width=300>

## Schema 

### Models
#### GET


   | Property      | Type     | Description |
   | ------------- | -------- | ------------|
   | movieId       | Integer  | unique id for each movie (default field) |
   | voteAverage   | Double   | rating of item rated by watchers |
   | posterPath    | String   | path for movie poster images |
   | title         | String   | movie's title |
   | overview      | String   | overview of movie |

### Networking
#### List of network requests by screen
   - Now_playing Screen
      - (Read/GET) Query all movies which are currently played at theatre.
         ```kotlin
         val client = AsyncHttpClient()
         client.get(NOW_PLAYING, object : JsonHttpResponseHandler(){
            override fun onFailure(statusCode: Int, headers: Headers?, response: String?, throwable: Throwable?
            ) {
                Log.e(TAG, "onFailure.")
            }

            override fun onSuccess(statusCode: Int, headers: Headers?, json: JSON) {
                try {
                    Log.i(TAG, "onSuccess. $statusCode")
                    val movieJsonArray = json.jsonObject.getJSONArray("results")
                    movies.addAll(Movie.fromJsonArray(movieJsonArray))
                    movieAdapter.notifyDataSetChanged()
                }
                catch (e: JSONException) { Log.e(TAG, "Encountered exception $e.") }
            }

        })
         ```
      - (Read/GET) Query all movies which are trending at theatre.
      - (Read/GET) Query all movies which are upcoming at theatre.

