## Creating a function

So far you have created a dot-to-dot for a single image. What about other images?
Rather than repeating the whole process for every new image, you can create a function that does it for you.

--- collapse ---
---
title: Functions explained
---

TODO: text

--- /collapse ---

--- task ---

Create a function that creates a dot-to-dot for any starting image.
It should have the option to show or hide the solution with `True` or `False`.

--- hints ---

--- hint ---

Here's a template to start off your function:

```
dotToDot[image_, solution_] :=
With[
    {
        <list of points in image>
    },
    <list plot of points>
]
```

--- /hint ---

--- hint ---

The list of points can be computed as follows:

```
points = Part[ImageGraphics[image, 2, ImageSize -> 300], 1, 1]
```

--- /hint ---

--- hint ---

The list plot can be created as follows:

```
ListPlot[
    Table[
        Callout[
            Part[points, position],
            position
        ],
        {position, 1, Length[points], 1}
    ],
    Joined -> solution,
    AspectRatio -> 1,
    Axes -> False
]
```

--- /hint ---

--- /hints ---

--- /task ---

Now that you have a function, you can use it.

--- task ---

Apply your function to a new image.
Remember, your image should be fairly simple, with just one or two block colours.

Alternatively, evaluate the following code to get an example image.

```
CloudGet["https://www.wolframcloud.com/obj/RasPi/NumberThree"]
```

--- hints ---

--- hint ---

Here's an example in which the solution is not shown:

```
three = CloudGet["https://www.wolframcloud.com/obj/RasPi/NumberThree"];

dotToDot[three, False]
```

--- /hint ---

--- /hints ---