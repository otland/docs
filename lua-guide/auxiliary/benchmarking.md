# Benchmarking

With `os.clock`, you can compute (just about) the CPU time taken to execute a chunk of code.

```lua
local start = os.clock() -- save current CPU time

for i = 1, 100000 do
    -- do something
end

print('Time taken: '.. (os.clock() - start) ..' seconds.')
```

By saving the time before starting the code and subtracting the before from the time after it executes, you get an approximate amount of seconds taken to execute that chunk of code.

Here's a benchmarking function to help with determining the performance of code:

```lua
do
    local units = {
        ['seconds'] = 1,
        ['milliseconds'] = 1000,
        ['microseconds'] = 1000000,
        ['nanoseconds'] = 1000000000
    }

    function benchmark(unit, decPlaces, n, f, ...)
        local elapsed = 0
        local multiplier = units[unit]
        for i = 1, n do
            local now = os.clock()
            f(...)
            elapsed = elapsed + (os.clock() - now)
        end
        print(string.format('Benchmark results:\n  - %d function calls\n  - %.'.. decPlaces ..'f %s elapsed\n  - %.'.. decPlaces ..'f %s avg execution time.', n, elapsed * multiplier, unit, (elapsed / n) * multiplier, unit))
    end
end
```

* `unit`: Unit of time to show the result in ('seconds', 'milliseconds', 'microseconds', or 'nanoseconds')
* `decPlaces`: Number of decimal places to use when showing the elapsed time
* `n`: Number of times to run the function
* `f`: Function to run
* `...`: Arguments passed to function `f`

Example of using it from the previous page:

```lua
local stringLen = string.len
local tostring = tostring

function f()
	for i = 1, 10000 do
		stringLen(tostring(i))
	end
end

function f_2()
	for i = 1, 10000 do
		string.len(tostring(i))
	end
end

benchmark('milliseconds', 2, 50, f)
benchmark('milliseconds', 2, 50, f_2)
```

Output of the above:

```
Benchmark results:
  - 50 function calls
  - 868.86 milliseconds elapsed
  - 17.38 milliseconds avg execution time.
Benchmark results:
  - 50 function calls
  - 874.66 milliseconds elapsed
  - 17.49 milliseconds avg execution time.
```
