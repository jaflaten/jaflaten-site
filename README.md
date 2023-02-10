## Guide

This guide covers the necessary bits. As the project evolves, it will only become more comprehensive

# Troubleshooting the site

If having issues with missing files and warnings for the theme or for instance if shortcodes can´t be found. Then this helped fix the issue. 

```
hugo mod clean
hugo server
```

Another suggestion for the shortcodes was to add /* and */ inside the {{shortcode }} brackets, but this broke the site and after cleaning it did not render shortcodes properly. Cleaning worked well. 

