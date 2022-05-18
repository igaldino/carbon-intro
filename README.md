# Carbon for IBM.com Intro

## Overview

This is a fast hands-on introduction to Carbon for IBM.com standard by a developer point of view.

### Myself

Isaque Galdino - Developer - CIO - eDelivery - Web UI squad.

### Carbon for IBM.com

Carbon for IBM.com is built with Carbon at its foundation, with additional components and styling optimized for a more editorial approach that allows users to scan, read, and navigate multiple pages with comfort and ease. Our goals are to provide visual consistency and the highest quality for all IBM.com website pages.

### Carbon

Carbon is IBM’s open source design system for products and digital experiences. With the IBM Design Language as its foundation, the system consists of working code, design tools and resources, human interface guidelines, and a vibrant community of contributors.

### Frameworks
Carbon for IBM.com: React, Web Components and CSS/Vanilla.

Carbon: React, Angular, Vue, Svelte, Web Components and CSS/Vanilla.

## Node.js

Install Node.js 14.

### Windows
Download from the website.

### Fedora
```
sudo dnf module install nodejs:14
```

## Angular

Current Carbon for IBM.com for Web Components version (1.18.0) depends on TypeScript 4.3.5, which was deprecated in Angular 13, so it was suppose to work with Angular 12.

However, Carbon for Web Components uses TypeScript 3.9.1.

I was unable to make it work with Angular 10+, so, Angular 9 it is.

### Local
It will install in your current directory
```
npm install @angular/cli@9
echo 'export PATH=${PWD}/node_modules/.bin:${PATH}' > env.sh
chmod +x env.sh
. env.sh
ng version
```

### Global
```
npm install -g @angular/cli@9
ng version
```

## Project setup

### Creation
```
ng new --routing --style=scss --skip-tests tutorial20220518
```

### Carbon for IBM.com
```
cd tutorial20220518
npm install -S @carbon/ibmdotcom-web-components
```

### Web components support

Open `src/app/app.module.ts` and import `CUSTOM_ELEMENTS_SCHEMA` from `@angular/core`:
```
import { CUSTOM_ELEMENTS_SCHEMA, NgModule } from '@angular/core';
```

also, define the `schemas` property in `@NgModule`:
```
  schemas: [
    CUSTOM_ELEMENTS_SCHEMA
  ],
```

### Fake process.env support

Carbon for IBM.com references to the process.env global variable, so we need to fake it. Open `src/polyfills.ts` and add:
```
(window as any).process = {
  env: { DEBUG: undefined },
};
```

### Fix style support

Open `angular.json` and add:
```
"stylePreprocessorOptions": {
  "includePaths": [
    "node_modules"
  ]
}
```
to projects.tutorial20220518.architect.build.options property.

Then open `src/styles.scss` and add:
```
$feature-flags: (
  enable-css-custom-properties: true,
  grid-columns-16: true
);

@import 'carbon-components/scss/globals/scss/styles.scss';
```

### Start it up
```
ng serve
```

Open your browser at `http://localhost:4200`

## Page

### Change title
Open `src/index.html` and change `<title>` tag `Carbon for IBM.com Intro`.

Open `src/app/app.components.ts` and change `title` variable to `'Carbon for IBM.com Intro'`.

### Shell

