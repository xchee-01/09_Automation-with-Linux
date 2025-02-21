# 19. Running R on Linux 

Running R in Linux provides a powerful combination for data analysis and scientific computing, particularly valuable in medical and bioinformatics research.

## 19.1. Installation of R on Linux

**(a) Installation of R base**

```
# Install R base
sudo apt install r-base r-base-dev

# Verify installation
R --version
```

**(b) Installing R studio (IDE)**

```
# Download RStudio
wget https://download1.rstudio.org/electron/jammy/amd64/rstudio-2024.12.1-563-amd64.deb

# Install
sudo dpkg -i rstudio-*.deb
sudo apt -f install
```

## 19.2. Command line interface

The command line interface is essential for running R scripts efficiently in Linux. 

```
# Start R interactive console
R

# Basic commands in R console
> x <- 1:10
> mean(x)
> quit()
```

Let's create an R script using `touch`

```
touch my_first_script.R
echo "x <- 1:10" > my_first_script.R
echo "mean(x)" >> my_first_script.R
echo "quit()" >> my_first_script.R
```

To run the R script, you would do the following:

```
# Run R script
Rscript my_first_script.R
```

## 19.3. Package management 

Package management in Linux-based R is crucial for maintaining dependencies and ensuring reproducibility.

You can install packages using the similar method as you would in R. 

```
# Install from CRAN
R
install.packages("ggplot2")
```

## 19.4. Running R script using bash script

The bash and R scripts work together to create a simple plot. 

The bash script prepares two lists of numbers (coordinates x and y) and sends them to R. The R script then receives these numbers, uses ggplot2 to create a graph with points and connecting lines, and saves it as a PNG file. 

This shows how two different programming languages can work together: bash handles the data preparation, while R specializes in creating the visualization.

First, create an R script as such. Let's call it "plot_sequences.R"

```
args <- commandArgs(trailingOnly=TRUE)
x <- as.numeric(strsplit(args[1], " ")[[1]])
y <- as.numeric(strsplit(args[2], " ")[[1]])

library(ggplot2)
ggplot(data.frame(x=x, y=y), aes(x=x, y=y)) + 
    geom_point() + 
    geom_line()

ggsave("plot.png")
```

Then create a bash script as such. 

```
#!/bin/bash

# Define arrays
x=(1 2 3 4 5 6 7 8 9 10)
y=(5 10 15 20 25 30 35 40 45 50)

# Pass arrays to R script
Rscript plot_sequences.R "${x[*]}" "${y[*]}"
```

> [!NOTE]
> `Rscript plot_sequences.R "${x[*]}" "${y[*]}"` refers to
>
> Each part means:
> 
> - `Rscript`: The command to run an R script from the command line
> - `plot_sequences.R`: The name of your R script file
> 
> For `"${x[*]}"`:
> - `x` is your array variable containing numbers 1-10
> - `[*]` means "all elements of the array"
> - `${ }` is for variable expansion in bash
> - The quotes " " keep all numbers together as one argument
> 
> So if you were to write it out fully, it's equivalent to:
>
> ```
> Rscript plot_sequences.R "1 2 3 4 5 6 7 8 9 10" "5 10 15 20 25 30 35 40 45 50"
> ```

You should be able to view the plot using the command `display`

Try the following

```
display plot.png
```

You might need to install the imagemagick package first using the following command if you cannot view anything

```
sudo apt install graphicsmagick-imagemagick-compat
```
