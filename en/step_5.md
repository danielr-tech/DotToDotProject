## Creating a function

TODO: Arrive at the following result:

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