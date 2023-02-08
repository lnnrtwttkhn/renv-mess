# renv-mess

## History

### Adding new R Studio project

## Adding `renv`

### Test: Adding `test.R` with example code

Code in [`test.R`](test.R):

```r
mtcars %>%
  select(gear == 4)
```

Return the errror:

```r
Error in mtcars %>% select(gear == 4) : could not find function "%>%"
```

Fine, so we install `magrittr`:

```r
> install.packages("magrittr")
Installing magrittr [2.0.3] ...
	OK [linked cache]
```

Rerun `test.R`, same error:

```r
> mtcars %>%
+   select(gear == 4)
Error in mtcars %>% select(gear == 4) : could not find function "%>%"
```

## Issues

### Installed packages are not included in `renv::snapshot()`

I run `renv::snapshot()` to capture all installed packages in `renv.lock`.
So far, I have only installed `magrittr`.

```r
> renv::snapshot()
* Lockfile written to '~/renv-mess/renv.lock'.
```

Result: Nothing.
`renv.lock` is not updated.