## Blazor Deferred Remove

Wait for CSS Transitions or Animations to complete, before removing your Blazor UI.
Allows you to achieve fadeout effects etc in your blazor applications.

[![Build Status](https://dev.azure.com/darrelltunnell/Public%20Projects/_apis/build/status/dazinator.BlazorDeferredRemove?branchName=master)](https://dev.azure.com/darrelltunnell/Public%20Projects/_build/latest?definitionId=8&branchName=master)

## Usage

1. Add the `BlazorDeferredRemove` nuget package to your blazor project.

2. Include the following js script on your index.html page:

```html
    <script src="_content/BlazorDeferredRemove/BlazorDeferredRemove.js"></script>
```

3. In your blazor page / component you can now wrap your content in a `RemoveOnCssTransitionEnd` or `RemoveOnCssAnimationEnd` component, to have some UI that will be removed from the render tree only after a CSS property transition or CSS animation has completed respectively.

## Example

The following example renders some UI that will be removed once a CSS property transition has completed for `visibility` property:

```

@page "/"

<RemoveOnCssTransitionEnd CssPropertyName="visibility">
    <div class="@GetClassName()">
        <p>Hey there!</p>
        <button @onclick="()=>Done()"></button>
    </div>
</RemoveOnCssTransitionEnd>

@code{

    [Parameter]
    public bool StartTransition { get; set; } = false;

    public void Done()
    {
        StartTransition = true;
    }

    public string GetClassName()
    {
        return StartTransition ? "fadeout" : "";
    }
}

```

And here is the CSS required for this example:

```
.fadeout {
    visibility: hidden;
    opacity: 0;
    transition: visibility 0s 2s, opacity 2s linear;
}

```

Ofcourse, if you have common transition or animation effects - there is nothing to stop you from deriving your own components from `RemoveOnCssTransitionEnd` or `RemoveOnCssAnimationEnd` components.
