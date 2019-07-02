## Extracting points from an image

Find and name an image:

![A cartoon temple](images/myImageTemple.png)

Resize the image:

```
myImage = Rasterize[myImage, RasterSize -> 250];
```

Convert to a vector graphic:

```
ImageGraphics[myImage, 2, ImageSize -> 300]
```

Extract and name the points:

```
points = Part[ImageGraphics[myImage, 2, ImageSize -> 300], 1, 1]
```


## Plotting the points

Plot the points:

```
ListPlot[
    points,
    AspectRatio -> 1,
    Axes -> False,
    Joined -> joined
]
```

![First dot to dot](images/TemplePlot.png)


## Adding labels

Plot the points with labels:

```
ListPlot[
    Table[
        Callout[
            Part[points, position],
            position
        ],
        {position, 1, Length[points], 1}
    ],
    AspectRatio -> 1,
    Axes -> False,
    Joined -> joined
]
```


## Creating a function

Create a function that takes an image and creates a dot-to-dot, allowing the user to choose whether or not to show the solution.

```
dotToDot[image_, solution_] := 
With[
    {
        points = Part[ImageGraphics[image, 2, ImageSize -> 300], 1, 1]
    },
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
]
```


## Challenges

The starting image can be simplified with `Blur`, `Rasterize` or `Binarize`.


`Part[points, 1]` can be used to find the first point.
This point can be added to end of the list with `Join[points, {Part[points, 1]}]`.
This will join the last point in the plot to the first.


All of the labels can be made visible using `LabelVisibility -> All` in `Callout`.


`ArrayResample[points, <number>]` can be used to create a shorter list of points.
The number used should be smaller than `Length[points]`.


The points can be replaced, added or dropped in a variety of ways.
Here, we use `Part`, `ReplacePart`, `Insert`, `Join` and `Drop`.
For simplicity, each instance of `Part[expression, part]` has been replaced with the shorthand version, `expression[[part]]`:

```
(* Replace points: *)
points = ReplacePart[points, 125 -> points[[114]]];
points = ReplacePart[points, {114, 1} -> points[[1, 1]]];

(* Add points: *)
points = Insert[points, points[[1]], 114];
points = Insert[points, {points[[167, 1]], points[[178, 2]]}, 177];
points = Insert[points, points[[178]], 182];
points = Insert[points, {points[[2, 1]], points[[178, 2]]}, 183];
points = Join[points, {points[[13]]}];

(* Remove points: *)
points = Drop[points, {67, 110}];
points = Drop[points, {16, 62}];
```

Plot the points to verify it has worked:

![Cleaned up dot to dot](images/CleanedTemplePlot.png)
