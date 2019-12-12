# Pyton Class
## Enrich dictionary to use `a['b']` as `a.b`
> The goal is to create a mock class which behaves like a db resultset.

From [here](https://stackoverflow.com/a/1328686/2268280): So what you want is a dictionary where you can spell a['b'] as a.b?

That's easy:

    class atdict(dict):
        __getattr__= dict.__getitem__
        __setattr__= dict.__setitem__
        __delattr__= dict.__delitem__
