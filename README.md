# 🧩 Web Dev Perplexities & Solutions Snippets
### A curated gallery of single-file demos solving frustrating browser quirks and modern API "gotchas."

## 🧭 Table of Contents
1. [CSS Typed OM & attributeStyleMap](#css-typed-om-and-attributeStyleMap)
2. [Houdini Typed OM & Variable Fonts](#houdini-typed-om--variable-fonts)
3. [Upcoming Demos](#upcoming-demos)

---

## **PERPLEXITY #1**:  CSS Typed OM & attributeStyleMap
This demo addresses the issue where `attributeStyleMap.set()` rejects `CSS.number()` or `CSSKeywordValue()` in certain browser versions.

[🔗 View Source Code](./css-typed-om-solutions.html) | [🚀 Live Preview](https://brandtryan.github.io)  

## **PERPLEXITY #2**:  Houdini Typed OM & Variable Fonts
This demo solves the "string-to-number" friction. By registering custom properties with `@property`, we can set values as strings but read them back as **true JavaScript numbers** (not strings!) via `computedStyleMap()`.

[🔗 View Source Code](./Houdini-Typed-OM-Fonts.html)
</br>
</br> 


## Upcoming Demos (Roadmap)
- [ ] Container Queries + Hidden Overflow bugs
- [ ] Subgrid alignment edge cases
- [ ] View Transitions API for multi-page apps  
</br>
</br>  
>[!NOTE]
After researching problems and finding workarounds, I'll often post a demo and
it's likely I'll have entrusted AI to create the convenient single html files. My time is better spent making sure the code is commented sufficiently to explain the problem and solution.  

</br>
© 2026 Brandt Ryan [Apache Software License 2.0](LICENSE)
