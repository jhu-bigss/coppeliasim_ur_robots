# Read CSV/Txt file in Lua

You can insert the function below into your code to read a CSV or a Txt file.
```Lua
-- Convert a csv file to a Lua table.
-- @return table: Two-dimensional table with cell values.
function read_data(file, delimiter)
    delimiter = delimiter or ","

    -- Always ensures that the file is in its beginning position
    file = io.open(file)
    local data = {}
    local row = 1

    -- Loop through the lines in the file
    for current in file:lines() do
        -- Initialize table for this row
        data[row] = {}

        -- Used for adding individual columns of data
        local col = 1
        data[row][col] = ""

        -- Split on delimiter
        local i = 0
        while true do
            j = i + 1
            i = string.find(current, delimiter, i + 1)
            if i ~= nil then
                data[row][col] = string.sub(current, j, i - 1)
                col = col + 1
            else
                data[row][col] = string.sub(current, j, string.len(current))
                break
            end
        end
        row = row + 1
    end

    -- Clean up
    file:close()
    return data
end
```
To test it out in Windows:
```Lua
-- Read a csv file
array = read_data("C:/Users/your_username/Documents/data.csv")
print(array)
```
Or in Linux:
```Lua
array = read_data("/home/your_username/data.txt")
print(array)
```

## Reference
[https://gist.github.com/calebreister/8dd7ab503c91dea4dd2c499b9d004231](https://gist.github.com/calebreister/8dd7ab503c91dea4dd2c499b9d004231)