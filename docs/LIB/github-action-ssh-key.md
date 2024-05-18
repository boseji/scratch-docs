# Using a SSH Key in GitHub Action to access private repositories

Source Article <https://www.webfactory.de/blog/use-ssh-key-for-private-repositories-in-github-actions>

Github Action for `ssh-agent` : <https://github.com/webfactory/ssh-agent>

This SSH key can be used also for Checkout action <https://github.com/actions/checkout>

```sh
# Create a New Key for Use
ssh-keygen -t ed25519 -C "comment" -f "output/path/of/key"
```

This key can be **password less** since it would remain
inside the **repository Action secrets**.


----
<!-- Footer Begins Here -->
## Links

- [Back to Root Document](../README.md)
