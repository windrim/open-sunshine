# OpenSunshine Data and Methods

This repo contains the raw data and corresponding methodology behind the [OpenSunshine project](https://www.opensunshine.herokuapp.com). It is meant to illustrate how I processed the data for publication. The `data` directory and `Methodology.ipynb` provides a step-by-step reproducible methodology to transform the source files from the government into the final dataset used on the project page. 

If you want to search through and download the data, or any section thereof, the website is a better venue. 

# How to deploy a similar app

The basic deployment with Datasette follows [this](https://www.youtube.com/watch?v=7kDFBnXaw-c) essential tutorial by the app's creator, Simon Willison. It requires some source data, in my case a CSV.

1. CSV --> SQLite with `sqlite-utils`
    - `sqlite-insert main.db main main.csv --csv`
      - `main.db` is output filename
      - `main` is name of table within DB 
      - `main.csv --csv` is input file with CSV flag  
2. Deploy Datasette app for testing
    - `datasette main.db` will host the app locally
    - `datasette install <plugin>` will add useful plugins for built-in viz, data downloads, APIs etc
    - `datasette main.db --template-dir=templates/` lets you customize the frontend as described in these [docs](https://docs.datasette.io/en/stable/custom_templates.html)
      - This is how I added the custom homepage
3. Publishing online
    - I published to [Heroku](https://www.heroku.com/) with this command:
      - `datasette publish heroku main.db -n opensunshine --install <plugin1> --install <plugin2> ... --templates-dir=templates/`
      - This requires the heroku CLI tool on your computer, with a corresponding Heroku account
