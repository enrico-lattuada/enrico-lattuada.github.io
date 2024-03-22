# Create a custom font

To customize the font set:

1. Copy a font set such as minimal.toml to `data/fonts/my_font_set.toml` at the root of your site, creating the `data/fonts/` folders if they do not already exist. Note: avoid using spaces in filenames.
2. Adjust the font family, choosing from the library of [Google Fonts](https://fonts.google.com/) if you wish - refer to the Google Font guide below
3. Tell Wowchemy to use your new font set by setting `font: my_font_set` in `config/_default/params.yaml`

To select a free web-font available from Google Fonts:

1. Visit [Google Fonts](https://fonts.google.com/)
2. Click on each font you wish to use
3. For each font, click **+ Select this style** for each style you wish to use
4. Click on the icon at the top right (View your selected families) to open the dialog box on the right
5. Click on **Embed**
6. Under **<link>**, copy the part of the URL starting from `family=` to `&display=swap...` (not included) and paste it as the `google_fonts` option in your new font theme.
For example, if Google gives you `<link href="https://fonts.googleapis.com/css2?family=B612+Mono&family=Open+Sans&display=swap" rel="stylesheet">`, set `google_fonts = "family=B612+Mono&family=Open+Sans"`
1. Under **CSS rules to specify families** in Google Font’s dialog, copy the font name and paste it as one of the fonts in your font theme.
For example, given `font-family: 'B612 Mono', monospace;`, copy `B612 Mono`
