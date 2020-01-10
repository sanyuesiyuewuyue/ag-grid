In v23 we are releasing a major rewrite of our themes with the goal of making it easier to write custom themes. There will be breaking changes for most custom themes. We want to explain why we are doing this, and let you know how to update your custom themes.

In previous versions of the grid, our philosophy was to provide Sass variables to allow the grid to be customised. The CSS classes on the DOM were considered an implementation detail to support the variables, not a public API for creating themes. However from our own experience writing themes and from user feedback, we knew that in practice the variables were not enough, and theme authors had to write CSS. This meant that most themes ended up relying on implementation details (DOM class names) to apply their styles. Sometimes the CSS required to achieve quite a simple effect was quite complex. And as a result of this complexity, CSS rules would often require updating for minor releases.

In v23.0 we have done a lot of work to make it easier to style the grid using plain CSS:

- We have added new class names to the DOM to make it easier to target specific elements. For example, overriding the colour of a child-level heading in the filter tool panel previously required the following CSS rule: `.ag-tool-panel-wrapper .ag-filter-panel .ag-group-component-container .ag-group-item { color: red }` and now the same effect can be achieved with: `.ag-filter-toolpanel-group-level-1-header { color: red }`.
- We have renamed classes and variables to make them consistent throughout the grid.
- We have rewritten and simplified our provided themes to take advantage of these new classes. Extending and customising provided themes will now be easier.
- Some variables were only really necessary because of the difficulty of using CSS selectors. These have been removed.
- In order to support the next major version of Sass, we have changed the way we handle renamed variables. Previously we automatically imported old variables. Now we will issue a warning when an old variable name is used to notify you to update it to the new name.



// TODO change this to use tables with old on left and new on right




## Placeholders removed

%tab - use .ag-tab
%selected-tab - use .ag-tab-selected
%card - use $ag-card-* variables or CSS selectors


## Sass variable changes

We have made various changes to Sass variables. When we have renamed variables, we still support the old variable names for compatibilty, but the changes are listed here for your information.

$ag-header-icon-size, $ag-row-border-width, $ag-transition-speed, $ag-cell-data-changed-color: These vars were defined but not used and have been removed.

$ag-foreground-opacity > $ag-foreground-color-opacity
$ag-alt-icon-color > $ag-checkbox-background-color

$ag-range-selection-background-color > $ag-selection-background-color
$ag-range-selection-border-color > $ag-selection-border-color
   
$ag-range-selected-color-1 (and -2, -3, -4): removed. Colour when multiple ranges overlap now calculated automatically from the opacity of $ag-selection-background-color.

$ag-foreground-color-opacity, $ag-secondary-foreground-color-opacity, $ag-disabled-foreground-color-opacity: removed. If you were using them, instead set a semi-transparent colour to $ag-foreground-color, $ag-secondary-foreground-color, or $ag-disabled-foreground-color

$ag-primary-color removed. Use $ag-selection-border-color and $ag-selected-tab-underline-color.

$ag-tooltip-background-color, $ag-tooltip-border-color, $ag-tooltip-border-radius, $ag-tooltip-border-style, $ag-tooltip-border-width, $ag-tooltip-foreground-color, $ag-tooltip-padding: removed. Use a CSS rule like .ag-tooltip { padding: 10px; }

$ag-accent-color > $ag-checkbox-checked-color

Variables starting `$ag-dialog-` and `$ag-dialog-title-` have been removed. Instead of using these variables, use a css selector like `.ag-panel { ... }` or `.ag-panel-title { ... }`. The full list of removed variables is: $ag-dialog-background-color, $ag-dialog-border-size, $ag-dialog-border-style, $ag-dialog-border-color, $ag-dialog-title-background-color, $ag-dialog-title-foreground-color, $ag-dialog-title-height, $ag-dialog-title-font-family, $ag-dialog-title-font-size, $ag-dialog-title-font-weight, $ag-dialog-title-padding, $ag-dialog-title-icon-size, 

