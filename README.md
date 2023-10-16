# DotNetMAUIBlazor8RC2Bug
 Example of bug in .NET 8 RC2 loading js script tags

## Bug
This example project tries to use <script>...</script> tags within the body content of a .razor page. .NET 8 RC1 allowed this. However, RC2 seems to ignore the <script> tags within the body even thought they are present in the DOM after blazor renders the page.

 Instructions. Remove the following line from Index.razor:
`<script src="https://unpkg.com/ionicons@5.5.2/dist/ionicons/ionicons.js"></script>`

and place it in `/wwwroot/index.html` (after `<script src="_framework/blazor.webview.js" autostart="false"></script>`)

That will enable the icon in Index.razor to work: <ion-icon name="checkmark-circle-outline"></ion-icon>

## Expected:
![State where the .js library loads](https://github.com/aarondcoleman/DotNetMAUIBlazor8RC2Bug/blob/main/CheckboxAppState.png)

## Current RC2 state:
![State currently where the .js script doesn't load](https://github.com/aarondcoleman/DotNetMAUIBlazor8RC2Bug/blob/main/NoCheckboxAppState.png)

## Implications
This introduces tremendous limitations as many javascript libraries need to be loaded after the body content has loaded. For example, a page with selectors that needs to apply attributes from javascript after the dom is loaded. This breaks the majority of our solution as-is. 
