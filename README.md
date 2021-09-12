# Live Project <a id="top"></a>
Live Project with a team of members using Python, Bootstrap, Django, and Agile methodologies.
# Introduction 
For my Python live project at The Tech Academy, I worked with a development team of my peers to create a fully functioning web application through the use of the Django framework. The web application that I created is meant to be a database of user's favorite video games. As a team we shared stories of various difficulty that ranged from backend to frontend as well as UX improvements that needed to be completed. Over the course of the two week sprint I had the opportunity to understand the software development lifecycle as well as implement programming techniques that I'm confident I will use again and again.
# User Stories 
* [Bootstrap for styling](#bootstrap)
* [Navigation Bar](#navigation-bar)
* [Edit and Delete User Inputs](#edit-and-delete-functions)
* [Beautiful Soup](#beautiful-soup)

# Bootstrap <a id="bootstrap"></a>
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

# Navigation Bar <a id="navigation-bar"></a>
I was able to create a functioning navigation bar that redirects users to the database of entries as well as the ability to create new games for said database. I also employed bootstrap to style the nav bar as well as the footer to provide a symmetrical UI design for anyone who visits the site.

```
<head>
    <meta charset="UTF-8">
    <title>{% block title %}{% endblock %}</title>
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
    <link rel="stylesheet" href="https://unpkg.com/bootstrap-table@1.18.3/dist/bootstrap-table.min.css">
    <link rel="stylesheet" href="{% static 'css/games.css' %}">
</head>
<body>
    <!-- NAV BAR -->
    <nav>
        <ul>
            <li><a href="{% url 'BestGamesEver_Home' %}">Home</a></li>
            <li><a href="{% url 'Game_Create' %}">Add Game</a></li>
            <li><a href="{% url 'Game_View' %}">View Games</a></li>
            <li><a href="{% url 'View_Price' %}">View Prices</a></li>
            
        </ul>
    </nav>
    
   ```
# Edit and Delete Functions <a id="edit-and-delete-functions"></a>
I allowed for edits and deletion of entries through the use of model forms and instances that displayed the content of a single item from the database as well as a deletion confirmation alert to the user.

```
def Edit_Games(request, game_id):
    item = get_object_or_404(Game, id=game_id)
    form = GameForm(data=request.POST or None, instance=item)
    if request.method == 'POST':
        if form.is_valid():
            form.save()
            return redirect("Game_View")
    content = {'form': form}
    return render(request, 'BestGamesEver/Game_Edit.html', content)


# Function to delete an entry
def Delete_Games(request, game_id):
    item = get_object_or_404(Game, id=game_id)
    form = GameForm(data=request.POST or None, instance=item)
    if request.method == 'POST':
            item.delete()
            return redirect("Game_View")
    content = {'form': form}
    return render(request, 'BestGamesEver/Game_Delete.html', {'item': item, 'form': form})
 ```
 
 # Beautiful Soup <a id="beautiful-soup"></a>
 I employed web scraping with the use of Beautiful Soup to scrape data from Amazon to give current video game prices. While this was one of the more challenging aspects of my project, I was able to print out the video game title as well as the price in dictionary form through the use of two functions. The first function (get_html_content) would scrape the specific game's current price from amazon which would pass the information to the second function(View_Price) to display the content to the user.
 
 ```
 def get_html_content(game):
    USER_AGENT = "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/44.0.2403.157 Safari/537.36"
    LANGUAGE = "en-US,en;q=0.5"
    session = requests.Session()
    session.headers['User-Agent'] = USER_AGENT
    session.headers['Accept-Language'] = LANGUAGE
    session.headers['Content-Language'] = LANGUAGE
    game = game.replace(' ', '+')
    html_content = session.get(f'https://www.amazon.com/s?k={game}&ref=nb_sb_noss_2').text
    return html_content


# Beautiful Soup Function
def View_Price(request):
    game_data = None
    if 'game' in request.GET:
        # Fetch game data
        game = request.GET.get('game')
        html_content = get_html_content(game)
        soup = BeautifulSoup(html_content, 'html.parser')
        # Setting our variable to dictionary form
        game_data = {}
        # Will display name of the game and current price
        game_data['title'] = soup.find('span', attrs={'class': 'a-size-medium a-color-base a-text-normal'}).text
        game_data['price'] = soup.find('span', attrs={'class': 'a-offscreen'}).text

    return render(request, 'BestGamesEver/View_Price.html', {'game': game_data})
 
 ```
 *Jump to [Bootstrap for styling](#bootstrap), [Navigation Bar](#navigation-bar), [Edit and Delete User Inputs](#edit-and-delete-functions), [Top](#top)