[Dotcom shell story book](https://www.ibm.com/standards/carbon/web-components/?path=/story/components-dotcom-shell--default)

Open `src/app/app.components.ts` and add:
```
import '@carbon/ibmdotcom-web-components/es/components/dotcom-shell/index';
```

Open `src/app/app.components.html`, remove everything and add:
```
<dds-dotcom-shell-container>
  <main>
    content
  </main>
</dds-dotcom-shell-container>
```

### Micro footer

Open `src/app/app.components.html` and add `footer-size="micro"` attribute to `dds-dotcom-shell-container` tag.

How to know the values for `footer-size` attribute?

### Grid

[Carbon 2x Grid](https://carbondesignsystem.com/guidelines/2x-grid/overview/)

Open `src/app/app.components.html` and replace `content` by:
```
    <div class="bx--grid">
      <div class="bx--row">
        <div class="bx--col">
          content
        </div> <!-- col -->
      </div> <!-- row -->
    </div> <!-- grid -->
```

### Table of contents

[Table of contents story book](https://www.ibm.com/standards/carbon/web-components/?path=/story/components-table-of-contents--default)


Open `src/app/app.components.ts` and add:
```
import '@carbon/ibmdotcom-web-components/es/components/table-of-contents/index';
```

Open `src/app/app.components.scss` and add:
```
@import '@carbon/ibmdotcom-styles/scss/globals/vars';
@import '@carbon/ibmdotcom-styles/scss/components/tableofcontents/tableofcontents';

body {
  scroll-behaviour: smooth;
  overflow-y: scroll;
}

h3 {
  margin-top: 1rem;
  margin-bottom: 0.5rem;
}

.bx--tableofcontents__contents {
  margin-bottom: 2rem;
}
```

Open `src/app/app.components.html` and add:
```
    <dds-table-of-contents>
      <div class="bx--tableofcontents__contents">
        <a name="toc-carbon-for-ibm-dot-com" data-title="Carbon for IBM.com"></a>
        <h3>Carbon for IBM.com</h3>
        <p>Carbon for IBM.com is built with Carbon at its foundation, with additional components and styling optimized for a more editorial approach that allows users to scan, read, and navigate multiple pages with comfort and ease. Our goals are to provide visual consistency and the highest quality for all IBM.com website pages.</p>

        <a name="toc-carbon" data-title="Carbon"></a>
        <h3>Carbon</h3>
        <p>Carbon is IBM’s open source design system for products and digital experiences.</p>
        <p>With the IBM Design Language as its foundation, the system consists of working code, design tools and resources, human interface guidelines, and a vibrant community of contributors.</p>

        <a name="toc-frameworks" data-title="Frameworks"></a>
        <h3>Frameworks</h3>
        <p>Carbon for IBM.com: React, Web Components and CSS/Vanilla</p>
        <p>Carbon: React, Angular, Vue, Svelte, Web Components and CSS/Vanilla</p>

        <a name="toc-angular" data-title="Angular"></a>
        <h3>Angular</h3>
        <p>Angular is a framework and platform that is written in TypeScript.  It is used for developing single page applications employing TypeScript and HTML template language.</p>

        <a name="toc-carbon-for-angular" data-title="Carbon for Angular"></a>
        <h3>Carbon for Angular</h3>
        <p>Just use Carbon for Angular components if you won’t use Carbon for IBM.com Web components.</p>
        <p>Mixing both may cause some issues, specially with scss conflicts and long compilation time.</p>

        <a name="toc-carbon-for-web-components" data-title="Carbon for Web Components"></a>
        <h3>Carbon for Web Components</h3>
        <p>There is no Carbon for IBM.com Angular components.</p>
        <p>The Carbon for IBM.com team is focusing in Web Components even as a base for the Rect implementation.</p>
      </div>
    </dds-table-of-contents>
```

In order to unleash the full potential of this component, return the shell to its regular size. Remove `footer-size="micro"` attribute from `dds-dotcom-shell-container` install.

### Lead space block

[Lead space block story book](https://www.ibm.com/standards/carbon/web-components/?path=/story/components-lead-space-block--default)

Open `src/app/app.components.ts` and add:
```
import '@carbon/ibmdotcom-web-components/es/components/leadspace-block/index';
```

Open `src/app/app.components.html` and add:

```
        <dds-leadspace-block>
          <dds-leadspace-block-heading>Carbon for IBM.com Intro</dds-leadspace-block-heading>
        </dds-leadspace-block>
```

Check other lead space options.

### Content group simple

[Content group simple story book](https://www.ibm.com/standards/carbon/web-components/?path=/story/components-content-group-simple--default)

Open `src/app/app.components.ts` and add:
```
import '@carbon/ibmdotcom-web-components/es/components/content-group-simple/index';
```

Open `src/app/app.components.html` and change the first `h3` by `dds-content-group-heading` and `p` by `dds-content-group-copy` tags.

Then, change `h3` by `dds-content-item-heading` and `p` by `dds-content-item-copy` tags.

Wrap every `dds-content-item-heading` and `dds-content-item-copy` set inside a `dds-content-item` tag.

Using regex, replace `</dds-content-item-copy>$\n.*<dds-content-item-copy>` by `</p>\n<p>` and fix the paragraphs.

And finally, wrap it all inside a `dds-content-group-simple` tag.

## Forms

What about them?

Use [Carbon forms](https://carbondesignsystem.com/patterns/forms-pattern/).

## Links

* Carbon for IBM.com - [web site](https://www.ibm.com/standards/web/carbon-for-ibm-dotcom/), [GitHub](https://github.com/carbon-design-system/carbon-for-ibm-dotcom)
* Carbon for IBM.com Web Components - [GitHub](https://github.com/carbon-design-system/carbon-for-ibm-dotcom/tree/master/packages/web-components), [storybooks](https://www.ibm.com/standards/carbon/web-components/?path=/docs/overview-getting-started--page)
* [Carbon Design System](https://www.carbondesignsystem.com/)
* [Angular](https://angular.io/)
* [How to use Web Components in Angular](https://vaadin.com/learn/tutorials/using-web-components-in-angular)
* Node.js - [web site](https://nodejs.org/en/), [releases](https://nodejs.org/en/download/releases/)
* [Application](http://localhost:4200)
