# Rails API Relationships Diagnostic

Place your responses inside the fenced code-blocks where indicated by comments.

1. Describe a reason why join tables may be valuable.

    ```md
      Join tables can provide insight into the relationship between
      different data tables in the database. It's a way of gathering data on from different parts of the database on one query.
    ```

2. Provide a database table structure and explain the Entity Relationship that
describes a many-to-many relationship for `Profiles`, `Movies` and `Favorites`
(think Netflix). The `Profiles` table would have `given_name`, `surname` and
`email` fields, the `Movies` table would have `title`, `release_date`, and
`length` fields, and `Favorites` would be the join table with references to
`Movies` and `Profiles`.

    ```md
    Profiles: id, given_name, surname, email
    Movies: id, title, release_date, length
    Favorites: id, movie_id, profile_id

    The favorites join table provides a way to store the many to many relationship between profiles and movies by storing their IDs.
    ```

3. For the above example, what needs to be added to the Model files?

    ```rb
    class Profile < ApplicationRecord
      has_many :favorites
    end
    ```

    ```rb
    class Movie < ApplicationRecord
      has_many :favorites
    end
    ```

    ```rb
    class Favorite < ApplicationRecord
      belongs_to :profile
      belongs_to :movie
    end
    ```

4. What is the purpose of a serializer? What would our `Profile` serializer look
  like to show all movies favorited by a profile on
  `http://localhost:3000/profiles/1`

    ```md
  The serializer is a filter. It allows us to format our JSON without messing around with the front end. We can select only the information we want, as well as get access to our relationships with a single request.

    ```

    ```rb
    class ProfileSerializer < ActiveModel::Serializer
      attributes :id, :given_name, :surname, :email
    end
    ```

5. What would the command be to _scaffold_ out a **join table** for Favorites from
  the above `Movies` and `Profiles`.

    ```sh
    bundle exec rails g scaffold favorites movie:references profile:references
    ```

6. What is `dependent: :destroy` and where/why would we use it?

    ```md
    You would use it when you are trying to delete the specific model (all of the parent and children objects - keys and values)>
    ```

7. Think of **ANY** example where you would have a one-to-many relationship as well
  as a many-to-many relationship in an application. You only need to list the
  description about the resources and how they relate to one another.
  ```md
  Creating a jokes API, where one user has access to CRUD his/her jokes. It would be like a personal journal/diary. This would be a One-to-Many.

  A many-to-many example would be a list of patients who have many doctors and many medical staff attending to them.
    ```
