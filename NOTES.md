Leow's Solutions
-----------------------

1. Bug: "no fillings" text is never displayed when cookies have no fillings

Solution:
- create an if else statement, when cookies have no filling, show "no fillings" error, if cookies have filling, proceed to save the cookie

2. Feature: Cookies should actually be cooked
   We lazily added to Cookie: def ready?; true; end
   But, the cookies are not actually ready instantly! When a cookie is placed in the oven, we need to trigger a background cooking worker to cook the cookies and update their state after a couple minutes of "cooking"

Solution:
- when cookie is saved in the oven
- trigger a timer in ruby and show state: "cooking"
- "refresh the page to show latest status"
- show "done" after a few minutes
- use timestamp
- record "created_at" timestamp
- direct user to "check oven" button first, remove "retrieve" for now
- "check oven" button will compare the time created_at with the current time, if it is 2 minutes and above, direct user to "retrieve" button

Solution 2:
- make changes to def ready? method
- compare time between created_at and "check oven", maybe use method updated_at?


3. Feature: As a bakery owner, I should see the oven page update automatically when the cookies are ready
   Given I have unfinished cookies in an oven
   And I am on the oven page
   Then I should see that the cookies are not yet ready
   When the cookies finish cooking
   Then I should see that the cookies are ready
   Note: Periodic polling is acceptable, but only the relevant part of the page should update

   Solution:
   - polling in Rails

4. Feature: As a bakery owner, I should be able to place a sheet with multiple cookies into an oven
   Given I have an oven
   When I am on the oven page
   Then I should be able to prepare a batch of cookies with the same filling
   When the batch of cookies is finished cooking
   Then I should be able to remove the cookies into my store inventory

5. Feature: As a bakery owner using the mobile web, I want my "Prepare Cookie" button to be first
   Since the Prepare Cookie button is really important, when the bakery owner is using a mobile screen, the prepare cookie button should be the first thing on the oven page. But, on non-mobile browsers, the button should remain where it is currently.
   - isnt this the first thing on the oven page already?