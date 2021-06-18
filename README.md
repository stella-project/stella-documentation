# STELLA's documentation

This repository contains the markdown files of [STELLA's documentation page](https://stella-project.org/stella-documentation/).

It is made with [mkdocs](https://github.com/mkdocs/mkdocs) and the [Material theme](https://github.com/squidfunk/mkdocs-material).

## How to contribute?

1. Clone repository
```
git clone https://github.com/stella-project/stella-documentation.git
``` 

2. Install requirements
```
pip install -r requirements.txt
```

3. Add new page and place it under `docs/`.
```
echo "New contents" >> docs/new-page.md
```

4. Deploy locally (`127.0.0.1:8000`) to review changes
```
mkdocs serve
```

5. Commit changes to this repository

6. Render and commit website files to the `gh-pages` branch
```
mkdocs gh-deploy
```

7. Updates should be avaible at [https://stella-project.org/stella-documentation/](https://stella-project.org/stella-documentation/)
