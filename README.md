# Documentation Source Folder

This folder contains source files of **52Pi documentation**.

The sources do not render well in GitHub and some information is not visible at all.

Use actual documentation generated within about 1 minutes on each commit:

# Hosted Documentation

* English: https://docs.52pi.com

The above URLs are all for the master branch latest version.

## Extensions dependencies 

```bash 
sudo apt -y install mkdocs
```

* Python extensions

```python
sudo pip3 install pymdown-extensions --break-system-packages
sudo pip3 install mkdocs-video --break-system-packages
```

## Run Debug mode 
```bash
sudo mkdocs serve -a 0.0.0.0:80 
```
