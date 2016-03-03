## Cave
A portofolio website

### Polymer
This website is written with Polymer, a library whose purpose is to showcase what could be done in the future with coming web technologies: custom elements, shadow DOM, html imports and innert html templates.

### Lessons learned
#### Web components
A web component is a handy mix of html (view), js (controller) and css. The syntax is different, but in terms of functionality a polymer component resembles an angular directive, the major difference being that style is also included. Web components are the basic building blocks of a Polymer application. The very cool thing is that they provide a simple interface to customize them through the so-called "declared properties". `<iron-ajax>` for example makes it possible to easily configure an ajax request and expose the response to the local nodes. For example to query a static json document and expose `projects` to the local DOM:
```html
<iron-ajax auto url="../../data/webProjects.json" handle-as="json" last-response="{{projects}}"></iron-ajax>
```
#### Styling
Shadow DOM makes it hard at the start to understand how elements are styled. Elements are no more styled based on cascading css properties and their specificity at the global document level, but at the web component level. How do you set global styles then? Or style the elements inside a web component from the outside? Styles shared by all components can be put into a shared-styles documents and inmported by all components. Another pattern consists in styling your web components based on css properties and mixins (using [css variables] (https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_variables) defined outside the component.

Styling in Polymer still has limitations however. As in many browsers don't have a Shadow DOM, it is polyfilled in Polymer with Shady DOM, in a way that for performance reasons doesn't perfectly mimic the Shadow DOM specification. For example in a few non-unusual situations style changes are not automatically applied and have to be triggered manually. This is the case for example if you want to redefine custom css properties at different screen sizes based on media queries. DOM manipulations also have to occur through a dedicated API so that shady DOM understands what's happening.

#### Performance
elements.html, the file where all the web components are "vulcanized" (merged), weighs around 150kB in my case. Optimizations can certainly be done, but by default it is something you have to pay attention to when building a Polymer project. Also bootstraping takes time on mobile devices, it has to be measured why but it may be due to the web components polyfill also.

#### Routing
An external library has to be used for routing.
