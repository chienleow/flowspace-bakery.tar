Leow's Solutions
-----------------------

1. Bug: "no fillings" text is never displayed when cookies have no fillings

Pseudo Code Solution:
- create an if else statement, when cookies have no filling, show "no fillings" error, if cookies have filling, proceed to save the cookie

2. Feature: Cookies should actually be cooked
   We lazily added to Cookie: def ready?; true; end
   But, the cookies are not actually ready instantly! When a cookie is placed in the oven, we need to trigger a background cooking worker to cook the cookies and update their state after a couple minutes of "cooking"

Pseudo Code Solution (timestamp):
Step 1:
   - when cookie is saved in the oven
   - frontend: display state in haml: "cooking"
   - backend: record "created_at" timestamp when cookie is saved in the oven
Step 2:
   - frontend: "check oven" button, user click on it to check status
   - backend: record "updated_at" timestamp when the "check oven" button is clicked
   - backend: a method to compare "created_at" and "updated_at" timestamps
Step 3:
   - backend: if time difference is more than 2 minutes
   - frontend: display state "done"
   - backend: if time difference is less than 2 minutes
   - frontend: display state "still cooking"
   - frontend: the "retrieve cookie" button will be hidden until the timestamp difference is more than 2 minutes

3. Feature: As a bakery owner, I should see the oven page update automatically when the cookies are ready
   Given I have unfinished cookies in an oven
   And I am on the oven page
   Then I should see that the cookies are not yet ready
   When the cookies finish cooking
   Then I should see that the cookies are ready
   Note: Periodic polling is acceptable, but only the relevant part of the page should update

Pseudo Code Solution (polling in Rails):
   Solution 1: - use JS, update the page so changes can be reflected
   Solution 2: - use Ruby gem(render async)

4. Feature: As a bakery owner, I should be able to place a sheet with multiple cookies into an oven
   Given I have an oven
   When I am on the oven page
   Then I should be able to prepare a batch of cookies with the same filling
   When the batch of cookies is finished cooking
   Then I should be able to remove the cookies into my store inventory

5. Feature: As a bakery owner using the mobile web, I want my "Prepare Cookie" button to be first
   Since the Prepare Cookie button is really important, when the bakery owner is using a mobile screen, the prepare cookie button should be the first thing on the oven page. But, on non-mobile browsers, the button should remain where it is currently.
   - isnt this the first thing on the oven page already?