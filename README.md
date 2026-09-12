Sitepackage for the project "Mountain Star Bootstrap Template"
==============================================================

TYPO3 sitepackage (extension key `mountain_star_bootstrap_template`) built on top of
[bk2k/bootstrap-package](https://github.com/benjaminkott/bootstrap_package). It ships the
project's TypoScript, page/content templates, backend layouts, RTE preset, logo/favicon and
the theme SCSS.

Requirements
------------

* TYPO3 v13 or v14
* EXT:bootstrap_package 13.x or 14.x (installed and activated first)

Manual installation (without Composer)
--------------------------------------

Use this if your TYPO3 instance is a legacy (non-Composer) installation.

1. **Install the dependency.** In the TYPO3 backend go to *Admin Tools > Extensions*, switch to
   *Get Extensions* and install **bootstrap_package** from the TER. Without it this sitepackage
   cannot be activated.

2. **Get the sitepackage files.** Either clone the repository or download it as a ZIP:

   ```bash
   git clone https://github.com/mtnstar/web-typo3-template.git mountain_star_bootstrap_template
   ```

3. **Copy it into the extension directory.** The folder name *must* match the extension key
   exactly, otherwise TYPO3 will not find the extension:

   ```
   <typo3-root>/public/typo3conf/ext/mountain_star_bootstrap_template/
   ```

   (On older installations without a `public/` directory, use `<typo3-root>/typo3conf/ext/`.)

   The directory has to contain `ext_emconf.php` at its top level — i.e. the path
   `.../ext/mountain_star_bootstrap_template/ext_emconf.php` must exist.

4. **Activate the extension.** Go to *Admin Tools > Extensions*, search for
   *Mountain Star Bootstrap Template* and activate it.

5. **Flush the caches** via *Admin Tools > Maintenance > Flush TYPO3 and PHP Cache*.

Installation with Composer
--------------------------

On a Composer based instance, install it from the repository instead:

```bash
composer config repositories.mountain-star-bootstrap-template vcs https://github.com/mtnstar/web-typo3-template.git
composer require mountain-star/mountain-star-bootstrap-template:dev-main
vendor/bin/typo3 extension:setup
```

Setting up the site
-------------------

1. Create (or open) the root page of your site and mark it as *Is root of website* in the
   page properties.

2. Add a **Template** record on that root page (*Site Management > TypoScript > Edit TypoScript
   Record* / *Create template for a new site*).

3. In the template record, tab *Includes*, add the static template
   **Mountain Star Bootstrap Template** to *Include static (from extensions)*. The
   bootstrap_package TypoScript is pulled in by this sitepackage automatically, so it does not
   need to be included separately.

4. Make sure a site configuration exists for the root page
   (*Site Management > Sites*).

5. Flush the frontend caches and open the site.

Backend layouts and page templates provided by the sitepackage (e.g. *Example*) are then
selectable in the page properties.

Building the frontend assets (optional)
---------------------------------------

The theme SCSS (`Resources/Public/Scss/Theme/theme.scss`) is compiled by bootstrap_package at
runtime, so no build step is needed for CSS. JavaScript and images are processed with Grunt:

```bash
cd Build
npm install
npx grunt build     # minifies JavaScript/Src/main.js to JavaScript/Dist/scripts.js and optimises images
npx grunt watch     # rebuilds the JavaScript on change
```
