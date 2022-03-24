# Generic collection functions in Go

Some sample functions like Map, Filter, Any, All and Includes using 
the new generics support in Go 1.18. So, you'll need at least Go 1.18 for these to work.

### Map

Takes a slice and a function as arguments, calls the passed function on every value 
in the slice and returns a new slice containing the results.

```
func Map[T any, U any](xs []T, f func(T) U) []U {
	r := []U{}
	for _, x := range xs {
		r = append(r, f(x))
	}
	return r
}
```

### Filter

Returns a new slice containing all the values where the passed function returns true.

```
func Filter[T any](xs []T, f func(T) bool) []T {
	r := []T{}
	for _, x := range xs {
		if f(x) {
			r = append(r, x)
		}
	}
	return r
}
```

### Includes

Returns true if the target value is in the slice.

```
func Includes[T comparable](xs []T, t T) bool {
	for _, x := range xs {
		if x == t {
			return true
		}
	}
	return false
}
```

### Any

Returns true if at least one of the values satisfies the passed function.

````
func Any[T any](xs []T, f func(t T) bool) bool {
	for _, x := range xs {
		if f(x) {
			return true
		}
	}
	return false
}
````

### All

Returns true if at all of the values satisfies the passed function.

````
func All[T any](xs []T, f func(t T) bool) bool {
	for _, x := range xs {
		if !f(x) {
			return false
		}
	}
	return true
}
````
