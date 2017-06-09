# NYTimes

## https://github.com/chefjoannacodes/NYTimes

## Description 
Still working on this project. This is a scraper to gather articles from the NY Times website and add notes to articles you click on. 

## Requirements
#### 
- Create an app that follows this user story:
Whenever a user visits your site, the app will scrape stories from a news outlet of your choice. The data should at least include a link to the story and a headline, but feel free to add more content to your database (photos, bylines, and so on).
- Use Cheerio to grab the site content and Mongoose to save it to your MongoDB database.
- All users can leave comments on the stories you collect. They should also be allowed to delete whatever comments they want removed. All stored comments should be visible to every user.
- You'll need to use Mongoose's model system to associate comments with particular articles.


## Technologies Used
#### 
- node
- express
- express-handlebars
- mongoose
- body-parser
- cheerio
- request

## Code Explaination
- Cheerio and mongoose were primarily used to scrape data from the site. I used Chrome Inspector to select the elements I wanted to display for each article. In this case, it was .story, h3, and p. In the server.js file, the code looked like this:

-------------

```
// Scrape data from one site and place it into the mongodb db
app.get("/scrape", function(req, res) {
  // Make a request for the news section of ycombinator
  request("https://www.nytimes.com/pages/dining/index.html?action=click&pgtype=Homepage&region=TopBar&module=HPMiniNav&contentCollection=Food&WT.nav=page", function(error, response, html) {
    // Load the html body from request into cheerio
    var $ = cheerio.load(html);
    // For each element with a "title" class
    $(".story").each(function(i, element) {
      // Save the text of each link enclosed in the current element
      var title = $(this).children("h3").text();
      // Save the href value of each link enclosed in the current element
      var paragraph = $(this).children("p").text();
```