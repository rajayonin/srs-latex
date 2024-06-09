# SRS-latex-uc3m
Support for software engineering tasks (SRS, autogeneration of traceability matrices, etc.) in LaTeX2e.  FYI, see `example.tex` and notes in `SRS.sty`.

If you have any question, please send an e-mail to `luisdaniel.casais [at] alumnos.uc3m.es`.



## Compilation
First you must install [LaTeX](https://www.latex-project.org/).

- For Linux, install `texlive-full`.
- For Windows, install [MiKTeX](https://miktex.org/download#win), make sure you add it to your `PATH`, and install [Perl](https://strawberryperl.com/). If it’s not installed already, open the MiKTeX Package Manager and install the `latexmk` package.
- For macOS, install [MacTeX](https://www.tug.org/mactex/mactex-download.html) and then install `latexmk` with:
    ```
    sudo tlmgr install latexmk
    ```

To compile the example, use the following command:
```
latexmk -pdflua example.tex
```


## VS Code
Some useful extensions:
- [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop)
    - If you are using the extension, please set `-shell-escape` (see [LaTeX Workshop FAQ](https://github.com/James-Yu/LaTeX-Workshop/wiki/FAQ#how-to-pass--shell-escape-to-latexmk))
- [LTeX](https://marketplace.visualstudio.com/items?itemName=valentjn.vscode-ltex): Grammar checker.
    - You can change the language through the `ltex.language` setting in VS Code settings.