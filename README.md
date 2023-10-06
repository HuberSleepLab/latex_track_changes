# Rationale
LaTeX is beautiful, yet exporting a PDF file including track changes is painful. This repository explains how to export a PDF file with track changes with LaTeX.
Latex's way of introducing track changes into a PDF is to use a function inside the text that indicates which lines of text were removed in favor for other text. Packages such as `\usepackage{changes}` provide functions which can be used as follows:

```
\documentclass{article}
\usepackage{changes}

\begin{document}
  This is \deleted{the best} \added{some example} text.
\end{document}
```

<img width="1658" alt="example_diff" src="https://user-images.githubusercontent.com/32299254/204502891-5c08157d-f127-46e2-b47e-63f2bfb83aef.png">

While we could, theoratically, insert all revisions using these functions, this is ridiculously effortful. Instead, we want LaTeX to compare two .tex files and create a new .tex file in which LaTeX, for us, inserts the functions wherever the two compared files differ (both where text was deleted and where text was added).

# Steps
1) Install perl
2) Install MikTeX
3) Install `latexpand` and `latexdiff` package
4) Download source .tex file (e.g., from overleaf) with and without revisions.
5) Merge hierarchical .tex files using `latexpand` (only necessary when main.tex files impots other .tex files, which is highly recommended).
7) Compare merged files using `latexdiff`.
8) Upload the created .tex file to overleaf to compile a PDF file with track changes.
9) Enjoy the PDF file with track changes.

## Install Perl
Following [this tutorial](https://www.overleaf.com/learn/latex/Articles/Using_Latexdiff_For_Marking_Changes_To_Tex_Documents), the LaTeX scripts we will use later require the installation of perl. Install it [from here](https://www.perl.org/get.html). Make sure you use the strawberry installation when on windows.

## Install MikTeX
Install MikTeX [from here](https://miktex.org/download).

## Install latexpand and latexdiff package
Once MikTeX is installed, open the `MikTeX console`, navigate to `packages` and look for the packages `latexpand` and `latexdiff`. Install them.

<img width="791" alt="miktex_console" src="https://user-images.githubusercontent.com/32299254/204505862-345c17b4-d309-4b7a-9947-2a4ed30743b4.png">

## Download source. tex files
When you work in Overleaf, download the source file of the two versions that you want to compare. While overleaf offers [the option](https://www.overleaf.com/learn/how-to/Track_Changes_in_Overleaf) to insert track changes, to date, it does not provide an option to export a PDF that includes track changes. In Overleaf, navigate to `Menu` > `Source`. This will download the source file. Unzip the source file. Do this for both the version with and without the revisions. You can open an earlier version of your document by navigating to `History`. If you labelled the earlier version, open the labeled earlier version. Otherwise browse through the history. 

I personally liked it best to push the version without ad with track changed to github. For that, navigate to `Menu` > `GitHub` and commit + push the version without and with track changes to GitHub. Then clone the repository. Using `github desktop`, you can easily switch between commits, that is, the two versions of your file. Copy both versions to a seperate folder.

## Merge hierarchical .tex files using `latexpand`
To date, `latexdiff` cannot handle .tex files that import other .tex files. This is why we first need to build one big .tex file in which the text of all imported files is simply copied. Instead of doing that manually (we want to avoid human errors), we let `latexpand` do this for us. In the MiKTeX console, open the `command window` (the black screen on the left). In the command window, navigate the current folder to the folder in which the .tex source file without track changes lies, by using `cd C:\path\to\your\source\files`. Then type `latexpand main.tex > without_tc.tex`. 

<img width="583" alt="folder" src="https://user-images.githubusercontent.com/32299254/204512760-1bdaa2d3-a00e-4a5c-b4cb-71eaafbb739f.png">


Then change the current directory to the folder with the .tex source file with track changes. Type `latexpand main.tex > with_tc.tex`. This will create two new merged .tex files. Copy them into a new folder.

<img width="587" alt="folder2" src="https://user-images.githubusercontent.com/32299254/204513005-8d68d8c9-c0d7-480e-bdb6-dd3f8b00bf3d.png">


## Copmare .tex file using `latexdiff`
In the `command window`, change the current directory to the folder in which the merged .tex file lie. Then type `latexdiff without_tc.tex with_tc.tex > track_changes.tex`. This will create a new .tex file in which all differences betwen `without_tc.tex` and `with_tc.tex` are marked with function calls.

<img width="584" alt="folder3" src="https://user-images.githubusercontent.com/32299254/204513289-db05c79b-2a84-41b8-9ecd-b30061fdf562.png">

## Upload .tex file to overleaf
Upload `track_changes.tex` to into your original project in overleaf and compile the .tex file. First change the main file in overleaf by navigating to `menu` > `main_document` > `track_changes.tex`. Then compile the file.

## Download the PDF file
Enjoy your PDF file with track changes

<img width="1051" alt="example_output" src="https://user-images.githubusercontent.com/32299254/204511494-303c57c2-d4e4-4844-ae19-1454378962bf.png">



