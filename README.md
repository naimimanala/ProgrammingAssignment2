
This script contains two functions that create a special "matrix" object capable of caching its inverse, and a function to compute the inverse while utilizing the cache to avoid repeated computations for the same matrix.


The first function creates a special "matrix" object that can cache its inverse.
It returns a list of four functions:
1. set: set the value of the matrix
2. get: get the value of the matrix
3. setinverse: set the value of the inverse
4. getinverse: get the cached inverse

    makeCacheMatrix <- function(x = matrix()) {
    inv <- NULL
    set <- function(y) {
        x <<- y          ## store new matrix
        inv <<- NULL     ## reset cached inverse
    }
    get <- function() x  ## return the matrix
    setinverse <- function(inverse) inv <<- inverse  ## store inverse
    getinverse <- function() inv  ## return cached inverse
    list(set = set, get = get,
         setinverse = setinverse,
         getinverse = getinverse)
}

This function computes the inverse of the special "matrix" returned by makeCacheMatrix.
If the inverse has already been calculated, it retrieves it from the cache instead of recomputing it.

    cacheSolve <- function(x, ...) {
    inv <- x$getinverse()
    if (!is.null(inv)) {
        message("getting cached data")
        return(inv)
    }
    data <- x$get()
    inv <- solve(data, ...)
    x$setinverse(inv)
    inv
}
