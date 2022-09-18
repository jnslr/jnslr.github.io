# Local setup instructions

## Prerequisites 

- Use WSL instead of windows crap (`bash` in powershell)
- Install latest ruby version and packages: `sudo apt-get install ruby ruby-dev build-essential dh-autoreconf`
- install node for Mermaid diagrams: `sudo apt-get install nodejs`
- Install jekyll: ``

## Serve locally

- `bundle install`
- `bundle exec jekyll serve --force_polling`

remote_theme: alshedivat/al-folio@v0.7.0