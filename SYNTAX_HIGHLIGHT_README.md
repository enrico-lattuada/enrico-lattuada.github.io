# Add a new syntax highlight theme

Go to the [Chroma playground](https://swapoff.org/chroma/playground/) website.
Test the themes.

If it does not exist, create the directory `assest/css/libs/chroma/`.
Create a new theme by running the command:

```bash
hugo gen chromastyles --style=<style-name> > <style-name>.css
```