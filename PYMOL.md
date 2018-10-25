# PyMOL
[*PyMOL Wiki*](https://pymolwiki.org/index.php/Main_Page)

## Selections

* `select selection-name, selection-algebra`
* i.e. `select modified, resname hem+glg+cyp`

## Alignment

* `align mobile, target`

## Color By Mutation

<img src="https://pymolwiki.org/images/0/06/Color_by_mutation.png" width="200">


* First, download the color-by-mutation script [here](https://pymolwiki.org/index.php/Color_By_Mutations) and place it in your current directory.
* In PyMOL, execute the following:
``` run color_by_mutation.py;
color_by_mutation protein1, protein2```