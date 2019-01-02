# Shovel

Are you sick of writing this:

``` python
def main(argv):
    file = argv[0]

    xs = []
    ys = []
    with open(file, 'rb') as csvfile:
        reader = csv.reader(csvfile)
        for row in reader:
            xs.append(row[1])
            ys.append(row[0])

    plt.plot(xs, ys, 'b-')
    plt.show()

if __name__ == '__main__':
    if(len(sys.argv) != 2):
        raise Exception("usage: filename")
    main(sys.argv[1::])
```

because you don't feel like recompiling gnuplot so you can just plot y against x
just so you can make sure your ETL didn't go horribly horribly wrong?

Congratulations! Shovel gives you a god-damn plot without having to leave the terminal.

Gnuplot I'm sorry. I would have learned you, but having pandas and all of python
*there* for me was too tempting.

Shovel is designed to make *getting a god-damn plot* of your data as easy as
possible. You can include shovel as a module for doing your input handling if
you want to go crazy with matplot lib.

The farthest I'm willing to go on this is supplying

## The Goods

``` sh
shovel-plot [options] filename
shovel-histo [options] filename
```

## Why Two Scripts?

Well, if you leave the plot type as an argument, you have to either confusingly
overload all of your options for each plot type, or have a situation where some
options are invalid based on other options. This is not what shovel is about.
Shovel is about give me a god-damn plot.

## Examples

### Line Plotting:
#### KISS:
``` sh
shvl-plt data.txt
```
#### Chose your qwn independent variable (defaults to the 0th field):
``` sh
shovel-plt --x-num=3 data.txt
```
#### ADVANCED -- Adding titles to your axes:
``` sh
shvl-plt --x-num=3 --legend=[0=vegans, 1=omnivores, 2=vegetarians, 3=time]
```
You can label as many fields or as few as you would like.
#### So you have a csv:
``` sh
shvl-plt data.txt
```
By default, Shovel will try to label your axes according to the csv header if
there is one.

### Histograms:
``` sh
shvl-hist data.txt
```