$ag-header-background-image: removed. .ag-header {background: xxx}

$ag-row-stub-background-color: removed. use .ag-row-loading {background-color: xxx}

$ag-row-floating-background-color: removed. Use .ag-row-pinned {background-color: xxx}

$ag-group-border-color: removed

TODO: replaced with new styles, document
$ag-editor-background-color: null !default;
$ag-panel-background-color: null !default;
$ag-group-background-color: null !default;
$ag-group-border-color: null !default;
$ag-group-title-background-color: null !default;
$ag-group-toolbar-background-color: null !default;

## CSS class renames

ag-group-component
ag-group-component-title-bar
ag-group-component-title-bar-icon
ag-group-component-title
ag-group-component-container
ag-group-component-toolbar

.ag-row-stub > .ag-row-loading

Are now ag-group, ag-group-title-bar etc


.ag-alignment-stretch, .ag-alignment-start, .ag-alignment-end
are now
.ag-group-item-alignment-stretch, .ag-group-item-alignment-start, .ag-group-item-alignment-end

.ag-column-drag and .ag-row-drag are now .ag-drag-handle

.ag-nav-card-selector is now .ag-chart-settings-card-selector

.ag-nav-card-item is now .ag-chart-settings-card-item

ag-title-bar > ag-panel-title-bar
ag-title-bar-title > ag-panel-title-bar-title
ag-title-bar-buttons > ag-panel-title-bar-buttons
.ag-button > ag-panel-title-bar-button

.ag-paging-button > .ag-paging-button-wrapper

.ag-cell-with-height > .ag-cell-auto-height

.ag-name-value > ag-status-name-value


ag-parent-circle > ag-angle-select-parent-circle
ag-child-circle > ag-angle-select-child-circle

ag-picker-button > ag-picker-field-button

ag-fill > ag-spectrum-fill

ag-hue-alpha > ag-spectrum-tool


ag-tab-header > ag-tabs-header
ag-tab-body > ag-tabs-body


ag-chart-tabbed-menu > ag-chart-menu-tabs

ag-column-select-panel > ag-column-select
ag-primary-cols-header-panel > ag-column-select-header
ag-primary-cols-filter > ag-column-select-header-filter
ag-primary-cols-filter-wrapper > ag-column-select-header-filter-wrapper
ag-primary-cols-list-panel > ag-column-select-list


ag-filter-toolpanel-search
ag-filter-toolpanel-group
ag-filter-toolpanel-filter
ag-filter-toolpanel-filter-header
ag-filter-toolpanel-filter-body

Shared: 
ag-filter-toolpanel-header
ag-filter-toolpanel-header-expand
ag-filter-toolpanel-header-text


ag-filter-panel -> ag-filter-toolpanel
ag-filter-header > ag-filter-toolpanel-search-header
ag-filter-toolpanel-header > ag-filter-toolpanel-instance-header
ag-filter-panel-group-title -> ag-filter-toolpanel-group-title
ag-filter-panel-group-title-bar -> ag-filter-toolpanel-group-title-bar
ag-filter-panel-group-item -> ag-filter-toolpanel-group-item

ag-stub-cell > ag-loading


ag-paging-button-wrapper

ag-column-tool-panel-column > ag-column-select-column
ag-column-tool-panel-column-group > ag-column-select-column-group
ag-column-tool-panel-column-label > ag-column-select-column-label

.ag-toolpanel-indent-1 > .ag-column-select-indent-1
.ag-toolpanel-indent-2 > .ag-column-select-indent-2
.ag-toolpanel-indent-3 > .ag-column-select-indent-3
.ag-toolpanel-indent-4 > .ag-column-select-indent-4
.ag-toolpanel-indent-5 > .ag-column-select-indent-5

.ag-toolpanel-add-group-indent > .ag-column-select-add-group-indent

.ag-column-drop > .ag-column-drop-horizontal-half-width