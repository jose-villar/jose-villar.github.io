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
