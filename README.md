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

#### Attempt 1: Check `renv::dependencies()`.

As suggested [here](https://rstudio.github.io/renv/articles/faq.html#why-isnt-my-package-being-snapshotted-into-the-lockfile) I should check `renv::dependencies()` to see whether usages of my package are reported in the output:

```r
> renv::dependencies()
Finding R package dependencies ... Done!
                                   Source Package Require Version   Dev
1 ~/renv-mess/renv.lock    renv                 FALSE
```

No `magrittr`.
So apparently, something is wrong with the installation.

### Packages are not installed properly.

So although `renv` is activated, no packages are installed inside:

```r
> renv::activate()
* Project '~/edu/renv-mess' loaded. [renv 0.16.0]
> install.packages("magrittr")
Installing magrittr [2.0.3] ...
	OK [linked cache]
```

When I run `utils::install.packages()` explicitly, the installation looks better:

```r
> utils::install.packages("magrittr")
Installing package into ‘/renv-mess/renv/library/R-4.2/x86_64-apple-darwin17.0’
(as ‘lib’ is unspecified)
trying URL 'https://cran.rstudio.com/bin/macosx/contrib/4.2/magrittr_2.0.3.tgz'
Content type 'application/x-gzip' length 227506 bytes (222 KB)
==================================================
downloaded 222 KB


The downloaded binary packages are in
	/var/folders/c9/0x656y4x5l1csbkyc_kzc8h80000gq/T//RtmphaDMRH/downloaded_packages
```

Still `renv::snapshot()` does not add `magrittr` as a new dependency.