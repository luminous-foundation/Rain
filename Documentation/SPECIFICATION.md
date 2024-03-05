# Rainbow Specification

## Type type

```csharp
type mytype = typeof(string);
mytype str = "Hello, World!";
```

## String Struct

```csharp
struct string
{
    private ref char raw { get; set; }
    int Length { get { return raw.Lengths } };
    
    string(ref char str) {
        this.raw = str;
    }
    
    static string this(ref char ptr)  {
        ref char newPtr = ref char[ptr.Length];
        
        for(int i = 0; i < ptr.Length; i++) {
            newPtr[i] = ptr[i];
        }
    }
}
```

## Inline Try Catch
Since error handling is forced, this is how you can handle it

```csharp
string HandleError(Exception ex)
{
    Console.WriteLine(ex.Message);
    return "Hi!";
}

void SomeFunction()
{
    string str = try ICanThrowAnError() catch (Exception ex) => HandleError(ex);
    str = try ICanThrowAnError() catch (Exception ex) => {
        Console.WriteLine(ex.Message);
    }
}
```

## Extension Methods
You can declare extension methods ANYWHERE!

```csharp
string x = "Hello, World!";
x.ResetSize(50);

void ResetSize(this string str, int size)
{
    str.raw = null ?? () => {
        return ref char[size];
    };
}    
```

## Default Constructor

```csharp
class MyClass
{
    int x { get; set; }
    int y { get; set; }
    int z { get; set; }
    
    MyClass(default);
    
    /* Turns into:
    MyClass(int x, int y, int z)
    {
        this.x = x;
        this.y = y;
        this.z = z;
    }
    */
}
```