---
---

# c# array

## single dimension array

In C#, an array is a structure that stores a fixed-size sequential collection of elements of the same type. You can think of it as a container that holds a specific number of "slots" for data, like a row of lockers.

Starts at 0, ends at Length - 1.

## Fixed Size (Empty): Use this when you know how many items you need but don't have the data yet.
```csharp
int[] numbers = new int[5]; // Creates an array with 5 slots, all initialized to 0.
```
## With Initial Values: Use curly braces {} to set values immediately.

```csharp
string[] fruits = { "Apple", "Banana", "Orange" };
```

## Multidimensional Arrays

A multidimensional array is basically an array of arrays.

To create a 2D array, add each array within its own set of curly braces, and insert a comma (,) inside the square brackets:

```chsarp
int[,] numbers = { {1, 4, 2}, {3, 6, 8} };
```

in the above example, the row 0 will contain 1,4,2 and the column 0 will contain 1 and 3.

|   | COLUMN 0 | COLUMN 1 | COLUMN 2 |
| :-: | :-: | :-: | :-: |
| ROW 0 | 1 | 4 | 2 |
| ROW 1 | 3 | 6 | 8 |

Access Elements of a 2D Array

To access an element of a two-dimensional array, you must specify two indexes: one for the array, and one for the element inside that array. Or better yet, with the table visualization in mind; one for the row and one for the column (see example below).

```csharp
int[,] numbers = { {1, 4, 2}, {3, 6, 8} };
Console.WriteLine(numbers[0, 2]);  // Outputs 2
```

## jagged array

A jagged array in C# is an "array of arrays." Unlike a traditional multidimensional (rectangular) array where every row has the same number of columns, a jagged array allows each "row" to be its own independent array with its own length.

```csharp
// Step 1: Declare the outer array with 3 rows
int[][] jaggedArray = new int[3][];

// Step 2: Initialize each row with different sizes
jaggedArray[0] = new int[5];    // Row 0 has 5 columns
jaggedArray[1] = new int[2];    // Row 1 has 2 columns
jaggedArray[2] = new int[3];    // Row 2 has 3 columns

// Step 3: Assign a value
jaggedArray[0][4] = 99;
```

## Go game

int length = 9;

```csharp
// 9x9 grid (81 cells total) that can hold integers.
int length = 9;
int[,] grid = new int[length, length];  // Creates 9x9 = 81 cells, all initialized to 0
```

Convert 2D array to JSON-friendly format

why used a jagged array?

because it is easier to read, hence to debug and analayze

jagged array output 

```csharp
{
  "grid": [
    [0, 1, 2, 0, 1, 2, 0, 1, 2],
    [2, 0, 1, 2, 0, 1, 2, 0, 1],
    // ... 7 more rows
  ]
}
```

array output
```csharp
{
  "size": 9,
  "grid": [0,1,2,0,1,2,0,1,2,2,0,1,2,0,1,2,0,1,...]
}
```

First, convert your int[,] to int[][] (jagged array):
```csharp
// Convert to jagged array for JSON
int[][] jaggedGrid = new int[length][];
for (int i = 0; i < length; i++)
{
    jaggedGrid[i] = new int[length];
    for (int j = 0; j < length; j++)
    {
        jaggedGrid[i][j] = grid[i, j];
    }
}
```

save to json
```csharp
using System.Text.Json;

// Wrap in object for better structure
var data = new { grid = jaggedGrid };

string json = JsonSerializer.Serialize(data, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText("grid.json", json);
```
Load back from JSON

```csharp
string json = File.ReadAllText("grid.json");
var data = JsonSerializer.Deserialize<dynamic>(json);
int[][] jaggedGrid = data.grid.ToObject<int[][]>();

// Convert back to 2D array if needed
int[,] grid = new int[length, length];
for (int i = 0; i < length; i++)
{
    for (int j = 0; j < length; j++)
    {
        grid[i, j] = jaggedGrid[i][j];
    }
}
```
XAML (GridCanvas.xaml)

```
<UserControl x:Class="YourApp.GridCanvas"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
    <Canvas x:Name="GridCanvas" 
            Background="Gray"
            MouseDown="OnCellClick">
    </Canvas>
</UserControl>
```
Code-behind (GridCanvas.xaml.cs)
```
public partial class GridCanvas : UserControl
{
    private readonly int[,] _grid;
    private readonly int _cellSize;
    private readonly Canvas _canvas;

    public GridCanvas(int[,] grid)
    {
        InitializeComponent();
        _grid = grid;
        int length = grid.GetLength(0);
        _cellSize = 40;  // Pixels per cell
        _canvas = GridCanvas;  // WPF-generated name
        
        Width = length * _cellSize;
        Height = length * _cellSize;
        RenderGrid();
    }

    private void RenderGrid()
    {
        int length = _grid.GetLength(0);
        _canvas.Children.Clear();

        for (int row = 0; row < length; row++)
        {
            for (int col = 0; col < length; col++)
            {
                Rectangle rect = new Rectangle
                {
                    Width = _cellSize,
                    Height = _cellSize,
                    Stroke = Brushes.Black,
                    StrokeThickness = 1
                };

                // Color based on grid value
                rect.Fill = _grid[row, col] switch
                {
                    1 => Brushes.Black,
                    2 => Brushes.White,
                    _ => Brushes.Transparent
                };

                Canvas.SetLeft(rect, col * _cellSize);
                Canvas.SetTop(rect, row * _cellSize);
                _canvas.Children.Add(rect);
            }
        }
    }

    private void OnCellClick(object sender, MouseButtonEventArgs e)
    {
        Point pos = e.GetPosition(_canvas);
        int col = (int)(pos.X / _cellSize);
        int row = (int)(pos.Y / _cellSize);

        // Return/raise event with position
        Clicked?.Invoke(this, (row, col));
    }

    public event Action<object, (int row, int col)> Clicked;
}
```
Usage
```
int length = 9;
int[,] grid = new int[length, length];
// ... fill your grid

GridCanvas canvas = new GridCanvas(grid);
canvas.Clicked += (sender, pos) => 
{
    Console.WriteLine($"Clicked row {pos.row}, col {pos.col}");
};
myWindow.Content = canvas;
```

