# Sublime Text Snippets

Sublime Documentation <https://docs.sublimetext.io/guide/extensibility/snippets.html>
Source <https://www.geeksforgeeks.org/how-to-create-snippets-in-sublime-text/>

- Go to the `Tools` menu
- Go to the `Developer` option and click on `New Snippet`. A Snippet file will be open with some pre-written code with `.sublime-snippet` extension.
- Add your snippet inside the `![CDATA[` section. The `${1}` are the tab stops for updating or predefined values.
- Enable the `<TabTrigger>` This would be the trigger binding.
- In case you need enable the `<scope>` This would narrow down the locations from where the snippet can be triggered. You can find the scope from `Tools->Developer->Show Scope Name` or press `Ctrl+Alt+Shift+p`. Copy the scope name and paste into the `<scope>` location.
- Finally Save the file.

Typically the files are stored under the `Package/User` directory of the 
Sublime Text configuration.

On Linux its Typically `~/.config/sublime-text/Packages/User/` directory.

Here is the syntax from a Markdown Snippet file:

```html
<snippet>
	<content><![CDATA[

----
<!-- Footer Begins Here -->
## Links

- [Back to Root Document](../README.md)

]]></content>
	<!-- Optional: Set a tabTrigger to define how to trigger the snippet -->
	<tabTrigger>mml0</tabTrigger>
	<!-- Optional: Set a scope to limit where the snippet will trigger -->
	<scope>text.html.markdown</scope>
</snippet>
```

----
<!-- Footer Begins Here -->
## Links

- [Back to Root Document](../README.md)

