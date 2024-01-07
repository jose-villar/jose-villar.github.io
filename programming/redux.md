- Reducers are pure functions (with the same input, they always return the same
  output, they don't mutate the arguments, they don't have any side effects).
  They get the current  store instance and return an updated one.

- The action should be an object with a type and a payload.

## Recommended structure of a redux store

~~~
{
    entities: {
        tags,
        categories,
        ...
    },
    auth: {
        user: {... },
        token: {...}
    },
    ui: {
        tags: {
            query:"...",
            sortBy: "..."
        }
    }
}
~~~
