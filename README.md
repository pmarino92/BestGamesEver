# Live Project
Live Project with a team of members using Python, Bootstrap, Django, and Agile methodologies.
# Introduction
For my Python live project at The Tech Academy, I worked with a development team of my peers to create a fully functioning web application through the use of the Django framework. The web application that I created is meant to be a database of user's favorite video games. As a team we shared stories of various difficulty that ranged from backend to frontend as well as UX improvements that needed to be completed. Over the course of the two week sprint I had the opportunity to understand the software development lifecycle as well as implement programming techniques that I'm confident I will use again and again.
# User Stories
* Bootstrap for styling
* Navigation Bar
* Edit and Delete User Inputs
* Beautiful Soup

# Bootstrap
For my live project, I decided to style my web app through the use of Bootstrap. I implemented Bootstrap to style everything from the navigation bar to my database forms. I used Bootstrap because I believe it is easy to setup, a good grid system, and overall is just more flexible than the traditional html/css. Below are some code snippets of my utilization of Bootstrap and how it looked on my project.

```
<div class="container">
        <table class="table table-hover table-dark">
            <thead>
                <tr>
                    <th scope="col" data-field="game" data-sortable="true">Game</th>
                    <th scope="col" data-field="genre" data-sortable="true">Genre</th>
                    <th scope="col" data-field="year" data-sortable="true">Year</th>
                    <th scope="col" data-field="description" data-sortable="true">Description</th>
                </tr>
            </thead>
            <tbody>
            {% for Game in game_list %}
                <tr>
                    <td>{{ Game }}</td>
                    <td>{{ Game.genre }}</td>
                    <td>{{ Game.year }}</td>
                    <td>{{ Game.description }}</td>
                    <td><a href="{% url 'Game_Details' Game.id %}">Details</a></td>
                    <td><a href="{% url 'Edit_Games' Game.id %}">Edit</a></td>
                    <td><a href="{% url 'Delete_Games' Game.id %}">Delete</a></td>
                </tr>
```

[![bootstrap.png](https://i.postimg.cc/rF14PRfq/bootstrap.png)](https://postimg.cc/RN0q3hrY)


