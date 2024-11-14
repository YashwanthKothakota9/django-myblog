- A `slug` is a short label that contains only letters,
numbers, underscores, or hyphens.

- `BigAutoField` is `64-bit` integer that automatically increments according to available IDs.

- `timezone.now` returns current datetime in a timezone-aware format.

- To use database-generated default values, we use the `db_default` attribute instead of `default`.

- By using `auto_now_add`, the date will be saved automatically when creating an object.

- By using `auto_now`, the date will be updated automatically when saving an object.

- `Meta` class defines metadata for the model.
  
- `Index ordering` is not supported on `MySQL`. If you use
MySQL for the database, a descending index will be created
as a normal index

- We use `related_name` to specify the name of the reverse relationship, from `User` to `Post`. This will allow us to access related objects easily from a user object by using the `user.blog_posts` notation.

- The `sqlmigrate` command takes the migration names and returns their SQL without executing it.

- We can specify a custom database name for your model in the `Meta` class of the model using the `db_table` attribute.

Django creates an auto-incremental id column that is used as the primary
key for each model, but you can also override this by specifying `primary_key=True` on one of your model fields. The default `id` column
consists of an integer that is incremented automatically. This column
corresponds to the `id` field that is automatically added to your model.

- `facet counts` indicate the number of objects corresponding to each specific filter.