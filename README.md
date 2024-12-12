# EASGraphTheoryJP2024
## Graph Theory Movie Recommendation

# In this digital age, people are exposed to an overwhelming number of entertainment options, especially in the world of movies. Online streaming platforms like Netflix, Disney+, and Amazon Prime host thousands of movies across various genres. For users, it can be challenging to discover new movies that align with their unique preferences. This is where recommendation systems come in—they help users find movies they’re likely to enjoy by analyzing patterns in their previous choices and in the preferences of other users.

# A simple yet powerful approach to building a movie recommendation system involves graph theory. By modeling the relationships between users and movies as a graph, we can use graph traversal techniques to suggest movies based on users with similar tastes.

<br>

**Code**

```
  class MovieGraph:
    def __init__(self):
        #Store graph structure
        self.graph = {}

    def add_user(self, user):
        #Add user node if it doesn't exist
        if user not in self.graph:
            self.graph[user] = set()

    def add_movie(self, movie):
        #Add movie node if it doesn't exist
        if movie not in self.graph:
            self.graph[movie] = set()

    def add_like(self, user, movie):
        #Create like relationship (edge) between user and movie
        self.add_user(user)
        self.add_movie(movie)
        self.graph[user].add(movie)
        self.graph[movie].add(user)

    def recommend_movies(self, user):
        #Find movies liked by similar users
        recommended = set()
        
        if user not in self.graph:
            print(f"User {user} not found.")
            return recommended

        #Movies the user has already seen
        watched_movies = self.graph[user]

        #Go through each movie the user has watched
        for movie in watched_movies:
            #Find other users who liked the same movie
            similar_users = self.graph[movie]
            for similar_user in similar_users:
                #Find movies they liked for each similar user
                for liked_movie in self.graph[similar_user]:
                    #Recommend movies not yet watched
                    if liked_movie not in watched_movies:
                        recommended.add(liked_movie)
        
        return recommended


#Initialize graph and sample data
graph = MovieGraph()

#Add users and movies with their like relationships
graph.add_like("Alice", "Inception")
graph.add_like("Alice", "The Matrix")
graph.add_like("Bob", "Inception")
graph.add_like("Bob", "Interstellar")
graph.add_like("Charlie", "The Matrix")
graph.add_like("Charlie", "Interstellar")
graph.add_like("Charlie", "Avatar")
graph.add_like("David", "Avatar")
graph.add_like("David", "Inception")

#Recommend movies to user
user = "Alice"
recommended_movies = graph.recommend_movies(user)
print(f"Recommended movies for {user}: {recommended_movies}")


  ```

<br>

***Result***
> Recommended movies for Alice: {'Interstellar', 'Avatar'}

## Explanation of Result

For each movie Alice has watched, we find:
- Other users who also like that movie (similar users).
- Movies those similar users like, but Alice hasn't watched.
<br>

- Users who like "Inception":
> Alice, Bob, and David

- Movies liked by these users:

> Alice: Already seen "Inception", "The Matrix"
> Bob: Also likes Interstellar
> David: Also likes Avatar
<br>

- Movies recommended from "Inception":

> Interstellar (from Bob)
> Avatar (from David)
<br>

- Alice has already watched:
> watched_movies = {"Inception", "The Matrix"}
So, movies like "Inception" and "The Matrix" are not included in the final recommendation.

<br>

The unique movies Alice hasn't watched, but are liked by similar users, are:
> {"Interstellar", "Avatar"}
So the Output will be : 
> Recommended movies for Alice: {'Interstellar', 'Avatar'}

<br>

**Graph theory Implementation**

In this recommendation system, I use graph theory to:
-  Represent Users and Movies as Nodes: Users and movies are treated as nodes in the graph.
-  Connect Users to Movies through Likes: When a user likes or rates a movie highly, we create an edge between that user and the movie.
-  Find Paths to New Movies: By traversing the graph along these edges, we identify paths to movies that similar users have watched and recommend those to the target user.

# More Explanation in the PPT

**Conclusion**

In this case, graph theory was applied to model the relationships between users and movies using a bipartite graph (users and movies as nodes, likes as edges). This allowed for an efficient recommendation system, which identified movies liked by users with similar preferences to Alice.

<br>

## Why Use Graph Theory?
- Graph theory provides a structured way to represent and query relationships, especially for complex datasets involving many users and movies.
- It scales efficiently, as the graph allows direct traversal of connections without repeatedly iterating over data structures like lists.

