# Using foreign key as primary key in Ecto

```elixir
  @primary_key {:id, :id, autogenerate: false}
  schema "traders" do
    belongs_to :user, User, foreign_key: :id, primary_key: true, define_field: false

    has_many :assets, Asset
  end
```

or

```elixir
  @primary_key false
  schema "traders" do
    belongs_to :user, User, foreign_key: :id, primary_key: true

    has_many :assets, Asset, references: :id
  end
```

Reference: https://elixirforum.com/t/use-foreign-key-as-primary-key-with-ecto/11668
