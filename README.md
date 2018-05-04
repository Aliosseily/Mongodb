# MyBlog

Please make sure that you have completed and UNDERSTOOD the following tutorial [https://zellwk.com/blog/crud-express-mongodb/](https://zellwk.com/blog/crud-express-mongodb/) before starting this exercise.

You may refer to this tutorial throughout this exercise.

Done? Great, Let's start!

## Getting Started

- Create a folder for this project. Initialize npm to manage dependencies. Create a `server.js` file inside this folder.
- Create an app that uses `express` and `body-parser` and listens on port `3000`
- Install Nodemon and create a script in `package.json` to use it
- Install `MongoDB`, connect to it and create a Database on `MongoLab`. 
- Make sure that your app `only` listens when the database is connected
- Create an `index.html` file that contains a form as follows:
  - action `'/posts'` and method `post` 
  - input field of type `text` with placeholder `"Title"` and a name `"title"`
  - textarea of type `text` with placeholder `"Text"`, a name `"text"`, rows `"5"`, and cols `"50"` 
  - input of type `submit`

- Send the above file on the main page `'/'`
- Using *`save()`* function, save the data submitted through this form in the database. Remember that your form action is `'/posts'` and your form method is `post`


- Using *`find()`* and *`toArray()`* functions, display the data you have in the database on the console

- Install `ejs` and set it as the `view engine`
- Create a directory named `views` and create `index.ejs` file inside it
- Copy the code you have inside `index.html` to `index.ejs` and delete `index.html`
- using *`render()`* function and an `ejs` code that you will write, display the data you have in the database on the main page `'/'` as follows:
   - The form be displayed on the `left` part of the page
   - Posts should be displayed on the `right` part of the page as: `h3` for title and `p` for text of each post

Congratulations! You successfully applied everything you learned in the tutorial.

## Edit and Delete Posts

Now that you can add posts, let's make the user able to delete and edit them.
- Delete
   - Add an anchor `<a>` under each post of href `'delete/id' with id being the id of the post selected`. *Remember that `MongoLab` sets a default id for each post*
   - Handle this link in `server.js` using `app.post(/delete/:id)` where you delete the selected post from database using *`delete()`* function and render to `'/'` page
- Edit
  - In views, create `update.ejs` page that contains a form as follows: 
    - action `'/update/id'` and method `post`
    - input field of type `text` with placeholder `"Title"`, name `"title"`, and value of the old title 
    - textarea of type `text` with placeholder `"Text"`, name `"text"`, rows `"5"`, cols `"50"`, and value of the old text
    - input of type `submit`
  - Add an anchor `<a>` under each post of href `'edit/id' with id being the id of post selected`. *Remember that `MongoLab` sets a default id for each post* 
  - Handle this link in `server.js` using `app.post(/edit/:id)` where you find the post that the user looking for using *`findOne()`* function and render the result to `update.ejs`
  - The form in `update.ejs` has `'/update/id'` as action, this should also be handled in `server.js` using `app.post(/update/:id)` Use *`findOneAndUpdate()`* function to set the new values for `Title` and `Text` as entered by the user
         
  Congratulations! You can now Add, edit and delete posts from a database.
  
## Sorting Posts

Now, the user shall be able to sort the posts by ID (default sorting), title (alphabetical order) or date.
- Delete all your posts to avoid any type of conflict.
- Go to `index.ejs` and add the following:
    - An input field to the form of type `hidden` id `date` and name `date` 
    - The following script
    ```js
    n = new Date(); // get current date
    // formatting the date
    h = n.getHours();
    M = n.getMinutes();
    y = n.getFullYear();
    // getMonth() counts January as 0 so we need +1 
    m = n.getMonth() + 1;
    d = n.getDate();
    //check if it's AM or PM
    if (h < 12){
    document.getElementById("date").value = h + ":" + M + " AM " + m + "/" + d + "/" + y;
    }
    else {
        document.getElementById("date").value = h + ":" + M + " PM " + m + "/" + d + "/" + y;
    }
    ```
    This step allowed us to send the `date` when the post was added
- Now, in `index.ejs` add 3 anchors `<a>` above the posts as follows:
    - Sort by Id with `href = "/default"`
    - Sort by Title with `href = "/title"`
    - Sort by Date with `href = "/date"`
- Handle these links in `server.js` by adding `:sorting?` to `app.get('/')`. The question mark means that this parameter is optional (not required). Using *`find()`* and *`sort()`* functions, sort the posts based on which anchor is pressed. 

Congratulations! You created a full Blog.

## Read More

Only display the first 3 words of each post on the `index.ejs` page and give the option for the user to read full post on another page `read.ejs`. Use *`split()`*, *`slice()`* and *`join()`* functions.

## Optional

For those who want to have more fun, here are some additional tasks you might find interesting.

#### Pagination

Limit the number of posts displayed on one page to 3 posts. If there are additional posts, the user has the option to move between pages (there will be 2 anchors next and previous). Use *`limit()`* and *`skip()`* functions.