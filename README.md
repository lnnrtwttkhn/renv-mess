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