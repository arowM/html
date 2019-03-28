# elm/html with Attributes.batch

An elm/html alternative which enables you to batch attributes.
The compatible elm/html version is `1.0.0`.

Quickly render HTML in Elm.

## What's the difference from elm/html?

The only difference is that this library exposes `Html.Attributes.batch` and `Html.Attributes.none`.

* `Html.Attributes.batch` enables you to flatten list of attributes
* `Html.Attributes.none` does nothing

```elm
import Html as Html exposing (Html, Attribute)
import Html.Attributes as Attributes
import Html.Events as Events


mixin : msg -> Attribute msg
mixin onClick =
    Attributes.batch
        [ Attributes.class "foo"
        , Events.onClick onClick
        ]


mixin2 : Bool -> Attribute msg
mixin2 p =
    if p
        then Attributes.none
        else Attributes.class "bar"
```

It will help you factor out reusable attributes of your views.

## Migrating from elm/html

All you need to do for migrating from elm/html is just replacing dependencies in your `elm.json` to `arowM/html`.
Then compiler would claim you to add "indirect" dependencies when trying to compile.

Let's see you have following `elm.json` file:

```elm
{
    ...
    "dependencies": {
        "elm/core": "1.0.0 <= v < 2.0.0",
        "elm/html": "1.0.0 <= v < 2.0.0",
        "elm/json": "1.1.3 <= v < 2.0.0"
    },
    ...
}
```

In this case, just replace "elm/html" with "arowM/html":

```elm
{
    ...
    "dependencies": {
        "elm/core": "1.0.0 <= v < 2.0.0",
        "arowM/html": "1.0.0 <= v < 2.0.0",
        "elm/json": "1.1.3 <= v < 2.0.0"
    },
}
```

The compiler would claim you to add some indirect dependencies.

```
{
    ...
    "indirect": {
        ...
        "arowM/elm-html-internal": "1.0.0",
        "elm/html": "1.0.0"
    }
    ...
}
```

It's all!

Make sure to remove `elm-stuff` directory before compiling to avoid build errors.

## Other things

The other things are same as `elm/html`.
So please see its README for details if you are not familiar with `elm/html`.
