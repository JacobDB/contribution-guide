# Sass

[Style Guide](style-guide.md) | [Resources](resources.md)

In this section, you'll learn how to organize and structure Sass, when and how to use mixins, variables, and functions, and much more.

## Quick Notes

### RSCSS

Projects should adhere to RSCSS guidelines. For full documentation, [view this repository](https://github.com/rstacruz/rscss). Note that some of the rules below differ slightly from the official documentation, so be sure to read through the below highlights.

**Components** are any predefined block that can stand on its own. Component names should be two lowercase words separated by a space. Some examples: `.article-card`, `.search-form`, and `.like-button`. Each component should be contained within it's own folder within the `components` folder.

**Elements** make up components. Element names should be one lowercase word. They should only appear within components, and should always be preceeded by a direct decedent selector. Some examples: `> .header`, `> .content`, and `> .footer`. Elements should be saved in the same file as the component they're a part of.

**Variants** modify components or elements. Variant names should be a dash followed by a single lowercase word. Some examples: `.article-card.-light`, `.search-form.-wide`, and `.like-button.-small`. Variants should be saved in the same file as the component they're modifying.

**Nested Components** are components within other components. If a sub component needs to appear differently when it's inside a specific component, this should be done with a variant, rather than applying styles specific to the sub component. Some examples: `.search-form.-small`, **not** `.header-block > .search-form`. In some cases, `@extend` can be used to simply nested component names, but this can create bloated compiled CSS, and should be used sparingly.

**Layouts** are blocks of components in specific contexts. For example, if three `.article-card` components need to appear in three columns, you would use a layout to do so. Layouts should be named like components (two lowercase words separated by a dash), but should be clearly labeled as a group of components in some way when possible. For the previous example, a name like `.article-grid` would work well, as the word `grid` indicates a group of items. Each layout should be contained in it's own folder within the `layouts` folder.

**Helpers** are global classes meant to override specific values. Their names should be as concise as possible, all lowercase, and preceeded by an underscore. All helper rules should end in `!important` to ensure they override styles as intended. These should be used very sparingly, as using too many `!important` rules can create all kinds of issues. All helpers should appear in the same file, located at `helpers/_helpers.scss`. The `helpers` folder also contains all mixins, variables, and functions.

**Base** is a special folder that contains basic global rules. This includes the grid system, user content styles (on basic elements, only within `.user-content`), basic content styles (never on elements themselves, always on classes), and Normalize rules. Some examples would be basic heading styles on a `.title` element, basic text styles on a `.text` element, styles for user entered content such as `.user-content p`, and other such things. This folder should be used sparingly, as global styles can cause many issues. With the exception of styles in `.user-content`, all styles within `base` should be as generic as possible so that they're globally applicable.

**Vendor** is a special folder that contains styles set up for vendor created components. These should never be modified during development, except when updating to a newer version of the vendor created component. Instead, styles to modify vendor components should be set up as new components, importing the vendor styles at the top of the document.

### Rule Structure

- Rules should be alphabetized.
- A single space should always appear between the last letter of a class and the opening curly bracket.
- Styles should never be applied to the top level component. Instead, they should be applied to an `&` rule that appears as the first rule in a component.
- Pseudo classes should appear directly after the main element styles, in alphabetical order (i.e. `:active`, then `:focus`, then `:hover`, and so on).
- Pseudo element styles should appear directly after their associated elements pseudo class styles, in structural order (i.e. `:before`, then `:after`).
- Pseudo classes that get applied to pseudo elements should appear directly after their associated pseudo elements, in alphabetical order (i.e. `:before:active`, then `:before:hover`).
- Variant classes should appear directly after pseudo elements. Again, variants should be in alphabetical order (i.e. `.-box`, then `.-margined`, then `.-opaque`).
- Pseudo classes for variants should appear directly after their associated variant, in structural order.
- Pseudo elements for variants should appear directly after their associated variants pseudo class styles, in alphabetical order.
- Pseudo classes that get applied to pseudo elements of a variant should appear directly after their associated variants pseudo elements, in alphabetical order.
- Elements should appear directly after all the styles for the component itself, in structural order. At this point, the cycle repeats.

```
.article-card {
    & {
        background: $background;
        box-shadow: remify(0 4 2, 16) transparentize($dark, 0.75);
        font-size: remify(16, 16);
        padding: remify(20, 16);
        transition: background 0.15s;
    }

    &:hover {
        background: $background_alt;
    }

    &.-dark {
        background: $dark;
    }

    &.-dark:hover {
        background: $dark_alt;
    }

    > .header {
        @extend .title;

        color: $accent;
        font-size: remify(20, 16);
        margin: remify(0 0 10, 16);
        text-transform: uppercase;
        transition: color 0.15s;
    }

    > .header:hover {
        color: $accent_alt;
    }

    > .header:before {
        content: "\25B6\0020";
    }

    > .header:hover:before {
        color: $primary;
    }

    > .header > .link {
        color: inherit;
        display: block;
    }

    ...
}
```

### Folder Structure

WIP

```
project-root
├── src
├── dev
└── dist
```
