# Markdown

## Beamer

### Header

        ---
        title:
        - Tutorial
        author:
        - José Villar
        date:
        - \today
        institute:
        - Universidad de Talca
        theme:
        - CambridgeUS
        colortheme:
        - beaver
        ---

### Body

- `\pause`: reveal parts of the frame one after the other.

### Conversion

- `pandoc -t beamer a.md -o b.pdf`

## Articles

### Header

        ---
        header-includes:
        - \usepackage[spanish]{babel}
        ---

### Conversion

- `pandoc -s -o a.pdf b.md`

### Fenced Code Blocks

The color scheme of code blocks can be selected using the `--highlight-style`
option. To see a list of highlight styles, type `pandoc
--list-highlight-styles`.

Example usage:

        pandoc test.md -o test.pdf --indented-code-classes=numberLines --toc
        --highlight-style=espresso

**Note**: You need to install `texlive-latexextra` for the above command to work

### Templates

To use a latex template, you can make changes to the default, which you can
find by using the following command:

        pandoc -D latex > template.tex

### Defaults

You can use a yaml file with default configurations by doing the following:

1. Create a file at ~/.local/share/pandoc/defaults/<fileName>
1. Use `pandoc <input> -o <output> defaults=<fileName>`

        !pandoc % -o test.pdf --defaults=article --template=template.te


### Citation of Figures

- Install `pandoc-fignos`
- Use `--filter pandoc-fignos`
- Note that any use of `--filter pandoc-citeproc` or `--bibliography=FILE`
  should come after the `pandoc-fignos` or `pandoc-xnos` filter calls.
