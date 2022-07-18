
| Environment| Link |
| ------ | ------ |
| Testing| https://test-wiki.apps.cmich.edu/|
| Production | https://wiki.apps.cmich.edu/|

-----

### CSS for Bookstack

<details><summary>Expand for CSS</summary>


```
 <style>:root {
    --color-secondary: #ffc82e;
}

::-moz-selection {
    color: #FFF;
    background: var(--color-primary);
}

::selection {
    color: #FFF;
    background: var(--color-primary);
}

html.dark-mode * {

    outline-color: var(--color-secondary);

}

html.dark-mode .activity-list a,
html.dark-mode a.card-footer-link {
    color: var(--color-secondary);
}



html.dark-mode header {
    filter: unset;
}

html.dark-mode .dropdown-menu a,
html.dark-mode .dropdown-menu button {
    color: #eee !important;
}


html.dark-mode .dropdown-menu a:hover,
html.dark-mode .dropdown-menu a:focus,
html.dark-mode .dropdown-menu button:hover,
html.dark-mode .dropdown-menu button:focus {

    background-color: rgba(255, 255, 255, .05) !important;

}


html:not(.dark-mode) .page-content a {
    text-decoration: underline;
}

html:not(.dark-mode) .page-content a:hover {
    text-decoration: none;
}

html.dark-mode .content-wrap a {
    color: var(--color-secondary);
}

html.dark-mode .card a {
    color: var(--color-secondary);
}

html.dark-mode div[toolbox-tab-content=tags] a {
    color: var(--color-secondary);
}

html.dark-mode .floating-toolbox.open .tabs>button.active {
    background-color: rgba(255, 255, 255, 0.9);
    color: #000;
}

html.dark-mode .floating-toolbox.open .nav-tabs button.selected.tab-item {
    color: #FFF;
    border-bottom-color: var(--color-secondary);
}

html.dark-mode .nav-tabs a.selected,
html.dark-mode .nav-tabs .tab-item.selected {
    border-bottom: 2px solid var(--color-secondary);
}

html.dark-mode .text-primary {
    color: var(--color-secondary) !important;
}

html.dark-mode {
    background-color: #292929;
}

html.dark-mode .icon-list-item:not(.no-hover):hover {
    filter: grayscale(1) brightness(1.1);
}

html.dark-mode .entity-list-item:not(.no-hover):hover,
html.dark-mode .icon-list-item:not(.no-hover):hover {

    background-color: rgba(255, 255, 255, .05);

}

html.dark-mode .breadcrumbs a.icon-list-item.text-book {
    color: var(--color-book);
    fill: var(--color-book);
}

html.dark-mode .breadcrumbs a.icon-list-item.text-chapter {
    color: var(--color-chapter);
    fill: var(--color-chapter);
}

html.dark-mode .breadcrumbs a.icon-list-item.text-page {
    color: var(--color-page);
    fill: var(--color-page);
}

.breadcrumbs,
.tri-layout-left-contents>*,
.tri-layout-right-contents>* {
    opacity: 1;
}

html.dark-mode .tri-layout-left-contents>*,
html.dark-mode .tri-layout-right-contents>* {
    opacity: 1.0 !important;
}




html.dark-mode .toggle-switch .custom-checkbox {
    color: var(--color-secondary) !important;
    fill: var(--color-secondary) !important;
}


.code-base,
span.code,
code {
    border: none;
    background-color: rgba(106, 0, 50, 0.1);
    padding: 4px 5px;
    color: var(--color-primary);
}

html.dark-mode .code-base,
html.dark-mode span.code,
html.dark-mode code {
    background-color: rgba(255, 200, 46, 0.10);
    color: var(--color-secondary);
    filter: grayscale(0.5);
}



html.dark-mode .sidebar-page-nav .sidebar-page-nav-bullet.primary-background {
    background-color: var(--color-secondary) !important;
}

html.dark-mode .sidebar-page-nav .page-nav-item a {
    color: var(--color-secondary);
}

html.dark-mode blockquote {
    border-left: 4px solid var(--color-secondary);
}


blockquote {

    border-left: 4px solid var(--color-secondary);

}

blockquote::before {
    display: none;
}


html.dark-mode .tri-layout-right-contents .actions a {
    color: var(--color-secondary);
}

/* FORM STYLES */

html.dark-mode .input-base:focus,
html.dark-mode input[type=text]:focus,
html.dark-mode input[type=number]:focus,
html.dark-mode input[type=email]:focus,
html.dark-mode input[type=date]:focus,
html.dark-mode input[type=search]:focus,
html.dark-mode input[type=url]:focus,
html.dark-mode input[type=color]:focus,
html.dark-mode input[type=password]:focus,
html.dark-mode select:focus,
html.dark-mode textarea:focus,
html.dark-mode .fake-input:focus {
    border-color: var(--color-secondary);
    outline: 1px solid var(--color-secondary);
}

html.dark-mode .text-neg,
html.dark-mode .text-neg:hover,
html.dark-mode .text-neg-hover:hover {
    color: #f44336 !important;
    fill: #f44336 !important;
}

.tri-layout-right-contents .actions .icon-list>a[href*="delete"] {
    color: #CC0000;
    fill: #CC0000;

}


html.dark-mode .tri-layout-right-contents .actions .icon-list>a[href*="delete"] {
    color: #f44336;
    fill: #f44336;

}

html.dark-mode .contained-search-box input,
html.dark-mode .contained-search-box button {

    color: #EEE;
}

html.dark-mode .dropzone-container {
    background-color: #222;
    background: rgba(0, 0, 0, 0.25);
    border: 1px solid #444;
    box-shadow: inset 0 3px 6px rgb(0 0 0 / 55%);
}

html.dark-mode .form-group[collapsible] {

    border-color: rgba(255, 255, 255, 0.15);

}

html.dark-mode .card.drag-card .handle:hover,
html.dark-mode .card.drag-card .drag-card-action:hover {
    background-color: rgba(255, 255, 255, .05);
}

html.dark-mode [back-to-top] {
    background-color: var(--color-secondary) !important;
    color: var(--color-primary);
}

html.dark-mode [back-to-top]:hover {
    filter: grayscale(1) brightness(1.1);
}

[back-to-top] {
    opacity: 1.0 !important;
}

.fade-in-when-active {
    opacity: 1.0;

}

html.dark-mode .button:not(.outline) {
    filter: unset;
    background-color: var(--color-secondary);
    color: var(--color-primary);
    border-color: var(--color-primary);
}

html.dark-mode .button:not(.outline):hover,
html.dark-mode .button:not(.outline):focus,
html.dark-mode .button:not(.outline):active {
    filter: grayscale(1) brightness(1.1);

}

html.dark-mode button.primary-background {
    background-color: var(--color-secondary) !important;
    color: #333 !important;
}

html.dark-mode button.primary-background:hover {
    filter: grayscale(1) brightness(1.1);
}

.floating-toolbox.open [toolbox-toggle] {
    background-color: var(--color-secondary);
    color: rgba(0, 0, 0, 0.5) !important;
}


html.dark-mode hr.primary-background {
    background-color: var(--color-secondary) !important;
}

html.dark-mode table td,
html.dark-mode table th {
    border-color: rgba(255, 255, 255, 0.10);
}


/* TYPOGRAPHY STYLES */

h1,
h1.list-heading {
    font-size: 2.488rem;
}

h2 {
    font-size: 2.074rem;
}

h3 {
    font-size: 1.728rem;
}

h4 {
    font-size: 1.44rem;
}

h5 {
    font-size: 1.2rem;
}



#recently-viewed h4,
#recent-pages h4,
.dropdown-search .dropdown-search-list h4 {
    font-size: 1rem;
}

.entity-list .content h4 {
    font-size: 1rem;
}

/* POPUP STYLES */

html.dark-mode .popup-body {
    background-color: #333;
}

html.dark-mode .popup-body a {
    color: var(--color-secondary);
}

html.dark-mode .popup-body a:hover {
    color: white;
    text-decoration: none;
}



html.dark-mode .popup-body .input-base,
html.dark-mode .popup-body input[type=text],
html.dark-mode .popup-body input[type=number],
html.dark-mode .popup-body input[type=email],
html.dark-mode .popup-body input[type=date],
html.dark-mode .popup-body input[type=search],
html.dark-mode .popup-body input[type=url],
html.dark-mode .popup-body input[type=color],
html.dark-mode .popup-body input[type=password],
html.dark-mode .popup-body select,
html.dark-mode .popup-body textarea,
html.dark-mode .popup-body .fake-input {
    background-color: #2b2b2b;
}

html.dark-mode .breadcrumbs {
    --color-primary: var(--color-secondary);
}

html.dark-mode .page-content a {
    --color-primary: var(--color-secondary);
}

</style>
```
</details>
